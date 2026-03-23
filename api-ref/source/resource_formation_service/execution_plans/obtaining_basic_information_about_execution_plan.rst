:original_name: GetExecutionPlanMetadata.html

.. _GetExecutionPlanMetadata:

Obtaining basic information about Execution Plan
================================================

Function
--------

This API obtains the metadata of a specified execution plan, including the ID and name of the stack and the ID, name, description, creation time, execution time, and status of the execution plan.

You can obtain details by referring to :ref:`GetExecutionPlanMetadataResponseBody <getexecutionplanmetadata__section1283315152428>`.

To obtain the details of an execution plan, call :ref:`GetExecutionPlan <getexecutionplan>`.

URI
---

GET /v1/{project_id}/stacks/{stack_name}/execution-plans/{execution_plan_name}/metadata

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

.. _getexecutionplanmetadata__section1283315152428:

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 4** Response body parameters

   +-----------------------+---------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                                                                                                                      | Description                                                                                                                                                                                                                                                     |
   +=======================+===========================================================================================================================+=================================================================================================================================================================================================================================================================+
   | stack_id              | String                                                                                                                    | Unique stack ID.                                                                                                                                                                                                                                                |
   +-----------------------+---------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | stack_name            | String                                                                                                                    | A stack name is unique within its domain (domain_id), region, and project (project_id).                                                                                                                                                                         |
   +-----------------------+---------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | execution_plan_id     | String                                                                                                                    | Unique execution plan ID.                                                                                                                                                                                                                                       |
   +-----------------------+---------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | execution_plan_name   | String                                                                                                                    | An execution plan name is unique within its domain (domain_id), region, project (project_id), and stack (stack_id).                                                                                                                                             |
   +-----------------------+---------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | description           | String                                                                                                                    | Execution plan description. It is used to identify your own execution plans.                                                                                                                                                                                    |
   +-----------------------+---------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | vars_structure        | Array of :ref:`VarsStructure <getexecutionplanmetadata__en-us_topic_0000001709318818_response_varsstructure>` objects     | HCL variable structure. Transferring variables is supported by the HCL template. The same template can use different variables for different purposes.                                                                                                          |
   |                       |                                                                                                                           |                                                                                                                                                                                                                                                                 |
   |                       |                                                                                                                           | -  var_structure allows string variables.                                                                                                                                                                                                                       |
   |                       |                                                                                                                           | -  RFS supports vars_structure, vars_body, and vars_uri. If they declare the same variable, error code 400 will be reported.                                                                                                                                    |
   |                       |                                                                                                                           | -  vars_structure only supports string variables. To use variables of other types, you need to convert them in HCL reference. Alternatively, you can use vars_uri and vars_body, which support various types and complex structures supported by HCL.           |
   |                       |                                                                                                                           | -  If vars_structure is too large, you can use vars_uri.                                                                                                                                                                                                        |
   |                       |                                                                                                                           | -  Note: vars_structure cannot contain any sensitive information. RFS directly uses, logs, displays, and stores the corresponding vars in plaintext. If the information is sensitive, you are advised to set the encryption field.                              |
   |                       |                                                                                                                           |                                                                                                                                                                                                                                                                 |
   |                       |                                                                                                                           | Array Length: **0 - 100**                                                                                                                                                                                                                                       |
   +-----------------------+---------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | vars_uri_content      | String                                                                                                                    | File content corresponding to vars_uri.                                                                                                                                                                                                                         |
   +-----------------------+---------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | vars_body             | String                                                                                                                    | Content of the HCL variable file. Transferring variables is supported by the HCL template. The same template can use different variables for different purposes.                                                                                                |
   |                       |                                                                                                                           |                                                                                                                                                                                                                                                                 |
   |                       |                                                                                                                           | -  The vars_body uses the tfvars format of HCL. You can submit the content in the .tfvars file to the vars_body.                                                                                                                                                |
   |                       |                                                                                                                           | -  RFS supports vars_structure, vars_body, and vars_uri. If they declare the same variable, error code 400 will be reported.                                                                                                                                    |
   |                       |                                                                                                                           | -  If vars_body is too large, you can use vars_uri.                                                                                                                                                                                                             |
   |                       |                                                                                                                           | -  If the content in vars is simple strings, you can use var_structure.                                                                                                                                                                                         |
   |                       |                                                                                                                           | -  vars_body cannot contain any sensitive information. RFS directly uses, logs, displays, and stores the corresponding vars in plaintext. If the information is sensitive, you are advised to use vars_structure and set the encryption field for transmission. |
   +-----------------------+---------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | status                | String                                                                                                                    | Status of an execution plan.                                                                                                                                                                                                                                    |
   |                       |                                                                                                                           |                                                                                                                                                                                                                                                                 |
   |                       |                                                                                                                           | -  **CREATION_IN_PROGRESS** indicates that creation is in progress.                                                                                                                                                                                             |
   |                       |                                                                                                                           | -  **CREATION_FAILED** indicates the creation failed. You can obtain the error information summary from status_message.                                                                                                                                         |
   |                       |                                                                                                                           | -  **AVAILABLE** indicates the creation completed. You can call ApplyExecutionPlan to apply the plan.                                                                                                                                                           |
   |                       |                                                                                                                           | -  **APPLY_IN_PROGRESS** indicates the execution is in progress. You can call GetStackMetadata to query the stack status, or call ListStackEvents to obtain the stack events generated during the execution.                                                    |
   |                       |                                                                                                                           | -  **APPLIED** indicates the plan has been applied.                                                                                                                                                                                                             |
   |                       |                                                                                                                           |                                                                                                                                                                                                                                                                 |
   |                       |                                                                                                                           | Enumeration values:                                                                                                                                                                                                                                             |
   |                       |                                                                                                                           |                                                                                                                                                                                                                                                                 |
   |                       |                                                                                                                           | -  **CREATION_IN_PROGRESS**                                                                                                                                                                                                                                     |
   |                       |                                                                                                                           | -  **CREATION_FAILED**                                                                                                                                                                                                                                          |
   |                       |                                                                                                                           | -  **AVAILABLE**                                                                                                                                                                                                                                                |
   |                       |                                                                                                                           | -  **APPLY_IN_PROGRESS**                                                                                                                                                                                                                                        |
   |                       |                                                                                                                           | -  **APPLIED**                                                                                                                                                                                                                                                  |
   +-----------------------+---------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | status_message        | String                                                                                                                    | If an execution plan is in a CREATION_FAILED status, a brief error information summary is displayed for debugging.                                                                                                                                              |
   +-----------------------+---------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | create_time           | String                                                                                                                    | Creation time of an execution plan. The format complies with RFC 3339 (YYYY-MM-DDTHH:MM:SSZ), for example, 1970-01-01T00:00:00Z.                                                                                                                                |
   +-----------------------+---------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | apply_time            | String                                                                                                                    | Time of applying an execution plan. The format complies with RFC 3339 (YYYY-MM-DDTHH:MM:SSZ), for example, 1970-01-01T00:00:00Z.                                                                                                                                |
   +-----------------------+---------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | summary               | :ref:`ExecutionPlanSummary <getexecutionplanmetadata__en-us_topic_0000001709318818_response_executionplansummary>` object | Summary of the execution plan result may include:                                                                                                                                                                                                               |
   |                       |                                                                                                                           |                                                                                                                                                                                                                                                                 |
   |                       |                                                                                                                           | -  Number of resources to be added.                                                                                                                                                                                                                             |
   |                       |                                                                                                                           |                                                                                                                                                                                                                                                                 |
   |                       |                                                                                                                           | -  Number of resources to be updated.                                                                                                                                                                                                                           |
   |                       |                                                                                                                           |                                                                                                                                                                                                                                                                 |
   |                       |                                                                                                                           | -  Number of resources to be deleted.                                                                                                                                                                                                                           |
   |                       |                                                                                                                           |                                                                                                                                                                                                                                                                 |
   |                       |                                                                                                                           |    Note:                                                                                                                                                                                                                                                        |
   |                       |                                                                                                                           |                                                                                                                                                                                                                                                                 |
   |                       |                                                                                                                           | -  The summary is returned only when the execution plan is in the following states: *AVAILABLE*, *APPLY_IN_PROGRESS* or *APPLIED*.                                                                                                                              |
   |                       |                                                                                                                           |                                                                                                                                                                                                                                                                 |
   |                       |                                                                                                                           | -  The summary also includes resource changes brought by a drift. The resource status drift is caused by inconsistency between the resource status recorded in the stack and the remote resource status.                                                        |
   +-----------------------+---------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _getexecutionplanmetadata__en-us_topic_0000001709318818_response_varsstructure:

