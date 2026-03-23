:original_name: UpdateStack.html

.. _UpdateStack:

Updating basic information of a Stack
=====================================

Function
--------

This API updates the attributes of a stack based on the information provided by users. One or more of the following attributes can be updated: **description**, **enable_deletion_protection**, **enable_auto_rollback**, and **agencies**.

This API updates only the fields contained in the information assigned by the user.

Note: All attributes are overwritten once updated. New parameters will overwrite original attributes of a stack.

For example, if you want to add agencies, call :ref:`GetStackMetadata <getstackmetadata>` to obtain the original agencies, integrate the information of old and new agencies, and then call :ref:`UpdateStack <updatestack>`.

-  A stack cannot be updated if it is in a non-final state (ending with *IN_PROGRESS*). The states may include:

   -  DEPLOYMENT_IN_PROGRESS
   -  DELETION_IN_PROGRESS
   -  ROLLBACK_IN_PROGRESS

-  If the value of enable_auto_rollback is changed from false to true, the stack state is determined more strictly. A stack cannot be updated if it is in a state ending with *\_FAILED*. The states may include:

   -  DEPLOYMENT_FAILED
   -  ROLLBACK_FAILED
   -  DELETION_FAILED

URI
---

PATCH /v1/{project_id}/stacks/{stack_name}

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

   +----------------------------+-----------------+-------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter                  | Mandatory       | Type                                                                                      | Description                                                                                                                                                                                                                                                                                                                                                                                                   |
   +============================+=================+===========================================================================================+===============================================================================================================================================================================================================================================================================================================================================================================================================+
   | description                | No              | String                                                                                    | Description of a stack. It can be used by customers to identify their own stacks.                                                                                                                                                                                                                                                                                                                             |
   |                            |                 |                                                                                           |                                                                                                                                                                                                                                                                                                                                                                                                               |
   |                            |                 |                                                                                           | Minimum: **0**                                                                                                                                                                                                                                                                                                                                                                                                |
   |                            |                 |                                                                                           |                                                                                                                                                                                                                                                                                                                                                                                                               |
   |                            |                 |                                                                                           | Maximum: **1024**                                                                                                                                                                                                                                                                                                                                                                                             |
   +----------------------------+-----------------+-------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | stack_id                   | No              | String                                                                                    | Unique stack ID.                                                                                                                                                                                                                                                                                                                                                                                              |
   |                            |                 |                                                                                           |                                                                                                                                                                                                                                                                                                                                                                                                               |
   |                            |                 |                                                                                           | It is a UUID generated by RFS when a stack is created.                                                                                                                                                                                                                                                                                                                                                        |
   |                            |                 |                                                                                           |                                                                                                                                                                                                                                                                                                                                                                                                               |
   |                            |                 |                                                                                           | Stack name is unique, if you create stack with name ‘HelloWorld’, the same name cannot be used for another stack until original stack is deleted.                                                                                                                                                                                                                                                             |
   |                            |                 |                                                                                           |                                                                                                                                                                                                                                                                                                                                                                                                               |
   |                            |                 |                                                                                           | For parallel development, team members may want to ensure that they are operating the stack they created, not one with the same name created by other members after deleting the previous one.                                                                                                                                                                                                                |
   |                            |                 |                                                                                           |                                                                                                                                                                                                                                                                                                                                                                                                               |
   |                            |                 |                                                                                           | To avoid this mismatch, check the ID, since RFS ensures each stack has a unique ID that does not change with updates. If the stack_id value differs from the current stack ID, 400 is returned.                                                                                                                                                                                                               |
   |                            |                 |                                                                                           |                                                                                                                                                                                                                                                                                                                                                                                                               |
   |                            |                 |                                                                                           | Minimum: **36**                                                                                                                                                                                                                                                                                                                                                                                               |
   |                            |                 |                                                                                           |                                                                                                                                                                                                                                                                                                                                                                                                               |
   |                            |                 |                                                                                           | Maximum: **36**                                                                                                                                                                                                                                                                                                                                                                                               |
   +----------------------------+-----------------+-------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | enable_deletion_protection | No              | Boolean                                                                                   | Deletion protection flag. If this variable is not assigned, the default value is false, indicating that deletion protection is disabled by default. (After deletion protection is enabled, stacks cannot be deleted.)                                                                                                                                                                                         |
   |                            |                 |                                                                                           |                                                                                                                                                                                                                                                                                                                                                                                                               |
   |                            |                 |                                                                                           | *In the* :ref:`UpdateStack <updatestack>` *API, if this variable is not assigned in the RequestBody, the deletion protection attribute of the stack will not be updated.*                                                                                                                                                                                                                                     |
   +----------------------------+-----------------+-------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | enable_auto_rollback       | No              | Boolean                                                                                   | Auto-rollback flag. If this variable is not assigned, the default value is false, indicating that auto-rollback is disabled by default. (After auto-rollback is enabled, if the deployment fails, the stack is automatically rolled back and returns to the previous stable status.)                                                                                                                          |
   |                            |                 |                                                                                           |                                                                                                                                                                                                                                                                                                                                                                                                               |
   |                            |                 |                                                                                           | *In the* :ref:`UpdateStack <updatestack>` *API, if this variable is not assigned in the RequestBody, the auto-rollback attribute of the stack will not be updated.* *This property is mutually exclusive with the import resources using templates feature, which does not allow the deployment of templates containing imported resources if the stack's auto-rollback is set to true.*                      |
   +----------------------------+-----------------+-------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | agencies                   | No              | Array of :ref:`Agency <updatestack__en-us_topic_0000001757038289_request_agency>` objects | Agency information.                                                                                                                                                                                                                                                                                                                                                                                           |
   |                            |                 |                                                                                           |                                                                                                                                                                                                                                                                                                                                                                                                               |
   |                            |                 |                                                                                           | RFS uses an agency only in requests that involve resource operations, such as creating a stack (triggering deployment), creating an execution plan, deploying a stack, and deleting a stack. In addition, the agency applies only to resource operations performed by the provider bound to the agency. If the permissions provided by the agency are insufficient, operations on related resources may fail. |
   |                            |                 |                                                                                           |                                                                                                                                                                                                                                                                                                                                                                                                               |
   |                            |                 |                                                                                           | Array Length: **0 - 10**                                                                                                                                                                                                                                                                                                                                                                                      |
   +----------------------------+-----------------+-------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _updatestack__en-us_topic_0000001757038289_request_agency:

