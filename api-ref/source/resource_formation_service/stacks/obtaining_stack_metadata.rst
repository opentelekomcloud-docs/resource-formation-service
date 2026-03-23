:original_name: GetStackMetadata.html

.. _GetStackMetadata:

Obtaining Stack Metadata
========================

Function
--------

This API obtains the metadata of a stack, including the stack ID, stack name, stack description, creation time, update time, stack status, and agency. You can obtain details by referring to :ref:`GetStackMetadataResponseBody <getstackmetadata__section3804181315219>`.

If a stack is in a non-final state (The state ends with IN_PROGRESS. Details are shown in the following description.), its metadata is in a transition phase, which may be a state before or after deployment. The metadata of the stack is in a state after deployment only when the stack is in a final state (ending with *COMPLETE* or *FAILED*).

The non-final states may include:

-  DEPLOYMENT_IN_PROGRESS
-  ROLLBACK_IN_PROGRESS
-  DELETION_IN_PROGRESS

The final states may include:

-  CREATION_COMPLETE
-  DEPLOYMENT_FAILED
-  DEPLOYMENT_COMPLETE
-  ROLLBACK_FAILED
-  ROLLBACK_COMPLETE
-  DELETION_FAILED

URI
---

GET /v1/{project_id}/stacks/{stack_name}/metadata

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

