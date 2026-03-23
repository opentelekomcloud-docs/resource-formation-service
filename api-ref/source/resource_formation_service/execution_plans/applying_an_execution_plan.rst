:original_name: ApplyExecutionPlan.html

.. _ApplyExecutionPlan:

Applying an Execution Plan
==========================

Function
--------

This API applies an execution plan.

-  Once the execution request is received, the state of the execution plan changes to APPLY_IN_PROGRESS, and the request is processed asynchronously in the background.
-  Once the execution is completed, the state of the execution plan changes to APPLIED.
-  You can call :ref:`GetStackMetadata <getstackmetadata>` to query the stack status to trace the stack deployment status and check whether the execution is successful.

If you do not want to deploy a stack using an execution plan, you can call :ref:`DeployStack <deploystack>` for direct deployment.

Expiration of execution plans:

#. If a stack has multiple execution plans, all the remaining plans will expire once any of them is applied (regardless of whether the execution is successful).
#. If the specified execution plan has expired when you call ApplyExecutionPlan, 403 is returned. If a stack is in a non-final state (ending with IN_PROGRESS), its execution plans cannot be applied and 403 is returned. The non-final states may include:

-  DEPLOYMENT_IN_PROGRESS
-  DELETION_IN_PROGRESS
-  ROLLBACK_IN_PROGRESS

URI
---

POST /v1/{project_id}/stacks/{stack_name}/execution-plans/{execution_plan_name}

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

Request Parameters
------------------

.. table:: **Table 2** Request header parameters

   +-------------------+-----------------+-----------------+--------------------------------------------------------------------------------------+
   | Parameter         | Mandatory       | Type            | Description                                                                          |
   +===================+=================+=================+======================================================================================+
   | Client-Request-Id | Yes             | String          | A unique request ID is specified by a user to locate a request. UUID is recommended. |
   |                   |                 |                 |                                                                                      |
   |                   |                 |                 | Minimum: **36**                                                                      |
   |                   |                 |                 |                                                                                      |
   |                   |                 |                 | Maximum: **128**                                                                     |
   +-------------------+-----------------+-----------------+--------------------------------------------------------------------------------------+

.. table:: **Table 3** Request body parameters

   +-------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter         | Mandatory       | Type            | Description                                                                                                                                                                                                                |
   +===================+=================+=================+============================================================================================================================================================================================================================+
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

Response Parameters
-------------------

**Status code: 202**

.. table:: **Table 4** Response body parameters

   +---------------+--------+-----------------------------------------------------------------------------------------------+
   | Parameter     | Type   | Description                                                                                   |
   +===============+========+===============================================================================================+
   | deployment_id | String | Unique deployment ID. It is a UUID generated by RFS when deployment or rollback is triggered. |
   +---------------+--------+-----------------------------------------------------------------------------------------------+

**Status code: 400**

.. table:: **Table 5** Response body parameters

   ========== ====== =================
   Parameter  Type   Description
   ========== ====== =================
   error_code String Response code.
   error_msg  String Response message.
   ========== ====== =================

**Status code: 401**

.. table:: **Table 6** Response body parameters

   ========== ====== =================
   Parameter  Type   Description
   ========== ====== =================
   error_code String Response code.
   error_msg  String Response message.
   ========== ====== =================

**Status code: 403**

.. table:: **Table 7** Response body parameters

   ========== ====== =================
   Parameter  Type   Description
   ========== ====== =================
   error_code String Response code.
   error_msg  String Response message.
   ========== ====== =================

**Status code: 404**

.. table:: **Table 8** Response body parameters

   ========== ====== =================
   Parameter  Type   Description
   ========== ====== =================
   error_code String Response code.
   error_msg  String Response message.
   ========== ====== =================

**Status code: 409**

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

-  Apply an execution plan of a specified stack.

   .. code-block:: text

      POST https://{endpoint}/v1/ba2b9930c977f71edaeaa3a5e96a8ff1/stacks/my_hello_world_stack/execution-plans/my_first_execution_plan

-  Apply an execution plan of a specified stack, with a stack ID provided to check whether the stack ID matches the current stack.

   .. code-block:: text

      POST https://{endpoint}/v1/ba2b9930c977f71edaeaa3a5e96a8ff1/stacks/my_hello_world_stack/execution-plans/my_first_execution_plan

      {
        "stack_id" : "f689e9fd-97e7-4185-bd8a-7d5f708d45d7"
      }

Example Responses
-----------------

**Status code: 202**

The request is accepted and processed asynchronously.

.. code-block::

   {
     "deployment_id" : "07e21c3e-d33c-4513-9d0f-e9e673817772"
   }

Status Codes
------------

+-----------------------------------+----------------------------------------------------------------------------------------+
| Status Code                       | Description                                                                            |
+===================================+========================================================================================+
| 202                               | The request is accepted and processed asynchronously.                                  |
+-----------------------------------+----------------------------------------------------------------------------------------+
| 400                               | Invalid request.                                                                       |
+-----------------------------------+----------------------------------------------------------------------------------------+
| 401                               | Authentication failed.                                                                 |
+-----------------------------------+----------------------------------------------------------------------------------------+
| 403                               | #. The user does not have the permission to call this API.                             |
|                                   | #. Invalid stack status.                                                               |
|                                   | #. The execution plan has expired.                                                     |
+-----------------------------------+----------------------------------------------------------------------------------------+
| 404                               | #. The stack does not exist.                                                           |
|                                   | #. The execution plan does not exist.                                                  |
+-----------------------------------+----------------------------------------------------------------------------------------+
| 409                               | Execution requests conflict. Another request is being processed on the execution plan. |
+-----------------------------------+----------------------------------------------------------------------------------------+
| 429                               | Too frequent requests.                                                                 |
+-----------------------------------+----------------------------------------------------------------------------------------+
| 500                               | Internal server error.                                                                 |
+-----------------------------------+----------------------------------------------------------------------------------------+
