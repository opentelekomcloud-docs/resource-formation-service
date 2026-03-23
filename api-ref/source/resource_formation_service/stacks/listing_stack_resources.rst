:original_name: ListStackResources.html

.. _ListStackResources:

Listing Stack Resources
=======================

Function
--------

This API lists the information about all resources managed by a stack.

When the stack is in a non-final state, only brief information about the resources in the stack is output, including logical_resource_name, logical_resource_type, physical_resource_id, physical_resource_name, and status. When the stack is in the final status, additional detailed information is output. For example, the resource_attributes.

The non-final states may include:

-  DEPLOYMENT_IN_PROGRESS
-  DELETION_IN_PROGRESS
-  ROLLBACK_IN_PROGRESS

URI
---

GET /v1/{project_id}/stacks/{stack_name}/resources

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

   +-----------------+-----------------------------------------------------------------------------------------------------------------+---------------------------------------+
   | Parameter       | Type                                                                                                            | Description                           |
   +=================+=================================================================================================================+=======================================+
   | stack_resources | Array of :ref:`StackResource <liststackresources__en-us_topic_0000001709159310_response_stackresource>` objects | List of resources managed by a stack. |
   +-----------------+-----------------------------------------------------------------------------------------------------------------+---------------------------------------+

.. _liststackresources__en-us_topic_0000001709159310_response_stackresource:

.. table:: **Table 5** StackResource

   +------------------------+-------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter              | Type                                                                                                                    | Description                                                                                                                                                                                                                                              |
   +========================+=========================================================================================================================+==========================================================================================================================================================================================================================================================+
   | physical_resource_id   | String                                                                                                                  | Physical ID of a resource, generated by the resource provider, cloud service provider, or other service providers during resource deployment.                                                                                                            |
   +------------------------+-------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | physical_resource_name | String                                                                                                                  | Physical name of the resource, defined by the resource provider, cloud service provider, or other service providers during resource deployment.                                                                                                          |
   +------------------------+-------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | logical_resource_name  | String                                                                                                                  | Logical name of the resource, defined in a template.                                                                                                                                                                                                     |
   |                        |                                                                                                                         |                                                                                                                                                                                                                                                          |
   |                        |                                                                                                                         | Logical variables are only used as identifiers of the resource in the template.                                                                                                                                                                          |
   |                        |                                                                                                                         |                                                                                                                                                                                                                                                          |
   |                        |                                                                                                                         | For example, in the following HCL template, the value of logical_resource_name is my_hello_world_vpc.                                                                                                                                                    |
   |                        |                                                                                                                         |                                                                                                                                                                                                                                                          |
   |                        |                                                                                                                         | .. code-block::                                                                                                                                                                                                                                          |
   |                        |                                                                                                                         |                                                                                                                                                                                                                                                          |
   |                        |                                                                                                                         |    resource "opentelekomcloud_vpc_v1" "my_hello_world_vpc" {                                                                                                                                                                                             |
   |                        |                                                                                                                         |      name = "test_vpc"                                                                                                                                                                                                                                   |
   |                        |                                                                                                                         |    }                                                                                                                                                                                                                                                     |
   |                        |                                                                                                                         |                                                                                                                                                                                                                                                          |
   |                        |                                                                                                                         | In a JSON template, the value of logical_resource_name is my_hello_world_vpc.                                                                                                                                                                            |
   |                        |                                                                                                                         |                                                                                                                                                                                                                                                          |
   |                        |                                                                                                                         | .. code-block::                                                                                                                                                                                                                                          |
   |                        |                                                                                                                         |                                                                                                                                                                                                                                                          |
   |                        |                                                                                                                         |    {                                                                                                                                                                                                                                                     |
   |                        |                                                                                                                         |      "resource": {                                                                                                                                                                                                                                       |
   |                        |                                                                                                                         |        "opentelekomcloud_vpc_v1": {                                                                                                                                                                                                                      |
   |                        |                                                                                                                         |          "my_hello_world_vpc": {                                                                                                                                                                                                                         |
   |                        |                                                                                                                         |            "name": "test_vpc"                                                                                                                                                                                                                            |
   |                        |                                                                                                                         |          }                                                                                                                                                                                                                                               |
   |                        |                                                                                                                         |        }                                                                                                                                                                                                                                                 |
   |                        |                                                                                                                         |      }                                                                                                                                                                                                                                                   |
   |                        |                                                                                                                         |    }                                                                                                                                                                                                                                                     |
   +------------------------+-------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | logical_resource_type  | String                                                                                                                  | Resource type.                                                                                                                                                                                                                                           |
   |                        |                                                                                                                         |                                                                                                                                                                                                                                                          |
   |                        |                                                                                                                         | Logical variables are only used as identifiers of the resource in the template.                                                                                                                                                                          |
   |                        |                                                                                                                         |                                                                                                                                                                                                                                                          |
   |                        |                                                                                                                         | For example, in the following HCL template, the value of logical_resource_type is opentelekomcloud_vpc_v1.                                                                                                                                               |
   |                        |                                                                                                                         |                                                                                                                                                                                                                                                          |
   |                        |                                                                                                                         | .. code-block::                                                                                                                                                                                                                                          |
   |                        |                                                                                                                         |                                                                                                                                                                                                                                                          |
   |                        |                                                                                                                         |    resource "opentelekomcloud_vpc_v1" "my_hello_world_vpc" {                                                                                                                                                                                             |
   |                        |                                                                                                                         |      name = "test_vpc"                                                                                                                                                                                                                                   |
   |                        |                                                                                                                         |    }                                                                                                                                                                                                                                                     |
   |                        |                                                                                                                         |                                                                                                                                                                                                                                                          |
   |                        |                                                                                                                         | In a JSON template, the value of logical_resource_type is opentelekomcloud_vpc_v1.                                                                                                                                                                       |
   |                        |                                                                                                                         |                                                                                                                                                                                                                                                          |
   |                        |                                                                                                                         | .. code-block::                                                                                                                                                                                                                                          |
   |                        |                                                                                                                         |                                                                                                                                                                                                                                                          |
   |                        |                                                                                                                         |    {                                                                                                                                                                                                                                                     |
   |                        |                                                                                                                         |      "resource": {                                                                                                                                                                                                                                       |
   |                        |                                                                                                                         |        "opentelekomcloud_vpc_v1": {                                                                                                                                                                                                                      |
   |                        |                                                                                                                         |          "my_hello_world_vpc": {                                                                                                                                                                                                                         |
   |                        |                                                                                                                         |            "name": "test_vpc"                                                                                                                                                                                                                            |
   |                        |                                                                                                                         |          }                                                                                                                                                                                                                                               |
   |                        |                                                                                                                         |        }                                                                                                                                                                                                                                                 |
   |                        |                                                                                                                         |      }                                                                                                                                                                                                                                                   |
   |                        |                                                                                                                         |    }                                                                                                                                                                                                                                                     |
   +------------------------+-------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | index_key              | String                                                                                                                  | Resource index. If **count** or **for_each** is used in a template, index_key is returned. If index_key appears, logical_resource_name + index_key can be used as an identifier of the resource.                                                         |
   |                        |                                                                                                                         |                                                                                                                                                                                                                                                          |
   |                        |                                                                                                                         | If **count** is used in a template, index_key is a number starting from 0.                                                                                                                                                                               |
   |                        |                                                                                                                         |                                                                                                                                                                                                                                                          |
   |                        |                                                                                                                         | For example, in the following HCL template, you can use opentelekomcloud_vpc_v1.my_hello_world_vpc[0] and opentelekomcloud_vpc_v1.my_hello_world_vpc[1] to identify two resources.                                                                       |
   |                        |                                                                                                                         |                                                                                                                                                                                                                                                          |
   |                        |                                                                                                                         | .. code-block::                                                                                                                                                                                                                                          |
   |                        |                                                                                                                         |                                                                                                                                                                                                                                                          |
   |                        |                                                                                                                         |    resource "opentelekomcloud_vpc_v1" "my_hello_world_vpc" {                                                                                                                                                                                             |
   |                        |                                                                                                                         |      count = 2                                                                                                                                                                                                                                           |
   |                        |                                                                                                                         |      name = "test_vpc"                                                                                                                                                                                                                                   |
   |                        |                                                                                                                         |    }                                                                                                                                                                                                                                                     |
   |                        |                                                                                                                         |                                                                                                                                                                                                                                                          |
   |                        |                                                                                                                         | In a JSON template, you can use opentelekomcloud_vpc_v1.my_hello_world_vpc[0] and opentelekomcloud_vpc_v1.my_hello_world_vpc[1] to identify two resources.                                                                                               |
   |                        |                                                                                                                         |                                                                                                                                                                                                                                                          |
   |                        |                                                                                                                         | .. code-block::                                                                                                                                                                                                                                          |
   |                        |                                                                                                                         |                                                                                                                                                                                                                                                          |
   |                        |                                                                                                                         |    {                                                                                                                                                                                                                                                     |
   |                        |                                                                                                                         |      "resource": {                                                                                                                                                                                                                                       |
   |                        |                                                                                                                         |        "opentelekomcloud_vpc_v1": {                                                                                                                                                                                                                      |
   |                        |                                                                                                                         |          "my_hello_world_vpc": {                                                                                                                                                                                                                         |
   |                        |                                                                                                                         |            "name": "test_vpc",                                                                                                                                                                                                                           |
   |                        |                                                                                                                         |            "count": 2                                                                                                                                                                                                                                    |
   |                        |                                                                                                                         |          }                                                                                                                                                                                                                                               |
   |                        |                                                                                                                         |        }                                                                                                                                                                                                                                                 |
   |                        |                                                                                                                         |      }                                                                                                                                                                                                                                                   |
   |                        |                                                                                                                         |    }                                                                                                                                                                                                                                                     |
   |                        |                                                                                                                         |                                                                                                                                                                                                                                                          |
   |                        |                                                                                                                         | If **for_each** is used in a template, index_key is a user-defined string. For example, in the following HCL template, opentelekomcloud_vpc_v1.my_hello_world_vpc["vpc1"] and opentelekomcloud_vpc_v1.my_hello_world_vpc["vpc2"] identify two resources. |
   |                        |                                                                                                                         |                                                                                                                                                                                                                                                          |
   |                        |                                                                                                                         | .. code-block::                                                                                                                                                                                                                                          |
   |                        |                                                                                                                         |                                                                                                                                                                                                                                                          |
   |                        |                                                                                                                         |    resource "opentelekomcloud_vpc_v1" "my_hello_world_vpc" {                                                                                                                                                                                             |
   |                        |                                                                                                                         |      for_each = {                                                                                                                                                                                                                                        |
   |                        |                                                                                                                         |        "vpc1" = "test_vpc"                                                                                                                                                                                                                               |
   |                        |                                                                                                                         |        "vpc2" = "test_vpc"                                                                                                                                                                                                                               |
   |                        |                                                                                                                         |      }                                                                                                                                                                                                                                                   |
   |                        |                                                                                                                         |      name = each.value                                                                                                                                                                                                                                   |
   |                        |                                                                                                                         |    }                                                                                                                                                                                                                                                     |
   |                        |                                                                                                                         |                                                                                                                                                                                                                                                          |
   |                        |                                                                                                                         | In a JSON template, opentelekomcloud_vpc_v1.my_hello_world_vpc["vpc1"] and opentelekomcloud_vpc_v1.my_hello_world_vpc["vpc2"] identify two resources.                                                                                                    |
   |                        |                                                                                                                         |                                                                                                                                                                                                                                                          |
   |                        |                                                                                                                         | .. code-block::                                                                                                                                                                                                                                          |
   |                        |                                                                                                                         |                                                                                                                                                                                                                                                          |
   |                        |                                                                                                                         |    {                                                                                                                                                                                                                                                     |
   |                        |                                                                                                                         |      "resource": {                                                                                                                                                                                                                                       |
   |                        |                                                                                                                         |        "opentelekomcloud_vpc_v1": {                                                                                                                                                                                                                      |
   |                        |                                                                                                                         |          "my_hello_world_vpc": {                                                                                                                                                                                                                         |
   |                        |                                                                                                                         |            "for_each": {                                                                                                                                                                                                                                 |
   |                        |                                                                                                                         |              "vpc1": "test_vpc",                                                                                                                                                                                                                         |
   |                        |                                                                                                                         |              "vpc2": "test_vpc"                                                                                                                                                                                                                          |
   |                        |                                                                                                                         |            }                                                                                                                                                                                                                                             |
   |                        |                                                                                                                         |            "name": "${each.value}"                                                                                                                                                                                                                       |
   |                        |                                                                                                                         |          }                                                                                                                                                                                                                                               |
   |                        |                                                                                                                         |        }                                                                                                                                                                                                                                                 |
   |                        |                                                                                                                         |      }                                                                                                                                                                                                                                                   |
   |                        |                                                                                                                         |    }                                                                                                                                                                                                                                                     |
   +------------------------+-------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | resource_status        | String                                                                                                                  | Status of the resource.                                                                                                                                                                                                                                  |
   |                        |                                                                                                                         |                                                                                                                                                                                                                                                          |
   |                        |                                                                                                                         | -  CREATION_IN_PROGRESS: The resource is being created.                                                                                                                                                                                                  |
   |                        |                                                                                                                         | -  CREATION_FAILED: Create resource failed.                                                                                                                                                                                                              |
   |                        |                                                                                                                         | -  CREATION_COMPLETE: Resource created.                                                                                                                                                                                                                  |
   |                        |                                                                                                                         | -  DELETION_IN_PROGRESS: The resource is being deleted.                                                                                                                                                                                                  |
   |                        |                                                                                                                         | -  DELETION_FAILED: Delete resource failed.                                                                                                                                                                                                              |
   |                        |                                                                                                                         | -  DELETION_COMPLETE: Resource deleted.                                                                                                                                                                                                                  |
   |                        |                                                                                                                         | -  UPDATE_IN_PROGRESS: The resource is being updated. The update is not a replacement. In the case of a replacement update, a replacement resource is created and then the old resource is deleted.                                                      |
   |                        |                                                                                                                         | -  UPDATE_FAILED: Update resource failed. The update is not a replacement. In the case of a replacement update, a replacement resource is created and then the old resource is deleted.                                                                  |
   |                        |                                                                                                                         | -  UPDATE_COMPLETE: Resource updated. The update is not a replacement. In the case of a replacement update, a replacement resource is created and then the old resource is deleted.                                                                      |
   |                        |                                                                                                                         |                                                                                                                                                                                                                                                          |
   |                        |                                                                                                                         | Enumeration values:                                                                                                                                                                                                                                      |
   |                        |                                                                                                                         |                                                                                                                                                                                                                                                          |
   |                        |                                                                                                                         | -  **CREATION_IN_PROGRESS**                                                                                                                                                                                                                              |
   |                        |                                                                                                                         | -  **CREATION_FAILED**                                                                                                                                                                                                                                   |
   |                        |                                                                                                                         | -  **CREATION_COMPLETE**                                                                                                                                                                                                                                 |
   |                        |                                                                                                                         | -  **DELETION_IN_PROGRESS**                                                                                                                                                                                                                              |
   |                        |                                                                                                                         | -  **DELETION_FAILED**                                                                                                                                                                                                                                   |
   |                        |                                                                                                                         | -  **DELETION_COMPLETE**                                                                                                                                                                                                                                 |
   |                        |                                                                                                                         | -  **UPDATE_IN_PROGRESS**                                                                                                                                                                                                                                |
   |                        |                                                                                                                         | -  **UPDATE_FAILED**                                                                                                                                                                                                                                     |
   |                        |                                                                                                                         | -  **UPDATE_COMPLETE**                                                                                                                                                                                                                                   |
   +------------------------+-------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | status_message         | String                                                                                                                  | If the resource is in a failure state (ending with FAILED), a summary of the error information is displayed for debugging.                                                                                                                               |
   +------------------------+-------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | resource_attributes    | Array of :ref:`ResourceAttribute <liststackresources__en-us_topic_0000001709159310_response_resourceattribute>` objects | Resource attribute list.                                                                                                                                                                                                                                 |
   +------------------------+-------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _liststackresources__en-us_topic_0000001709159310_response_resourceattribute:

.. table:: **Table 6** ResourceAttribute

   ========= ====== =========================
   Parameter Type   Description
   ========= ====== =========================
   key       String Resource attribute key.
   value     String Resource attribute value.
   ========= ====== =========================

**Status code: 400**

.. table:: **Table 7** Response body parameters

   ========== ====== =================
   Parameter  Type   Description
   ========== ====== =================
   error_code String Response code.
   error_msg  String Response message.
   ========== ====== =================

**Status code: 401**

.. table:: **Table 8** Response body parameters

   ========== ====== =================
   Parameter  Type   Description
   ========== ====== =================
   error_code String Response code.
   error_msg  String Response message.
   ========== ====== =================

**Status code: 403**

.. table:: **Table 9** Response body parameters

   ========== ====== =================
   Parameter  Type   Description
   ========== ====== =================
   error_code String Response code.
   error_msg  String Response message.
   ========== ====== =================

**Status code: 404**

.. table:: **Table 10** Response body parameters

   ========== ====== =================
   Parameter  Type   Description
   ========== ====== =================
   error_code String Response code.
   error_msg  String Response message.
   ========== ====== =================

**Status code: 429**

.. table:: **Table 11** Response body parameters

   ========== ====== =================
   Parameter  Type   Description
   ========== ====== =================
   error_code String Response code.
   error_msg  String Response message.
   ========== ====== =================