.. _getstackmetadata__section3804181315219:

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 4** Response body parameters

   +----------------------------+---------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter                  | Type                                                                                                          | Description                                                                                                                                                                                                                                                                                                                                                                                                   |
   +============================+===============================================================================================================+===============================================================================================================================================================================================================================================================================================================================================================================================================+
   | stack_id                   | String                                                                                                        | Unique stack ID.                                                                                                                                                                                                                                                                                                                                                                                              |
   +----------------------------+---------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | stack_name                 | String                                                                                                        | A stack name is unique within its domain (domain_id), region, and project (project_id).                                                                                                                                                                                                                                                                                                                       |
   +----------------------------+---------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | description                | String                                                                                                        | Description of a stack. It can be used by customers to identify their own stacks.                                                                                                                                                                                                                                                                                                                             |
   +----------------------------+---------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | vars_structure             | Array of :ref:`VarsStructure <getstackmetadata__en-us_topic_0000001709159306_response_varsstructure>` objects | HCL variable structure. Transferring variables is supported by the HCL template. The same template can use different variables for different purposes.                                                                                                                                                                                                                                                        |
   |                            |                                                                                                               |                                                                                                                                                                                                                                                                                                                                                                                                               |
   |                            |                                                                                                               | -  var_structure allows string variables.                                                                                                                                                                                                                                                                                                                                                                     |
   |                            |                                                                                                               | -  RFS supports vars_structure, vars_body, and vars_uri. If they declare the same variable, error code 400 will be reported.                                                                                                                                                                                                                                                                                  |
   |                            |                                                                                                               | -  vars_structure only supports string variables. To use variables of other types, you need to convert them in HCL reference. Alternatively, you can use vars_uri and vars_body, which support various types and complex structures supported by HCL.                                                                                                                                                         |
   |                            |                                                                                                               | -  If vars_structure is too large, you can use vars_uri.                                                                                                                                                                                                                                                                                                                                                      |
   |                            |                                                                                                               | -  Note: vars_structure cannot contain any sensitive information. RFS directly uses, logs, displays, and stores the corresponding vars in plaintext. If the information is sensitive, you are advised to set the encryption field.                                                                                                                                                                            |
   |                            |                                                                                                               |                                                                                                                                                                                                                                                                                                                                                                                                               |
   |                            |                                                                                                               | Array Length: **0 - 100**                                                                                                                                                                                                                                                                                                                                                                                     |
   +----------------------------+---------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | vars_body                  | String                                                                                                        | Content of the HCL variable file. Transferring variables is supported by the HCL template. The same template can use different variables for different purposes.                                                                                                                                                                                                                                              |
   |                            |                                                                                                               |                                                                                                                                                                                                                                                                                                                                                                                                               |
   |                            |                                                                                                               | -  The vars_body uses the tfvars format of HCL. You can submit the content in the .tfvars file to the vars_body.                                                                                                                                                                                                                                                                                              |
   |                            |                                                                                                               | -  RFS supports vars_structure, vars_body, and vars_uri. If they declare the same variable, error code 400 will be reported.                                                                                                                                                                                                                                                                                  |
   |                            |                                                                                                               | -  If vars_body is too large, you can use vars_uri.                                                                                                                                                                                                                                                                                                                                                           |
   |                            |                                                                                                               | -  If the content in vars is simple strings, you can use var_structure.                                                                                                                                                                                                                                                                                                                                       |
   |                            |                                                                                                               | -  vars_body cannot contain any sensitive information. RFS directly uses, logs, displays, and stores the corresponding vars in plaintext. If the information is sensitive, you are advised to use vars_structure and set the encryption field for transmission.                                                                                                                                               |
   +----------------------------+---------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | enable_deletion_protection | Boolean                                                                                                       | Deletion protection flag. If this variable is not assigned, the default value is false, indicating that deletion protection is disabled by default. (After deletion protection is enabled, stacks cannot be deleted.)                                                                                                                                                                                         |
   |                            |                                                                                                               |                                                                                                                                                                                                                                                                                                                                                                                                               |
   |                            |                                                                                                               | *In the* :ref:`UpdateStack <updatestack>` *API, if this variable is not assigned in the RequestBody, the deletion protection attribute of the stack will not be updated.*                                                                                                                                                                                                                                     |
   +----------------------------+---------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | enable_auto_rollback       | Boolean                                                                                                       | Auto-rollback flag. If this variable is not assigned, the default value is false, indicating that auto-rollback is disabled by default. (After auto-rollback is enabled, if the deployment fails, the stack is automatically rolled back and returns to the previous stable status.)                                                                                                                          |
   |                            |                                                                                                               |                                                                                                                                                                                                                                                                                                                                                                                                               |
   |                            |                                                                                                               | *In the* :ref:`UpdateStack <updatestack>` *API, if this variable is not assigned in the RequestBody, the auto-rollback attribute of the stack will not be updated.* *This property is mutually exclusive with the import resources using templates feature, which does not allow the deployment of templates containing imported resources if the stack's auto-rollback is set to true.*                      |
   +----------------------------+---------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | status                     | String                                                                                                        | Status of a stack.                                                                                                                                                                                                                                                                                                                                                                                            |
   |                            |                                                                                                               |                                                                                                                                                                                                                                                                                                                                                                                                               |
   |                            |                                                                                                               | -  CREATION_COMPLETE indicates an empty stack has been created and no deployment is performed.                                                                                                                                                                                                                                                                                                                |
   |                            |                                                                                                               | -  DEPLOYMENT_IN_PROGRESS indicates the stack deployment is in progress.                                                                                                                                                                                                                                                                                                                                      |
   |                            |                                                                                                               | -  DEPLOYMENT_FAILED indicates the deployment fails. You can obtain the error information summary from status_message. To obtain event details, you can call ListStackEvents.                                                                                                                                                                                                                                 |
   |                            |                                                                                                               | -  DEPLOYMENT_COMPLETE indicates the deployment completed.                                                                                                                                                                                                                                                                                                                                                    |
   |                            |                                                                                                               | -  ROLLBACK_IN_PROGRESS indicates the deployment failed and the rollback is in progress.                                                                                                                                                                                                                                                                                                                      |
   |                            |                                                                                                               | -  ROLLBACK_FAILED indicates the rollback failed. You can obtain the error information summary from status_message. To obtain event details, you can call ListStackEvents.                                                                                                                                                                                                                                    |
   |                            |                                                                                                               | -  ROLLBACK_COMPLETE indicates the rollback completed.                                                                                                                                                                                                                                                                                                                                                        |
   |                            |                                                                                                               | -  DELETION_IN_PROGRESS indicates the deletion is in progress.                                                                                                                                                                                                                                                                                                                                                |
   |                            |                                                                                                               | -  DELETION_FAILED indicates the deletion failed. You can obtain the error information summary from status_message. To obtain event details, you can call ListStackEvents.                                                                                                                                                                                                                                    |
   |                            |                                                                                                               |                                                                                                                                                                                                                                                                                                                                                                                                               |
   |                            |                                                                                                               | Enumeration values:                                                                                                                                                                                                                                                                                                                                                                                           |
   |                            |                                                                                                               |                                                                                                                                                                                                                                                                                                                                                                                                               |
   |                            |                                                                                                               | -  **CREATION_COMPLETE**                                                                                                                                                                                                                                                                                                                                                                                      |
   |                            |                                                                                                               | -  **DEPLOYMENT_IN_PROGRESS**                                                                                                                                                                                                                                                                                                                                                                                 |
   |                            |                                                                                                               | -  **DEPLOYMENT_FAILED**                                                                                                                                                                                                                                                                                                                                                                                      |
   |                            |                                                                                                               | -  **DEPLOYMENT_COMPLETE**                                                                                                                                                                                                                                                                                                                                                                                    |
   |                            |                                                                                                               | -  **ROLLBACK_IN_PROGRESS**                                                                                                                                                                                                                                                                                                                                                                                   |
   |                            |                                                                                                               | -  **ROLLBACK_FAILED**                                                                                                                                                                                                                                                                                                                                                                                        |
   |                            |                                                                                                               | -  **ROLLBACK_COMPLETE**                                                                                                                                                                                                                                                                                                                                                                                      |
   |                            |                                                                                                               | -  **DELETION_IN_PROGRESS**                                                                                                                                                                                                                                                                                                                                                                                   |
   |                            |                                                                                                               | -  **DELETION_FAILED**                                                                                                                                                                                                                                                                                                                                                                                        |
   +----------------------------+---------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | agencies                   | Array of :ref:`Agency <getstackmetadata__en-us_topic_0000001709159306_response_agency>` objects               | Agency information.                                                                                                                                                                                                                                                                                                                                                                                           |
   |                            |                                                                                                               |                                                                                                                                                                                                                                                                                                                                                                                                               |
   |                            |                                                                                                               | RFS uses an agency only in requests that involve resource operations, such as creating a stack (triggering deployment), creating an execution plan, deploying a stack, and deleting a stack. In addition, the agency applies only to resource operations performed by the provider bound to the agency. If the permissions provided by the agency are insufficient, operations on related resources may fail. |
   |                            |                                                                                                               |                                                                                                                                                                                                                                                                                                                                                                                                               |
   |                            |                                                                                                               | Array Length: **0 - 10**                                                                                                                                                                                                                                                                                                                                                                                      |
   +----------------------------+---------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | status_message             | String                                                                                                        | If a stack is in a failure state (ending with FAILED), a brief error information summary is displayed for debugging.                                                                                                                                                                                                                                                                                          |
   +----------------------------+---------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | vars_uri_content           | String                                                                                                        | File content corresponding to vars_uri.                                                                                                                                                                                                                                                                                                                                                                       |
   +----------------------------+---------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | create_time                | String                                                                                                        | Creation time of a stack. The format complies with RFC 3339 (YYYY-MM-DDTHH:MM:SSZ), for example, 1970-01-01T00:00:00Z.                                                                                                                                                                                                                                                                                        |
   +----------------------------+---------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | update_time                | String                                                                                                        | Update time of a stack (applied to the metadata update and deployment). The format complies with RFC 3339 (YYYY-MM-DDTHH:MM:SSZ), for example, 1970-01-01T00:00:00Z.                                                                                                                                                                                                                                          |
   +----------------------------+---------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _getstackmetadata__en-us_topic_0000001709159306_response_varsstructure:

