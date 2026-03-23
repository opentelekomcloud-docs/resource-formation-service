:original_name: DeleteStack.html

.. _DeleteStack:

Deleting a Stack
================

Function
--------

This API deletes a stack. **Exercise caution when performing this operation. Deleting a stack will delete all data related to the stack by default, such as execution plans, stack events, stack outputs, and resources.**

-  This API triggers the deletion of a stack, and all data of the stack is deleted for eventual consistency. You can call :ref:`GetStackMetadata <getstackmetadata>` or :ref:`ListStacks <liststacks>` to track the deletion.
-  A stack cannot be deleted if it is in a non-final state (ending with *IN_PROGRESS*). The states may include:

   -  DEPLOYMENT_IN_PROGRESS
   -  DELETION_IN_PROGRESS
   -  ROLLBACK_IN_PROGRESS

-  If deletion protection is enabled for a stack, the stack cannot be deleted. You can call :ref:`GetStackMetadata <getstackmetadata>` and view the *enable_deletion_protection* field in the returned result to check whether deletion protection is enabled. You can call :ref:`UpdateStack <updatestack>` to disable deletion protection.
-  If the deletion of a stack fails, you can correct the current template based on the information in StackEvents, and delete the stack again after completing deployment. Deployment can be triggered in either of the following ways:

   -  Call :ref:`CreateExecutionPlan <createexecutionplan>` to create an execution plan. After the execution plan is created, call :ref:`ApplyExecutionPlan <applyexecutionplan>` to deploy the stack.
   -  Call :ref:`DeployStack <deploystack>` to deploy the stack.

URI
---

DELETE /v1/{project_id}/stacks/{stack_name}

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

**Status code: 429**

.. table:: **Table 8** Response body parameters

   ========== ====== =================
   Parameter  Type   Description
   ========== ====== =================
   error_code String Response code.
   error_msg  String Response message.
   ========== ====== =================

**Status code: 500**

.. table:: **Table 9** Response body parameters

   ========== ====== =================
   Parameter  Type   Description
   ========== ====== =================
   error_code String Response code.
   error_msg  String Response message.
   ========== ====== =================

Example Requests
----------------

-  Delete a specified stack.

   .. code-block:: text

      DELETE https://{endpoint}/v1/ba2b9930c977f71edaeaa3a5e96a8ff1/stacks/my_hello_world_stack

-  Delete a specified stack and check whether the provided stack ID matches the current stack.

   .. code-block:: text

      DELETE https://{endpoint}/v1/ba2b9930c977f71edaeaa3a5e96a8ff1/stacks/my_hello_world_stack?stack_id=ea6a4f0e-ee8a-494e-b12a-8be4a1e65af2

Example Responses
-----------------

None

Status Codes
------------

+-----------------------------------+------------------------------------------------------------+
| Status Code                       | Description                                                |
+===================================+============================================================+
| 202                               | The request is accepted and processed asynchronously.      |
+-----------------------------------+------------------------------------------------------------+
| 400                               | Invalid request.                                           |
+-----------------------------------+------------------------------------------------------------+
| 401                               | Authentication failed.                                     |
+-----------------------------------+------------------------------------------------------------+
| 403                               | #. Invalid stack status.                                   |
|                                   | #. The user does not have the permission to call this API. |
+-----------------------------------+------------------------------------------------------------+
| 404                               | The stack does not exist.                                  |
+-----------------------------------+------------------------------------------------------------+
| 429                               | Too frequent requests.                                     |
+-----------------------------------+------------------------------------------------------------+
| 500                               | Internal server error.                                     |
+-----------------------------------+------------------------------------------------------------+
