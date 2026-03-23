:original_name: DeleteExecutionPlan.html

.. _DeleteExecutionPlan:

Deleting an Execution Plan
==========================

Function
--------

This API deletes an execution plan.

If an execution plan is in a CREATION_IN_PROGRESS or APPLY_IN_PROGRESS state, the execution plan cannot be deleted and 403 is returned.

URI
---

DELETE /v1/{project_id}/stacks/{stack_name}/execution-plans/{execution_plan_name}

.. table:: **Table 1** Path Parameters

   +---------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter           | Mandatory       | Type            | Description                                                                                                                                                                                                                            |
   +=====================+=================+=================+========================================================================================================================================================================================================================================+
   | project_id          | Yes             | String          | A project ID is obtained by calling an API or from the console.                                                                                                                                                                        |
   |                     |                 |                 |                                                                                                                                                                                                                                        |
   |                     |                 |                 | Minimum: **3**                                                                                                                                                                                                                         |
   |                     |                 |                 |                                                                                                                                                                                                                                        |
   |                     |                 |                 | Maximum: **64**                                                                                                                                                                                                                        |
   +---------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | stack_name          | Yes             | String          | A stack name is unique within its domain (domain_id), region, and project (project_id). It is case-sensitive and starts with a letter. Only letters, digits, underscores (_), and hyphens (-) are allowed.                             |
   |                     |                 |                 |                                                                                                                                                                                                                                        |
   |                     |                 |                 | Minimum: **1**                                                                                                                                                                                                                         |
   |                     |                 |                 |                                                                                                                                                                                                                                        |
   |                     |                 |                 | Maximum: **128**                                                                                                                                                                                                                       |
   +---------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | execution_plan_name | Yes             | String          | An execution plan name is unique within its domain (domain_id), region, project (project_id), and stack (stack_id). It is case-sensitive and starts with a letter. Only letters, digits, underscores (_), and hyphens (-) are allowed. |
   |                     |                 |                 |                                                                                                                                                                                                                                        |
   |                     |                 |                 | Minimum: **1**                                                                                                                                                                                                                         |
   |                     |                 |                 |                                                                                                                                                                                                                                        |
   |                     |                 |                 | Maximum: **128**                                                                                                                                                                                                                       |
   +---------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. table:: **Table 2** Query Parameters

   +-------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter         | Mandatory       | Type            | Description                                                                                                                                                                                                                |
   +===================+=================+=================+============================================================================================================================================================================================================================+
   | stack_id          | No              | String          | Unique stack ID.                                                                                                                                                                                                           |
   |                   |                 |                 |                                                                                                                                                                                                                            |
   |                   |                 |                 | It is a UUID generated by RFS when a stack is created.                                                                                                                                                                     |
   |                   |                 |                 |                                                                                                                                                                                                                            |
   |                   |                 |                 | Stack name is unique, if you create stack with name ‘HelloWorld’, the same name cannot be used for another stack until original stack is deleted.                                                                          |
   |                   |                 |                 |                                                                                                                                                                                                                            |
   |                   |                 |                 | For parallel development, team members may want to ensure that they are operating the stack they created, not one with the same name created by other members after deleting the previous one.                             |
   |                   |                 |                 |                                                                                                                                                                                                                            |
   |                   |                 |                 | To avoid this mismatch, check the ID, since RFS ensures each stack has a unique ID that does not change with updates. If the stack_id value differs from the current stack ID, 400 is returned.                            |
   |                   |                 |                 |                                                                                                                                                                                                                            |
   |                   |                 |                 | Minimum: **36**                                                                                                                                                                                                            |
   |                   |                 |                 |                                                                                                                                                                                                                            |
   |                   |                 |                 | Maximum: **36**                                                                                                                                                                                                            |
   +-------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | execution_plan_id | No              | String          | Unique execution plan ID.                                                                                                                                                                                                  |
   |                   |                 |                 |                                                                                                                                                                                                                            |
   |                   |                 |                 | A UUID is generated by RFS when an execution plan is created.                                                                                                                                                              |
   |                   |                 |                 |                                                                                                                                                                                                                            |
   |                   |                 |                 | Execution plan name is unique, if you create execution plan with name ‘HelloWorld’, the same name cannot be used for another execution plan until original execution plan is deleted.                                      |
   |                   |                 |                 |                                                                                                                                                                                                                            |
   |                   |                 |                 | For parallel development, team members may want to ensure that they are operating the execution plan they created, not one with the same name created by other members after deleting the previous one.                    |
   |                   |                 |                 |                                                                                                                                                                                                                            |
   |                   |                 |                 | To avoid this mismatch, check the ID, since RFS ensures each execution plan has a unique ID that does not change with updates. If the execution_plan_id value differs from the current execution plan ID, 400 is returned. |
   |                   |                 |                 |                                                                                                                                                                                                                            |
   |                   |                 |                 | Minimum: **36**                                                                                                                                                                                                            |
   |                   |                 |                 |                                                                                                                                                                                                                            |
   |                   |                 |                 | Maximum: **36**                                                                                                                                                                                                            |
   +-------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

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

