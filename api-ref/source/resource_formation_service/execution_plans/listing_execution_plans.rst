:original_name: ListExecutionPlans.html

.. _ListExecutionPlans:

Listing Execution Plans
=======================

Function
--------

This API lists all execution plans of a specified stack in the current region.

-  By default, the execution plans are sorted by creation time in descending order. The one created latest is displayed on the top.
-  Currently, all of the existing execution plans are returned. Pagination is not supported.
-  If the specified stack does not have any execution plan, an empty list is returned.
-  If the specified stack does not exist, 404 is returned. ListExecutionPlans returns only the summary information. You can obtain details about the summary information by referring to :ref:`Response Parameters <listexecutionplans__section15725105016414>`. For detailed execution plan metadata, call :ref:`GetExecutionPlanMetadata <getexecutionplanmetadata>`.

URI
---

GET /v1/{project_id}/stacks/{stack_name}/execution-plans

.. table:: **Table 1** Path Parameters

   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                                                                                                                                |
   +=================+=================+=================+============================================================================================================================================================================================================+
   | project_id      | Yes             | String          | A project ID is obtained by calling an API or from the console.                                                                                                                                            |
   |                 |                 |                 |                                                                                                                                                                                                            |
   |                 |                 |                 | Minimum: **3**                                                                                                                                                                                             |
   |                 |                 |                 |                                                                                                                                                                                                            |
   |                 |                 |                 | Maximum: **64**                                                                                                                                                                                            |
   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | stack_name      | Yes             | String          | A stack name is unique within its domain (domain_id), region, and project (project_id). It is case-sensitive and starts with a letter. Only letters, digits, underscores (_), and hyphens (-) are allowed. |
   |                 |                 |                 |                                                                                                                                                                                                            |
   |                 |                 |                 | Minimum: **1**                                                                                                                                                                                             |
   |                 |                 |                 |                                                                                                                                                                                                            |
   |                 |                 |                 | Maximum: **128**                                                                                                                                                                                           |
   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. table:: **Table 2** Query Parameters

   +-----------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                                                                                                                     |
   +=================+=================+=================+=================================================================================================================================================================================================+
   | stack_id        | No              | String          | Unique stack ID.                                                                                                                                                                                |
   |                 |                 |                 |                                                                                                                                                                                                 |
   |                 |                 |                 | It is a UUID generated by RFS when a stack is created.                                                                                                                                          |
   |                 |                 |                 |                                                                                                                                                                                                 |
   |                 |                 |                 | Stack name is unique, if you create stack with name ‘HelloWorld’, the same name cannot be used for another stack until original stack is deleted.                                               |
   |                 |                 |                 |                                                                                                                                                                                                 |
   |                 |                 |                 | For parallel development, team members may want to ensure that they are operating the stack they created, not one with the same name created by other members after deleting the previous one.  |
   |                 |                 |                 |                                                                                                                                                                                                 |
   |                 |                 |                 | To avoid this mismatch, check the ID, since RFS ensures each stack has a unique ID that does not change with updates. If the stack_id value differs from the current stack ID, 400 is returned. |
   |                 |                 |                 |                                                                                                                                                                                                 |
   |                 |                 |                 | Minimum: **36**                                                                                                                                                                                 |
   |                 |                 |                 |                                                                                                                                                                                                 |
   |                 |                 |                 | Maximum: **36**                                                                                                                                                                                 |
   +-----------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Request Parameters
------------------

.. table:: **Table 3** Request header parameters

   +-------------------+-----------------+-----------------+--------------------------------------------------------------------------------------+
   | Parameter         | Mandatory       | Type            | Description                                                                          |
   +===================+=================+=================+======================================================================================+
   | Client-Request-Id | Yes             | String          | A unique request ID is specified by a user to locate a request. UUID is recommended. |
   |                   |                 |                 |                                                                                      |
   |                   |                 |                 | Minimum: **36**                                                                      |
   |                   |                 |                 |                                                                                      |
   |                   |                 |                 | Maximum: **128**                                                                     |
   +-------------------+-----------------+-----------------+--------------------------------------------------------------------------------------+

.. _listexecutionplans__section15725105016414:

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 4** Response body parameters

   +-----------------+-----------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type                                                                                                            | Description                                                                                                       |
   +=================+=================================================================================================================+===================================================================================================================+
   | execution_plans | Array of :ref:`ExecutionPlan <listexecutionplans__en-us_topic_0000001757038293_response_executionplan>` objects | Execution plan list, sorted by creation time in descending order. The one created latest is displayed on the top. |
   +-----------------+-----------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------+

.. _listexecutionplans__en-us_topic_0000001757038293_response_executionplan:

.. table:: **Table 5** ExecutionPlan

   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                                                                                                                              |
   +=======================+=======================+==========================================================================================================================================================================================================+
   | stack_name            | String                | A stack name is unique within its domain (domain_id), region, and project (project_id).                                                                                                                  |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | stack_id              | String                | Unique stack ID.                                                                                                                                                                                         |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | execution_plan_id     | String                | Unique execution plan ID.                                                                                                                                                                                |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | execution_plan_name   | String                | An execution plan name is unique within its domain (domain_id), region, project (project_id), and stack (stack_id).                                                                                      |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | description           | String                | Execution plan description. It is used to identify your own execution plans. If this field was not set earlier, it will not be returned in this request.                                                 |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | status                | String                | Status of an execution plan.                                                                                                                                                                             |
   |                       |                       |                                                                                                                                                                                                          |
   |                       |                       | -  CREATION_IN_PROGRESS indicates that creation is in progress.                                                                                                                                          |
   |                       |                       | -  CREATION_FAILED indicates the creation failed. You can obtain the error information summary from status_message.                                                                                      |
   |                       |                       | -  AVAILABLE indicates the creation completed. You can call ApplyExecutionPlan to apply the plan.                                                                                                        |
   |                       |                       | -  APPLY_IN_PROGRESS indicates the execution is in progress. You can call GetStackMetadata to query the stack status, or call ListStackEvents to obtain the stack events generated during the execution. |
   |                       |                       | -  APPLIED indicates the plan has been applied.                                                                                                                                                          |
   |                       |                       |                                                                                                                                                                                                          |
   |                       |                       | Enumeration values:                                                                                                                                                                                      |
   |                       |                       |                                                                                                                                                                                                          |
   |                       |                       | -  **CREATION_IN_PROGRESS**                                                                                                                                                                              |
   |                       |                       | -  **CREATION_FAILED**                                                                                                                                                                                   |
   |                       |                       | -  **AVAILABLE**                                                                                                                                                                                         |
   |                       |                       | -  **APPLY_IN_PROGRESS**                                                                                                                                                                                 |
   |                       |                       | -  **APPLIED**                                                                                                                                                                                           |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | status_message        | String                | If an execution plan is in a CREATION_FAILED status, a brief error information summary is displayed for debugging.                                                                                       |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | create_time           | String                | Creation time of an execution plan. The format complies with the RFC 3339 format (YYYY-MM-DDTHH:MM:SSZ), for example, 1970-01-01T00:00:00Z.                                                              |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | apply_time            | String                | Time when an execution plan was applied. The format complies with the RFC 3339 format (YYYY-MM-DDTHH:MM:SSZ), for example, 1970-01-01T00:00:00Z.                                                         |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

**Status code: 400**

.. table:: **Table 6** Response body parameters

   ========== ====== =================
   Parameter  Type   Description
   ========== ====== =================
   error_code String Response code.
   error_msg  String Response message.
   ========== ====== =================

**Status code: 401**

.. table:: **Table 7** Response body parameters

   ========== ====== =================
   Parameter  Type   Description
   ========== ====== =================
   error_code String Response code.
   error_msg  String Response message.
   ========== ====== =================

**Status code: 403**

.. table:: **Table 8** Response body parameters

   ========== ====== =================
   Parameter  Type   Description
   ========== ====== =================
   error_code String Response code.
   error_msg  String Response message.
   ========== ====== =================

**Status code: 404**

.. table:: **Table 9** Response body parameters

   ========== ====== =================
   Parameter  Type   Description
   ========== ====== =================
   error_code String Response code.
   error_msg  String Response message.
   ========== ====== =================

**Status code: 429**

.. table:: **Table 10** Response body parameters

   ========== ====== =================
   Parameter  Type   Description
   ========== ====== =================
   error_code String Response code.
   error_msg  String Response message.
   ========== ====== =================

**Status code: 500**

.. table:: **Table 11** Response body parameters

   ========== ====== =================
   Parameter  Type   Description
   ========== ====== =================
   error_code String Response code.
   error_msg  String Response message.
   ========== ====== =================

Example Requests
----------------

-  List all execution plans of a specified stack.

   .. code-block:: text

      GET https://{endpoint}/v1/ba2b9930c977f71edaeaa3a5e96a8ff1/stacks/my_hello_world_stack/execution-plans

-  List all execution plans of a specified stack with a stack ID to check whether the stack ID matches the current stack.

   .. code-block:: text

      GET https://{endpoint}/v1/ba2b9930c977f71edaeaa3a5e96a8ff1/stacks/my_hello_world_stack/execution-plans?stack_id=f689e9fd-97e7-4185-bd8a-7d5f708d45d7

Example Responses
-----------------

**Status code: 200**

Execution plans listed.

.. code-block::

   {
     "execution_plans" : [ {
       "stack_name" : "my_hello_world_stack",
       "stack_id" : "f689e9fd-97e7-4185-bd8a-7d5f708d45d7",
       "execution_plan_id" : "b3e7e15f-f96b-4190-94f4-bb8120f8c4dc",
       "execution_plan_name" : "my_third_execution_plan",
       "description" : "my third execution plan",
       "status" : "AVAILABLE",
       "create_time" : "2023-05-15T15:39:25Z"
     }, {
       "stack_name" : "my_hello_world_stack",
       "stack_id" : "f689e9fd-97e7-4185-bd8a-7d5f708d45d7",
       "execution_plan_id" : "3ca87537-8d5c-4c9d-9292-d19068aaacbb",
       "execution_plan_name" : "my_second_execution_plan",
       "description" : "my second execution plan",
       "status" : "APPLIED",
       "create_time" : "2023-05-15T15:32:45Z"
     }, {
       "stack_name" : "my_hello_world_stack",
       "stack_id" : "f689e9fd-97e7-4185-bd8a-7d5f708d45d7",
       "execution_plan_id" : "8c1fb31d-9eec-4ce3-a4e6-fd07059cec83",
       "execution_plan_name" : "my_first_execution_plan",
       "description" : "my first execution plan",
       "status" : "CREATION_FAILED",
       "status_message" : "Failed to init workflow due to bad template. Error: Invalid variable name A name must start with a letter or underscore and may contain only letters, digits, underscores, and dashes.",
       "create_time" : "2023-05-15T12:23:38Z"
     } ]
   }

Status Codes
------------

=========== =======================================================
Status Code Description
=========== =======================================================
200         Execution plans listed.
400         Invalid request.
401         Authentication failed.
403         The user does not have the permission to call this API.
404         The stack does not exist.
429         Too frequent requests.
500         Internal server error.
=========== =======================================================