**Status code: 500**

.. table:: **Table 12** Response body parameters

   ========== ====== =================
   Parameter  Type   Description
   ========== ====== =================
   error_code String Response code.
   error_msg  String Response message.
   ========== ====== =================

Example Requests
----------------

-  List the stack resources.

   .. code-block:: text

      GET https://{endpoint}/v1/ba2b9930c977f71edaeaa3a5e96a8ff1/stacks/my_hello_world_stack/resources

-  List the stack resources and check whether the stack ID matches the current stack.

   .. code-block:: text

      GET https://{endpoint}/v1/ba2b9930c977f71edaeaa3a5e96a8ff1/stacks/my_hello_world_stack/resources?stack_id=ea6a4f0e-ee8a-494e-b12a-8be4a1e65af2

Example Responses
-----------------

**Status code: 200**

Stack resources listed.

.. code-block::

   {
     "stack_resources" : [ {
       "logical_resource_name" : "vpc",
       "logical_resource_type" : "opentelekomcloud_vpc_v1",
       "physical_resource_id" : "38d617da-9b7f-4550-9ff7-d0e271dd4735",
       "physical_resource_name" : "my_vpc",
       "resource_attributes" : [ {
         "key" : "cidr",
         "value" : "172.16.0.0/16"
       }, {
         "key" : "description",
         "value" : ""
       }, {
         "key" : "id",
         "value" : "38d617da-9b7f-4550-9ff7-d0e271dd4735"
       }, {
         "key" : "name",
         "value" : "test_name"
       }, {
         "key" : "secondary_cidr",
         "value" : "null"
       }, {
         "key" : "tags",
         "value" : "null"
       }],
       "resource_status" : "CREATION_COMPLETE"
     } ]
   }

Status Codes
------------

=========== =======================================================
Status Code Description
=========== =======================================================
200         Stack resources listed.
400         Invalid request.
401         Authentication failed.
403         The user does not have the permission to call this API.
404         The stack does not exist.
429         Too frequent requests.
500         Internal server error.
=========== =======================================================