.. table:: **Table 5** VarsStructure

   +-----------------------+-------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                                                                                                                    | Description                                                                                                                                                                                        |
   +=======================+=========================================================================================================================+====================================================================================================================================================================================================+
   | var_key               | String                                                                                                                  | Variable name.                                                                                                                                                                                     |
   +-----------------------+-------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | var_value             | String                                                                                                                  | Variable value.                                                                                                                                                                                    |
   |                       |                                                                                                                         |                                                                                                                                                                                                    |
   |                       |                                                                                                                         | Variables must be in the form of a string. If a parameter is a number, it must also be in the form of a string, for example, '10'.                                                                 |
   |                       |                                                                                                                         |                                                                                                                                                                                                    |
   |                       |                                                                                                                         | For different types or complex structures, you can use vars_uri or vars_body.                                                                                                                      |
   +-----------------------+-------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | encryption            | :ref:`EncryptionStructure <getexecutionplanmetadata__en-us_topic_0000001709318818_response_encryptionstructure>` object | If a transferred var_value has been encrypted, you can declare this variable to require RFS to decrypt the var_value before using it. Currently, only KMS encryption and decryption are supported. |
   +-----------------------+-------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _getexecutionplanmetadata__en-us_topic_0000001709318818_response_encryptionstructure:

