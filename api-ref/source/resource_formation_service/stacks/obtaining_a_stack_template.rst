:original_name: GetStackTemplate.html

.. _GetStackTemplate:

Obtaining a Stack Template
==========================

Function
--------

This API obtains the template used for the current deployment if the stack is in the final state.

Note: When a stack is in a non-final state (ending with IN_PROGRESS), the stack is in the transition phase. This API obtains the template used for the last deployment of the stack. Only when the stack is in the final state (ending with COMPLETE or FAILED), this API obtains the template used for the current deployment. CREATION_COMPLETE is an exception because there is no template yet and 404 is returned, indicating that the template does not exist.

The non-final states may include:

-  DEPLOYMENT_IN_PROGRESS
-  ROLLBACK_IN_PROGRESS
-  DELETION_IN_PROGRESS

The final states may include:

-  CREATION_COMPLETE (an empty stack has been created)
-  DEPLOYMENT_FAILED
-  DEPLOYMENT_COMPLETE
-  ROLLBACK_FAILED
-  ROLLBACK_COMPLETE
-  DELETION_FAILED

If the template is successfully obtained, the template download link (OBS presigned URL, valid for 5 minutes) is returned in temporary redirection mode. Most clients automatically redirect and download the template. If automatic redirection is not performed, refer to the HTTP redirection rule and manually download the template.

URI
---

GET /v1/{project_id}/stacks/{stack_name}/templates

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

**Status code: 307**

.. table:: **Table 4** Response header parameters

   +-----------+--------+----------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter | Type   | Description                                                                                                                            |
   +===========+========+========================================================================================================================================+
   | Location  | String | HTTP redirect header. The client can use this header to redirect to a template download link (OBS presigned URL, valid for 5 minutes). |
   +-----------+--------+----------------------------------------------------------------------------------------------------------------------------------------+

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

**Status code: 429**

.. table:: **Table 9** Response body parameters

   ========== ====== =================
   Parameter  Type   Description
   ========== ====== =================
   error_code String Response code.
   error_msg  String Response message.
   ========== ====== =================

**Status code: 500**

.. table:: **Table 10** Response body parameters

   ========== ====== =================
   Parameter  Type   Description
   ========== ====== =================
   error_code String Response code.
   error_msg  String Response message.
   ========== ====== =================

Example Requests
----------------

-  Obtain a stack template.

   .. code-block:: text

      GET https://{endpoint}/v1/ba2b9930c977f71edaeaa3a5e96a8ff1/stacks/my_hello_world_stack/templates

-  Obtain a stack template and check whether the stack ID matches the current stack.

   .. code-block:: text

      GET https://{endpoint}/v1/ba2b9930c977f71edaeaa3a5e96a8ff1/stacks/my_hello_world_stack/templates?stack_id=ea6a4f0e-ee8a-494e-b12a-8be4a1e65af2

Example Responses
-----------------

None

Status Codes
------------

=========== =======================================================
Status Code Description
=========== =======================================================
307         Stack template obtained. Temporary redirect.
400         Invalid request.
401         Authentication failed.
403         The user does not have the permission to call this API.
404         The stack or template does not exist.
429         Too frequent requests.
500         Internal server error.
=========== =======================================================
