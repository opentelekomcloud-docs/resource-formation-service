:original_name: ListStackOutputs.html

.. _ListStackOutputs:

Listing Stack Outputs
=====================

Function
--------

This API lists all outputs of a stack.

The stack output is the return information generated after the deployment of the output statement block defined in the template is complete. After the deployment is complete, you can call this API to obtain the specific output information.

If the stack is in a non-final state (ending with IN_PROGRESS), this API returns empty value. The non-final states may include:

-  DEPLOYMENT_IN_PROGRESS
-  DELETION_IN_PROGRESS
-  ROLLBACK_IN_PROGRESS

Output is defined in the HCL syntax. The returned information is similar to the return value programmatically. For details, refer to the HCL documentation.

URI
---

GET /v1/{project_id}/stacks/{stack_name}/outputs

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

**Status code: 200**

.. table:: **Table 4** Response body parameters

   +-----------+-----------------------------------------------------------------------------------------------------------+--------------------+
   | Parameter | Type                                                                                                      | Description        |
   +===========+===========================================================================================================+====================+
   | outputs   | Array of :ref:`StackOutput <liststackoutputs__en-us_topic_0000001757038285_response_stackoutput>` objects | Stack output list. |
   +-----------+-----------------------------------------------------------------------------------------------------------+--------------------+

.. _liststackoutputs__en-us_topic_0000001757038285_response_stackoutput:

.. table:: **Table 5** StackOutput

   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                                                           |
   +=======================+=======================+=======================================================================================================================================+
   | name                  | String                | Name of a stack output, defined in a template.                                                                                        |
   |                       |                       |                                                                                                                                       |
   |                       |                       | For example, in the following HCL template, the value of name is vpc_id.                                                              |
   |                       |                       |                                                                                                                                       |
   |                       |                       | .. code-block::                                                                                                                       |
   |                       |                       |                                                                                                                                       |
   |                       |                       |    output "vpc_id" {                                                                                                                  |
   |                       |                       |      value = opentelekomcloud_vpc_v1.my_hello_world_vpc.id                                                                            |
   |                       |                       |    }                                                                                                                                  |
   |                       |                       |                                                                                                                                       |
   |                       |                       | In a JSON template, the value of name is vpc_id.                                                                                      |
   |                       |                       |                                                                                                                                       |
   |                       |                       | .. code-block::                                                                                                                       |
   |                       |                       |                                                                                                                                       |
   |                       |                       |    {                                                                                                                                  |
   |                       |                       |      "output": {                                                                                                                      |
   |                       |                       |        "vpc_id": [                                                                                                                    |
   |                       |                       |          {                                                                                                                            |
   |                       |                       |            "value": "${opentelekomcloud_vpc_v1.my_hello_world_vpc.id}"                                                                |
   |                       |                       |          }                                                                                                                            |
   |                       |                       |        ]                                                                                                                              |
   |                       |                       |      }                                                                                                                                |
   |                       |                       |    }                                                                                                                                  |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------+
   | description           | String                | Description of a stack output, defined in a template.                                                                                 |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------+
   | type                  | String                | Output type of a stack.                                                                                                               |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------+
   | value                 | String                | Output value of a stack.                                                                                                              |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------+
   | sensitive             | Boolean               | Whether a stack output is sensitive. Value can be true (enabled) or false (disabled). This is defined in a template.                  |
   |                       |                       |                                                                                                                                       |
   |                       |                       | If an output is defined as sensitive in a template, the actual value and type of the output will not be returned in the reponse body. |
   |                       |                       |                                                                                                                                       |
   |                       |                       | Instead, it will be returned.                                                                                                         |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------+

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

-  List the stack outputs.

   .. code-block:: text

      GET https://{endpoint}/v1/ba2b9930c977f71edaeaa3a5e96a8ff1/stacks/my_hello_world_stack/outputs

-  List the stack outputs and check whether the stack ID matches the current stack.

   .. code-block:: text

      GET https://{endpoint}/v1/ba2b9930c977f71edaeaa3a5e96a8ff1/stacks/my_hello_world_stack/outputs?stack_id=ea6a4f0e-ee8a-494e-b12a-8be4a1e65af2

Example Responses
-----------------

**Status code: 200**

The stack outputs listed.

.. code-block::

   {
     "outputs" : [ {
       "name" : "my_first_vpc",
       "sensitive" : true,
       "type" : "<sensitive>",
       "value" : "<sensitive>",
       "description" : "type and value is invisible when sensitive is true."
     }, {
       "name" : "my_second_vpc",
       "type" : "string",
       "value" : "\"opentelekomcloud_vpc_v1.my_second_vpc\"",
       "description" : "type and value is real when sensitive not set or is false."
     } ]
   }

Status Codes
------------

=========== =======================================================
Status Code Description
=========== =======================================================
200         The stack outputs listed.
400         Invalid request.
401         Authentication failed.
403         The user does not have the permission to call this API.
404         The stack does not exist.
429         Too frequent requests.
500         Internal server error.
=========== =======================================================