.. table:: **Table 6** EncryptionStructure

   +-----------------------+-----------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                                                                                                      | Description                                                                                                                                                                                                                                                                                                                                       |
   +=======================+===========================================================================================================+===================================================================================================================================================================================================================================================================================================================================================+
   | kms                   | :ref:`KmsStructure <getexecutionplanmetadata__en-us_topic_0000001709318818_response_kmsstructure>` object | If an assigned var_value is encrypted by KMS, related encryption information can be transferred. RFS will help you decrypt the var_value by KMS.                                                                                                                                                                                                  |
   |                       |                                                                                                           |                                                                                                                                                                                                                                                                                                                                                   |
   |                       |                                                                                                           | **Note:**                                                                                                                                                                                                                                                                                                                                         |
   |                       |                                                                                                           |                                                                                                                                                                                                                                                                                                                                                   |
   |                       |                                                                                                           | -  The agency you specify for RFS should have the operation permissions on the specified key ID.                                                                                                                                                                                                                                                  |
   |                       |                                                                                                           | -  KMS provides a quota for free trial every month. If the quota is exceeded, you will be billed for KMS. The fee is not billed by RFS.                                                                                                                                                                                                           |
   |                       |                                                                                                           | -  KMS encryption only indicates that RFS uses ciphertext for storage and transmission. However, RFS still uses plaintext in stack-events. If you want RFS to use ciphertext in logs, you can declare sensitive in templates. For more information about sensitive, refer to https://learn.hashicorp.com/tutorials/terraform/sensitive-variables. |
   +-----------------------+-----------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _getexecutionplanmetadata__en-us_topic_0000001709318818_response_kmsstructure:

.. table:: **Table 7** KmsStructure

   +-------------+--------+-------------------------------------------------------------------------------------------------+
   | Parameter   | Type   | Description                                                                                     |
   +=============+========+=================================================================================================+
   | id          | String | KMS key ID is used by RFS during decryption. Generally, the key ID is that used for encryption. |
   +-------------+--------+-------------------------------------------------------------------------------------------------+
   | cipher_text | String | Ciphertext of data encryption key.                                                              |
   +-------------+--------+-------------------------------------------------------------------------------------------------+

.. _getexecutionplanmetadata__en-us_topic_0000001709318818_response_executionplansummary:

.. table:: **Table 8** ExecutionPlanSummary

   =============== ======= =============================
   Parameter       Type    Description
   =============== ======= =============================
   resource_add    Integer Number of new resources.
   resource_update Integer Number of updated resources.
   resource_delete Integer Number of deleted resources.
   resource_import Integer Number of imported resources.
   =============== ======= =============================

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

-  Obtain the metadata of a specified execution plan.

   .. code-block:: text

      GET https://{endpoint}/v1/ba2b9930c977f71edaeaa3a5e96a8ff1/stacks/my_hello_world_stack/execution-plans/my_first_execution_plan/metadata

-  Obtain the metadata of a specified execution plan, with a stack ID and an execution plan ID provided to check whether they match the current stack and execution plan.

   .. code-block:: text

      GET https://{endpoint}/v1/ba2b9930c977f71edaeaa3a5e96a8ff1/stacks/my_hello_world_stack/execution-plans/my_first_execution_plan/metadata?stack_id=ea6a4f0e-ee8a-494e-b12a-8be4a1e65af2&execution_plan_id=fb5e781e-a27d-46e2-9954-242753857a9f

Example Responses
-----------------

**Status code: 200**

Execution plan metadata obtained.

.. code-block::

   {
     "stack_id" : "f689e9fd-97e7-4185-bd8a-7d5f708d45d7",
     "stack_name" : "my_hello_world_stack",
     "execution_plan_id" : "ebc0979a-c617-4382-9147-57fc83a634aa",
     "execution_plan_name" : "my_first_execution_plan",
     "status" : "APPLIED",
     "apply_time" : "2023-05-17T11:56:40Z",
     "create_time" : "2023-05-16T03:37:24Z",
     "summary" : {
       "resource_add" : 2
     }
   }

Status Codes
------------

+-----------------------------------+---------------------------------------------------------+
| Status Code                       | Description                                             |
+===================================+=========================================================+
| 200                               | Execution plan metadata obtained.                       |
+-----------------------------------+---------------------------------------------------------+
| 400                               | Invalid request.                                        |
+-----------------------------------+---------------------------------------------------------+
| 401                               | Authentication failed.                                  |
+-----------------------------------+---------------------------------------------------------+
| 403                               | The user does not have the permission to call this API. |
+-----------------------------------+---------------------------------------------------------+
| 404                               | #. The execution plan does not exist.                   |
|                                   | #. The stack does not exist.                            |
+-----------------------------------+---------------------------------------------------------+
| 429                               | Too frequent requests.                                  |
+-----------------------------------+---------------------------------------------------------+
| 500                               | Internal server error.                                  |
+-----------------------------------+---------------------------------------------------------+
