:original_name: DeleteStackEnhanced.html

.. _DeleteStackEnhanced:

Deleting a Stack with Conditions
================================

Function
--------

This API deletes a stack with conditions. You can determine whether to retain resources. **Exercise caution when performing this operation. Deleting a stack will delete all data related to the stack by default, such as execution plans, stack events, stack outputs, and resources.** **If you want to retain stack resources when deleting the stack, specify retain_all_resources in the request.**

-  This API triggers the deletion of a stack, and all data of the stack is deleted for eventual consistency. You can call :ref:`GetStackMetadata <getstackmetadata>` or :ref:`ListStacks <liststacks>` to track the deletion. After the deletion is complete, the deleted stack will not be returned in the preceding API.
-  A stack cannot be deleted if it is in a non-final state (ending with *IN_PROGRESS*). The states may include:

   -  DEPLOYMENT_IN_PROGRESS
   -  DELETION_IN_PROGRESS
   -  ROLLBACK_IN_PROGRESS

-  If deletion protection is enabled for a stack, the stack cannot be deleted. You can call :ref:`GetStackMetadata <getstackmetadata>` and view the *enable_deletion_protection* field in the returned result to check whether deletion protection is enabled. You can call :ref:`UpdateStack <updatestack>` to disable deletion protection.
-  If the deletion of a stack fails, you can correct the current template based on the information in :ref:`StackEvents <liststackevents>`, and delete the stack again after completing deployment. Deployment can be triggered in either of the following ways:

   -  Call :ref:`CreateExecutionPlan <createexecutionplan>` to create an execution plan. After the execution plan is created, call :ref:`ApplyExecutionPlan <applyexecutionplan>` to deploy the stack.
   -  Call :ref:`DeployStack <deploystack>` to deploy the stack.

URI
---

POST /v1/{project_id}/stacks/{stack_name}/deletion

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

   +----------------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter            | Mandatory       | Type            | Description                                                                                                                                                                                                                                                |
   +======================+=================+=================+============================================================================================================================================================================================================================================================+
   | stack_id             | No              | String          | Unique stack ID.                                                                                                                                                                                                                                           |
   |                      |                 |                 |                                                                                                                                                                                                                                                            |
   |                      |                 |                 | It is a UUID generated by RFS when a stack is created.                                                                                                                                                                                                     |
   |                      |                 |                 |                                                                                                                                                                                                                                                            |
   |                      |                 |                 | Stack name is unique, if you create stack with name ‘HelloWorld’, the same name cannot be used for another stack until original stack is deleted.                                                                                                          |
   |                      |                 |                 |                                                                                                                                                                                                                                                            |
   |                      |                 |                 | For parallel development, team members may want to ensure that they are operating the stack they created, not one with the same name created by other members after deleting the previous one.                                                             |
   |                      |                 |                 |                                                                                                                                                                                                                                                            |
   |                      |                 |                 | To avoid this mismatch, check the ID, since RFS ensures each stack has a unique ID that does not change with updates. If the stack_id value differs from the current stack ID, 400 is returned.                                                            |
   |                      |                 |                 |                                                                                                                                                                                                                                                            |
   |                      |                 |                 | Minimum: **36**                                                                                                                                                                                                                                            |
   |                      |                 |                 |                                                                                                                                                                                                                                                            |
   |                      |                 |                 | Maximum: **36**                                                                                                                                                                                                                                            |
   +----------------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | retain_all_resources | No              | Boolean         | Indicates whether to retain resources when deleting a stack. If this variable is not assigned, the default value **false** is used, indicating that resources are not retained by default. (After a stack is deleted, resources in the stack are deleted.) |
   |                      |                 |                 |                                                                                                                                                                                                                                                            |
   |                      |                 |                 | -  In the :ref:`DeleteStackEnhanced <deletestackenhanced>` API, if this variable is not assigned in the RequestBody, the resources in the stack are not retained during deletion.                                                                          |
   +----------------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

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

-  Delete a stack without retaining resources.

   .. code-block:: text

      POST https://{endpoint}/v1/{project_id}/stacks/{stack_name}/deletion

      {
        "stack_id" : "1b15e005-bdbb-4bd7-8f9a-a09b6774b4b3"
      }

-  Delete a stack while retaining resources.

   .. code-block:: text

      POST https://{endpoint}/v1/{project_id}/stacks/{stack_name}/deletion

      {
        "stack_id" : "1b15e005-bdbb-4bd7-8f9a-a09b6774b4b3",
        "retain_all_resources" : true
      }

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