.. table:: **Table 4** Agency

   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                                                                                                                                                                                                                 |
   +=================+=================+=================+=============================================================================================================================================================================================================================================================================================+
   | provider_name   | Yes             | String          | Name of the provider used by a user. If duplicate values are found in the user-provided provider_name entries, a 400 error will be returned.                                                                                                                                                |
   |                 |                 |                 |                                                                                                                                                                                                                                                                                             |
   |                 |                 |                 | Minimum: **1**                                                                                                                                                                                                                                                                              |
   |                 |                 |                 |                                                                                                                                                                                                                                                                                             |
   |                 |                 |                 | Maximum: **128**                                                                                                                                                                                                                                                                            |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | agency_name     | No              | String          | IAM agency used by the corresponding provider. RFS uses this agency to access and create resources of the provider. Either agency_name or agency_urn must be specified.                                                                                                                     |
   |                 |                 |                 |                                                                                                                                                                                                                                                                                             |
   |                 |                 |                 | Minimum: **1**                                                                                                                                                                                                                                                                              |
   |                 |                 |                 |                                                                                                                                                                                                                                                                                             |
   |                 |                 |                 | Maximum: **64**                                                                                                                                                                                                                                                                             |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | agency_urn      | No              | String          | Agency URN When a user defines an agency, either agency_name or agency_urn must be specified. You are advised to set agency_urn when using the trust agency. agency_name can only receive common agency names. If agency_name is set to a trust agency name, template deployment will fail. |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Response Parameters
-------------------

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

-  Update the description of a stack.

   .. code-block::

      PATCH https://{endpoint}/v1/ba2b9930c977f71edaeaa3a5e96a8ff1/stacks/my_hello_world_stack

      {
        "stack_id" : "1b15e005-bdbb-4bd7-8f9a-a09b6774b4b3",
        "description" : "my hello world stack"
      }

-  Disable deletion protection and auto-rollback of a stack.

   .. code-block::

      PATCH https://{endpoint}/v1/ba2b9930c977f71edaeaa3a5e96a8ff1/stacks/my_hello_world_stack

      {
        "stack_id" : "1b15e005-bdbb-4bd7-8f9a-a09b6774b4b3",
        "enable_deletion_protection" : false,
        "enable_auto_rollback" : false
      }

-  Update agency information of a stack.

   .. code-block::

      PATCH https://{endpoint}/v1/ba2b9930c977f71edaeaa3a5e96a8ff1/stacks/my_hello_world_stack

      {
        "stack_id" : "1b15e005-bdbb-4bd7-8f9a-a09b6774b4b3",
        "agencies" : [{
          "provider_name" : "opentelekomcloud",
          "agency_name" : "my_agency"
        }]
      }

Example Responses
-----------------

None

Status Codes
------------

+-----------------------------------+----------------------------------------------------------------------------+
| Status Code                       | Description                                                                |
+===================================+============================================================================+
| 204                               | Updated.                                                                   |
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