.. table:: **Table 5** VarsStructure

   +-----------------------+-----------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                                                                                                            | Description                                                                                                                                                                                        |
   +=======================+=================================================================================================================+====================================================================================================================================================================================================+
   | var_key               | String                                                                                                          | Variable name.                                                                                                                                                                                     |
   +-----------------------+-----------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | var_value             | String                                                                                                          | Variable value.                                                                                                                                                                                    |
   |                       |                                                                                                                 |                                                                                                                                                                                                    |
   |                       |                                                                                                                 | Variables must be in the form of a string. If a parameter is a number, it must also be in the form of a string, for example, '10'.                                                                 |
   |                       |                                                                                                                 |                                                                                                                                                                                                    |
   |                       |                                                                                                                 | For different types or complex structures, you can use vars_uri or vars_body.                                                                                                                      |
   +-----------------------+-----------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | encryption            | :ref:`EncryptionStructure <getstackmetadata__en-us_topic_0000001709159306_response_encryptionstructure>` object | If a transferred var_value has been encrypted, you can declare this variable to require RFS to decrypt the var_value before using it. Currently, only KMS encryption and decryption are supported. |
   +-----------------------+-----------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _getstackmetadata__en-us_topic_0000001709159306_response_encryptionstructure:

.. table:: **Table 6** EncryptionStructure

   +-----------------------+---------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                                                                                              | Description                                                                                                                                                                                                                                                                                                                                       |
   +=======================+===================================================================================================+===================================================================================================================================================================================================================================================================================================================================================+
   | kms                   | :ref:`KmsStructure <getstackmetadata__en-us_topic_0000001709159306_response_kmsstructure>` object | If an assigned var_value is encrypted by KMS, related encryption information can be transferred. RFS will help you decrypt the var_value by KMS.                                                                                                                                                                                                  |
   |                       |                                                                                                   |                                                                                                                                                                                                                                                                                                                                                   |
   |                       |                                                                                                   | **Note:**                                                                                                                                                                                                                                                                                                                                         |
   |                       |                                                                                                   |                                                                                                                                                                                                                                                                                                                                                   |
   |                       |                                                                                                   | -  The agency you specify for RFS should have the operation permissions on the specified key ID.                                                                                                                                                                                                                                                  |
   |                       |                                                                                                   | -  KMS provides a quota for free trial every month. If the quota is exceeded, you will be billed for KMS. The fee is not billed by RFS.                                                                                                                                                                                                           |
   |                       |                                                                                                   | -  KMS encryption only indicates that RFS uses ciphertext for storage and transmission. However, RFS still uses plaintext in stack-events. If you want RFS to use ciphertext in logs, you can declare sensitive in templates. For more information about sensitive, refer to https://learn.hashicorp.com/tutorials/terraform/sensitive-variables. |
   +-----------------------+---------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _getstackmetadata__en-us_topic_0000001709159306_response_kmsstructure:

.. table:: **Table 7** KmsStructure

   +-------------+--------+-------------------------------------------------------------------------------------------------+
   | Parameter   | Type   | Description                                                                                     |
   +=============+========+=================================================================================================+
   | id          | String | KMS key ID is used by RFS during decryption. Generally, the key ID is that used for encryption. |
   +-------------+--------+-------------------------------------------------------------------------------------------------+
   | cipher_text | String | Ciphertext of data encryption key.                                                              |
   +-------------+--------+-------------------------------------------------------------------------------------------------+

.. _getstackmetadata__en-us_topic_0000001709159306_response_agency:

.. table:: **Table 8** Agency

   +---------------+--------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter     | Type   | Description                                                                                                                                                             |
   +===============+========+=========================================================================================================================================================================+
   | provider_name | String | Name of the provider used by a user. If duplicate values are found in the user-provided provider_name entries, a 400 error will be returned.                            |
   +---------------+--------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | agency_name   | String | IAM agency used by the corresponding provider. RFS uses this agency to access and create resources of the provider. Either agency_name or agency_urn must be specified. |
   +---------------+--------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | agency_urn    | String | The URN of Agency used by the corresponding provider.                                                                                                                   |
   +---------------+--------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

**Status code: 400**

.. table:: **Table 9** Response body parameters

   ========== ====== =================
   Parameter  Type   Description
   ========== ====== =================
   error_code String Response code.
   error_msg  String Response message.
   ========== ====== =================

**Status code: 401**

.. table:: **Table 10** Response body parameters

   ========== ====== =================
   Parameter  Type   Description
   ========== ====== =================
   error_code String Response code.
   error_msg  String Response message.
   ========== ====== =================

**Status code: 403**

.. table:: **Table 11** Response body parameters

   ========== ====== =================
   Parameter  Type   Description
   ========== ====== =================
   error_code String Response code.
   error_msg  String Response message.
   ========== ====== =================

**Status code: 404**

.. table:: **Table 12** Response body parameters

   ========== ====== =================
   Parameter  Type   Description
   ========== ====== =================
   error_code String Response code.
   error_msg  String Response message.
   ========== ====== =================

**Status code: 429**

.. table:: **Table 13** Response body parameters

   ========== ====== =================
   Parameter  Type   Description
   ========== ====== =================
   error_code String Response code.
   error_msg  String Response message.
   ========== ====== =================

**Status code: 500**

.. table:: **Table 14** Response body parameters

   ========== ====== =================
   Parameter  Type   Description
   ========== ====== =================
   error_code String Response code.
   error_msg  String Response message.
   ========== ====== =================

Example Requests
----------------

-  Obtain stack metadata.

   .. code-block:: text

      GET https://{endpoint}/v1/ba2b9930c977f71edaeaa3a5e96a8ff1/stacks/my_hello_world_stack/metadata

-  Obtain stack metadata, with a stack ID provided to check whether the stack ID matches the current stack.

   .. code-block:: text

      GET https://{endpoint}/v1/ba2b9930c977f71edaeaa3a5e96a8ff1/stacks/my_hello_world_stack/metadata?stack_id=ea6a4f0e-ee8a-494e-b12a-8be4a1e65af2

Example Responses
-----------------

**Status code: 200**

Stack metadata obtained.

.. code-block::

   {
     "stack_id" : "f689e9fd-97e7-4185-bd8a-7d5f708d45d7",
     "stack_name" : "my_hello_world_stack",
     "description" : "my hello world stack",
     "enable_deletion_protection" : false,
     "enable_auto_rollback" : false,
     "status" : "DEPLOYMENT_COMPLETE",
     "agencies" : [ {
       "agency_name" : "rf_admin_trust",
       "provider_name" : "opentelekomcloud"
     } ],
     "create_time" : "2023-03-16T03:28:20Z",
     "update_time" : "2023-05-24T08:56:10Z"
   }

Status Codes
------------

=========== =======================================================
Status Code Description
=========== =======================================================
200         Stack metadata obtained.
400         Invalid request.
401         Authentication failed.
403         The user does not have the permission to call this API.
404         The stack does not exist.
429         Too frequent requests.
500         Internal server error.
=========== =======================================================
