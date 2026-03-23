:original_name: ContinueRollbackStack.html

.. _ContinueRollbackStack:

Continuing to Roll Back a Stack
===============================

Function
--------

This API continues to roll back an existing stack.

If auto-rollback is enabled for a stack, the stack automatically rolls back when its deployment fails. However, the auto-rollback may fail. You can troubleshoot the issues based on the error message and then call ContinueRollbackStack to trigger the continuation of the rollback, which means retrying rollback.

-  If the stack is in the *ROLLBACK_FAILED* state, indicating that it can be rolled back, 202 and deploymentId are returned. Otherwise, the stack cannot be rolled back and a response error code is returned.
-  The continuation of rollback may also fail. If it fails, you can obtain the corresponding logs by calling :ref:`ListStackEvents <liststackevents>` and troubleshoot the issues. Once the issues are resolved, you can call :ref:`ContinueRollbackStack <continuerollbackstack>` again to trigger the rollback.

URI
---

POST /v1/{project_id}/stacks/{stack_name}/rollbacks

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

Response Parameters
-------------------

**Status code: 202**

.. table:: **Table 4** Response body parameters

   +---------------+--------+-----------------------------------------------------------------------------------------------------------------+
   | Parameter     | Type   | Description                                                                                                     |
   +===============+========+=================================================================================================================+
   | deployment_id | String | Unique ID of the deployment triggered by continuing rollback. The ID is generated by RFS and is usually a UUID. |
   +---------------+--------+-----------------------------------------------------------------------------------------------------------------+

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

-  Continue to roll back a stack.

   .. code-block:: text

      POST https://{endpoint}/v1/ba2b9930c977f71edaeaa3a5e96a8ff1/stacks/my_hello_world_stack/rollbacks

-  Continue to roll back a stack and check whether the provided stack ID matches the current stack.

   .. code-block:: text

      POST https://{endpoint}/v1/ba2b9930c977f71edaeaa3a5e96a8ff1/stacks/my_hello_world_stack/rollbacks

      {
        "stack_id" : "8592967b-18b0-421b-b6c1-079c9ded3931"
      }

Example Responses
-----------------

**Status code: 202**

The request is accepted. The stack continues to roll back.

.. code-block::

   {
     "deployment_id" : "8592967b-18b0-421b-b6c1-079c9ded3931"
   }

Status Codes
------------

+-----------------------------------+----------------------------------------------------------------------------+
| Status Code                       | Description                                                                |
+===================================+============================================================================+
| 202                               | The request is accepted. The stack continues to roll back.                 |
+-----------------------------------+----------------------------------------------------------------------------+
| 400                               | Invalid request.                                                           |
+-----------------------------------+----------------------------------------------------------------------------+
| 401                               | Authentication failed.                                                     |
+-----------------------------------+----------------------------------------------------------------------------+
| 403                               | #. Invalid stack status.                                                   |
|                                   | #. The user does not have the permission to call this API.                 |
+-----------------------------------+----------------------------------------------------------------------------+
| 404                               | The stack does not exist.                                                  |
+-----------------------------------+----------------------------------------------------------------------------+
| 409                               | Request conflict. Another request is being processed on the current stack. |
+-----------------------------------+----------------------------------------------------------------------------+
| 429                               | Too frequent requests.                                                     |
+-----------------------------------+----------------------------------------------------------------------------+
| 500                               | Internal server error.                                                     |
+-----------------------------------+----------------------------------------------------------------------------+