Response Parameters
-------------------

**Status code: 400**

.. table:: **Table 4** Response body parameters

   ========== ====== =================
   Parameter  Type   Description
   ========== ====== =================
   error_code String Response code.
   error_msg  String Response message.
   ========== ====== =================

**Status code: 401**

.. table:: **Table 5** Response body parameters

   ========== ====== =================
   Parameter  Type   Description
   ========== ====== =================
   error_code String Response code.
   error_msg  String Response message.
   ========== ====== =================

**Status code: 403**

.. table:: **Table 6** Response body parameters

   ========== ====== =================
   Parameter  Type   Description
   ========== ====== =================
   error_code String Response code.
   error_msg  String Response message.
   ========== ====== =================

**Status code: 404**

.. table:: **Table 7** Response body parameters

   ========== ====== =================
   Parameter  Type   Description
   ========== ====== =================
   error_code String Response code.
   error_msg  String Response message.
   ========== ====== =================

**Status code: 500**

.. table:: **Table 8** Response body parameters

   ========== ====== =================
   Parameter  Type   Description
   ========== ====== =================
   error_code String Response code.
   error_msg  String Response message.
   ========== ====== =================

Example Requests
----------------

-  Delete an execution plan of a specified stack.

   .. code-block:: text

      DELETE https://{endpoint}/v1/ba2b9930c977f71edaeaa3a5e96a8ff1/stacks/my_hello_world_stack/execution-plans/my_first_execution_plan

-  Delete an execution plan of a specified stack, with a stack ID and an execution plan ID provided to check whether they match the current stack and execution plan.

   .. code-block:: text

      DELETE https://{endpoint}/v1/ba2b9930c977f71edaeaa3a5e96a8ff1/stacks/my_hello_world_stack/execution-plans/my_first_execution_plan?stack_id=ea6a4f0e-ee8a-494e-b12a-8be4a1e65af2&execution_plan_id=fb5e781e-a27d-46e2-9954-242753857a9f

Example Responses
-----------------

None

Status Codes
------------

+-----------------------------------+--------------------------------------------------------------------+
| Status Code                       | Description                                                        |
+===================================+====================================================================+
| 204                               | Execution plan deleted.                                            |
+-----------------------------------+--------------------------------------------------------------------+
| 400                               | Invalid request.                                                   |
+-----------------------------------+--------------------------------------------------------------------+
| 401                               | Authentication failed.                                             |
+-----------------------------------+--------------------------------------------------------------------+
| 403                               | #. The user does not have the permission to call this API.         |
|                                   | #. The execution plan cannot be deleted due to its invalid status. |
+-----------------------------------+--------------------------------------------------------------------+
| 404                               | #. The stack does not exist.                                       |
|                                   | #. The execution plan does not exist.                              |
+-----------------------------------+--------------------------------------------------------------------+
| 500                               | Internal server error.                                             |
+-----------------------------------+--------------------------------------------------------------------+
