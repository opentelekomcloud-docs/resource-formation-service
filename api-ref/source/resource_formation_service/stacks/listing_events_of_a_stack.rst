:original_name: ListStackEvents.html

.. _ListStackEvents:

Listing Events of a Stack
=========================

Function
--------

This API lists all deployment events of a stack.

-  If deployment_id is assigned, deployment_id is used as a query criterion and the stack events corresponding to a specific deployment are returned. If no deployment_id is assigned, all of the stack events are returned.
-  If the deployment corresponding to the given deployment_id does not exist, 404 is returned.
-  You can use filter to query stack events by specifying the event type (event_type), resource type (resource_type), and resource name (resource_name).
-  You can use field to set the attributes to be returned. The attribute event type (event_type) cannot be configured and it is returned by default. The available attributes are elapsed time (elapsed_seconds), event message (event_message), resource ID key (resource_id_key), resource ID value (resource_id_value), resource key (resource_key), resource type (resource_type), resource name (resource_name), and timestamp (timestamp).
-  The returned events are arranged in descending order of time.

URI
---

GET /v1/{project_id}/stacks/{stack_name}/events

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

   +-----------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                                                                                                                                 |
   +=================+=================+=================+=============================================================================================================================================================================================================+
   | stack_id        | No              | String          | Unique stack ID.                                                                                                                                                                                            |
   |                 |                 |                 |                                                                                                                                                                                                             |
   |                 |                 |                 | It is a UUID generated by RFS when a stack is created.                                                                                                                                                      |
   |                 |                 |                 |                                                                                                                                                                                                             |
   |                 |                 |                 | Stack name is unique, if you create stack with name ‘HelloWorld’, the same name cannot be used for another stack until original stack is deleted.                                                           |
   |                 |                 |                 |                                                                                                                                                                                                             |
   |                 |                 |                 | For parallel development, team members may want to ensure that they are operating the stack they created, not one with the same name created by other members after deleting the previous one.              |
   |                 |                 |                 |                                                                                                                                                                                                             |
   |                 |                 |                 | To avoid this mismatch, check the ID, since RFS ensures each stack has a unique ID that does not change with updates. If the stack_id value differs from the current stack ID, 400 is returned.             |
   |                 |                 |                 |                                                                                                                                                                                                             |
   |                 |                 |                 | Minimum: **36**                                                                                                                                                                                             |
   |                 |                 |                 |                                                                                                                                                                                                             |
   |                 |                 |                 | Maximum: **36**                                                                                                                                                                                             |
   +-----------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | deployment_id   | No              | String          | Unique deployment ID. It is a UUID generated by RFS when deployment or rollback is triggered.                                                                                                               |
   |                 |                 |                 |                                                                                                                                                                                                             |
   |                 |                 |                 | Minimum: **36**                                                                                                                                                                                             |
   |                 |                 |                 |                                                                                                                                                                                                             |
   |                 |                 |                 | Maximum: **36**                                                                                                                                                                                             |
   +-----------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | filter          | No              | String          | Filter criteria.                                                                                                                                                                                            |
   |                 |                 |                 |                                                                                                                                                                                                             |
   |                 |                 |                 | -  The AND operator is defined using a comma (,).                                                                                                                                                           |
   |                 |                 |                 | -  The OR operator is defined using a vertical bar (|). The OR operator has a higher priority than the AND operator.                                                                                        |
   |                 |                 |                 | -  Parentheses are not supported.                                                                                                                                                                           |
   |                 |                 |                 | -  Only equal signs (==) are supported as the filter operator.                                                                                                                                              |
   |                 |                 |                 | -  Filter parameter names and values can contain only letters, digits, and underscores (_). Semicolons (;) are not allowed in filter criteria. If semicolons are used, the filter criteria will be ignored. |
   |                 |                 |                 | -  A filter parameter can be related to only one AND condition. Multiple OR conditions in an AND condition can be related to only one filter parameter.                                                     |
   |                 |                 |                 |                                                                                                                                                                                                             |
   |                 |                 |                 | Minimum: **0**                                                                                                                                                                                              |
   |                 |                 |                 |                                                                                                                                                                                                             |
   |                 |                 |                 | Maximum: **512**                                                                                                                                                                                            |
   +-----------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | field           | No              | String          | Specified attribute name.                                                                                                                                                                                   |
   |                 |                 |                 |                                                                                                                                                                                                             |
   |                 |                 |                 | -  The attribute name can contain only letters, digits, and underscores (_).                                                                                                                                |
   |                 |                 |                 | -  Multiple attribute names are separated by commas (,).                                                                                                                                                    |
   |                 |                 |                 |                                                                                                                                                                                                             |
   |                 |                 |                 | Minimum: **0**                                                                                                                                                                                              |
   |                 |                 |                 |                                                                                                                                                                                                             |
   |                 |                 |                 | Maximum: **128**                                                                                                                                                                                            |
   +-----------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

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

   +--------------+--------------------------------------------------------------------------------------------------------+-----------------------+
   | Parameter    | Type                                                                                                   | Description           |
   +==============+========================================================================================================+=======================+
   | stack_events | Array of :ref:`StackEvent <liststackevents__en-us_topic_0000001757158469_response_stackevent>` objects | List of stack events. |
   +--------------+--------------------------------------------------------------------------------------------------------+-----------------------+

.. _liststackevents__en-us_topic_0000001757158469_response_stackevent:

.. table:: **Table 5** StackEvent

   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                                                                                                                                                                                                        |
   +=======================+=======================+====================================================================================================================================================================================================================================================================================+
   | resource_type         | String                | Resource type.                                                                                                                                                                                                                                                                     |
   |                       |                       |                                                                                                                                                                                                                                                                                    |
   |                       |                       | For example, in the following HCL template, the value of resource_type is opentelekomcloud_vpc_v1.                                                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                                                                                                    |
   |                       |                       | .. code-block::                                                                                                                                                                                                                                                                    |
   |                       |                       |                                                                                                                                                                                                                                                                                    |
   |                       |                       |    resource "opentelekomcloud_vpc_v1" "my_hello_world_vpc" {                                                                                                                                                                                                                       |
   |                       |                       |      name = "test_vpc"                                                                                                                                                                                                                                                             |
   |                       |                       |    }                                                                                                                                                                                                                                                                               |
   |                       |                       |                                                                                                                                                                                                                                                                                    |
   |                       |                       | In a JSON template, the value of resource_type is opentelekomcloud_vpc_v1.                                                                                                                                                                                                         |
   |                       |                       |                                                                                                                                                                                                                                                                                    |
   |                       |                       | .. code-block::                                                                                                                                                                                                                                                                    |
   |                       |                       |                                                                                                                                                                                                                                                                                    |
   |                       |                       |    {                                                                                                                                                                                                                                                                               |
   |                       |                       |      "resource": {                                                                                                                                                                                                                                                                 |
   |                       |                       |        "opentelekomcloud_vpc_v1": {                                                                                                                                                                                                                                                |
   |                       |                       |          "my_hello_world_vpc": {                                                                                                                                                                                                                                                   |
   |                       |                       |            "name": "test_vpc"                                                                                                                                                                                                                                                      |
   |                       |                       |          }                                                                                                                                                                                                                                                                         |
   |                       |                       |        }                                                                                                                                                                                                                                                                           |
   |                       |                       |      }                                                                                                                                                                                                                                                                             |
   |                       |                       |    }                                                                                                                                                                                                                                                                               |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | resource_name         | String                | Resource name. The default value is the logical name of a resource.                                                                                                                                                                                                                |
   |                       |                       |                                                                                                                                                                                                                                                                                    |
   |                       |                       | For example, in the following HCL template, the value of resource_name is my_hello_world_vpc.                                                                                                                                                                                      |
   |                       |                       |                                                                                                                                                                                                                                                                                    |
   |                       |                       | .. code-block::                                                                                                                                                                                                                                                                    |
   |                       |                       |                                                                                                                                                                                                                                                                                    |
   |                       |                       |    resource "opentelekomcloud_vpc_v1" "my_hello_world_vpc" {                                                                                                                                                                                                                       |
   |                       |                       |      name = "test_vpc"                                                                                                                                                                                                                                                             |
   |                       |                       |    }                                                                                                                                                                                                                                                                               |
   |                       |                       |                                                                                                                                                                                                                                                                                    |
   |                       |                       | In a JSON template, the value of resource_name is my_hello_world_vpc.                                                                                                                                                                                                              |
   |                       |                       |                                                                                                                                                                                                                                                                                    |
   |                       |                       | .. code-block::                                                                                                                                                                                                                                                                    |
   |                       |                       |                                                                                                                                                                                                                                                                                    |
   |                       |                       |    {                                                                                                                                                                                                                                                                               |
   |                       |                       |      "resource": {                                                                                                                                                                                                                                                                 |
   |                       |                       |        "opentelekomcloud_vpc_v1": {                                                                                                                                                                                                                                                |
   |                       |                       |          "my_hello_world_vpc": {                                                                                                                                                                                                                                                   |
   |                       |                       |            "name": "test_vpc"                                                                                                                                                                                                                                                      |
   |                       |                       |          }                                                                                                                                                                                                                                                                         |
   |                       |                       |        }                                                                                                                                                                                                                                                                           |
   |                       |                       |      }                                                                                                                                                                                                                                                                             |
   |                       |                       |    }                                                                                                                                                                                                                                                                               |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | resource_id_key       | String                | Name of resource ID. If a resource is not created, resource_id_key is not returned. The ID is defined by a provider. Different providers may comply with different naming rules. For details about the naming rules, contact provider developers or read provider's documentation. |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | resource_id_value     | String                | Resource ID value. If a resource is not created, resource_id_value is not returned.                                                                                                                                                                                                |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | resource_key          | String                | Resource key. If **count** or **for_each** parameter is used in a template, resource_key will be returned.                                                                                                                                                                         |
   |                       |                       |                                                                                                                                                                                                                                                                                    |
   |                       |                       | If **count** is used in a template, resource_key is a number starting from 0.                                                                                                                                                                                                      |
   |                       |                       |                                                                                                                                                                                                                                                                                    |
   |                       |                       | For example, in the following HCL template, if the count is 2, two resources will be generated and the value of resource_key is 0 and 1.                                                                                                                                           |
   |                       |                       |                                                                                                                                                                                                                                                                                    |
   |                       |                       | .. code-block::                                                                                                                                                                                                                                                                    |
   |                       |                       |                                                                                                                                                                                                                                                                                    |
   |                       |                       |    resource "opentelekomcloud_vpc_v1" "my_hello_world_vpc" {                                                                                                                                                                                                                       |
   |                       |                       |      count = 2                                                                                                                                                                                                                                                                     |
   |                       |                       |      name = "test_vpc"                                                                                                                                                                                                                                                             |
   |                       |                       |    }                                                                                                                                                                                                                                                                               |
   |                       |                       |                                                                                                                                                                                                                                                                                    |
   |                       |                       | In a JSON template, the value of resource_key is 0 and 1.                                                                                                                                                                                                                          |
   |                       |                       |                                                                                                                                                                                                                                                                                    |
   |                       |                       | .. code-block::                                                                                                                                                                                                                                                                    |
   |                       |                       |                                                                                                                                                                                                                                                                                    |
   |                       |                       |    {                                                                                                                                                                                                                                                                               |
   |                       |                       |      "resource": {                                                                                                                                                                                                                                                                 |
   |                       |                       |        "opentelekomcloud_vpc_v1": {                                                                                                                                                                                                                                                |
   |                       |                       |          "my_hello_world_vpc": {                                                                                                                                                                                                                                                   |
   |                       |                       |            "name": "test_vpc",                                                                                                                                                                                                                                                     |
   |                       |                       |            "count": 2                                                                                                                                                                                                                                                              |
   |                       |                       |          }                                                                                                                                                                                                                                                                         |
   |                       |                       |        }                                                                                                                                                                                                                                                                           |
   |                       |                       |      }                                                                                                                                                                                                                                                                             |
   |                       |                       |    }                                                                                                                                                                                                                                                                               |
   |                       |                       |                                                                                                                                                                                                                                                                                    |
   |                       |                       | If for_each parameter is used in a template, resource_key is a user-defined string. In the following HCL template, the value of resource_key is vpc1 and vpc2.                                                                                                                     |
   |                       |                       |                                                                                                                                                                                                                                                                                    |
   |                       |                       | .. code-block::                                                                                                                                                                                                                                                                    |
   |                       |                       |                                                                                                                                                                                                                                                                                    |
   |                       |                       |    resource "opentelekomcloud_vpc_v1" "my_hello_world_vpc" {                                                                                                                                                                                                                       |
   |                       |                       |      for_each = {                                                                                                                                                                                                                                                                  |
   |                       |                       |        "vpc1" = "test_vpc"                                                                                                                                                                                                                                                         |
   |                       |                       |        "vpc2" = "test_vpc"                                                                                                                                                                                                                                                         |
   |                       |                       |      }                                                                                                                                                                                                                                                                             |
   |                       |                       |      name = each.value                                                                                                                                                                                                                                                             |
   |                       |                       |    }                                                                                                                                                                                                                                                                               |
   |                       |                       |                                                                                                                                                                                                                                                                                    |
   |                       |                       | In the following JSON template, the value of resource_key is vpc1 and vpc2.                                                                                                                                                                                                        |
   |                       |                       |                                                                                                                                                                                                                                                                                    |
   |                       |                       | .. code-block::                                                                                                                                                                                                                                                                    |
   |                       |                       |                                                                                                                                                                                                                                                                                    |
   |                       |                       |    {                                                                                                                                                                                                                                                                               |
   |                       |                       |      "resource": {                                                                                                                                                                                                                                                                 |
   |                       |                       |        "opentelekomcloud_vpc_v1": {                                                                                                                                                                                                                                                |
   |                       |                       |          "my_hello_world_vpc": {                                                                                                                                                                                                                                                   |
   |                       |                       |            "for_each": {                                                                                                                                                                                                                                                           |
   |                       |                       |              "vpc1": "test_vpc",                                                                                                                                                                                                                                                   |
   |                       |                       |              "vpc2": "test_vpc"                                                                                                                                                                                                                                                    |
   |                       |                       |            }                                                                                                                                                                                                                                                                       |
   |                       |                       |            "name": "${each.value}"                                                                                                                                                                                                                                                 |
   |                       |                       |          }                                                                                                                                                                                                                                                                         |
   |                       |                       |        }                                                                                                                                                                                                                                                                           |
   |                       |                       |      }                                                                                                                                                                                                                                                                             |
   |                       |                       |    }                                                                                                                                                                                                                                                                               |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | time                  | String                | Occurrence time of an event. The format complies with RFC 3339 (YYYY-MM-DDTHH:MM:SSZ), for example, 1970-01-01T00:00:00Z.                                                                                                                                                          |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | event_type            | String                | Event types may include:                                                                                                                                                                                                                                                           |
   |                       |                       |                                                                                                                                                                                                                                                                                    |
   |                       |                       | -  **LOG**: records status information, such as the current status and target status.                                                                                                                                                                                              |
   |                       |                       | -  **ERROR**: records failure information.                                                                                                                                                                                                                                         |
   |                       |                       | -  **DRIFT**: records resource deviation information.                                                                                                                                                                                                                              |
   |                       |                       | -  **SUMMARY**: records summary of resource change results.                                                                                                                                                                                                                        |
   |                       |                       | -  **CREATION_IN_PROGRESS**: The event is being created.                                                                                                                                                                                                                           |
   |                       |                       | -  **CREATION_FAILED**: Failed to create the event.                                                                                                                                                                                                                                |
   |                       |                       | -  **CREATION_COMPLETE**: Event created.                                                                                                                                                                                                                                           |
   |                       |                       | -  **DELETION_IN_PROGRESS**: The event is being deleted.                                                                                                                                                                                                                           |
   |                       |                       | -  **DELETION_FAILED**: Delete event failed.                                                                                                                                                                                                                                       |
   |                       |                       | -  **DELETION_COMPLETE**: Event deleted.                                                                                                                                                                                                                                           |
   |                       |                       | -  **UPDATE_IN_PROGRESS**: The event is being updated. The update is not a replacement. In the case of a replacement update, a replacement event is created and then the old event is deleted.                                                                                     |
   |                       |                       | -  **UPDATE_FAILED**: Update event failed. The update is not a replacement. In the case of a replacement update, a replacement event is created and then the old event is deleted.                                                                                                 |
   |                       |                       | -  **UPDATE_COMPLETE**: Event updated. The update is not a replacement. In the case of a replacement update, a replacement event is created and then the old event is deleted.                                                                                                     |
   |                       |                       |                                                                                                                                                                                                                                                                                    |
   |                       |                       | Enumeration values:                                                                                                                                                                                                                                                                |
   |                       |                       |                                                                                                                                                                                                                                                                                    |
   |                       |                       | -  **LOG**                                                                                                                                                                                                                                                                         |
   |                       |                       | -  **ERROR**                                                                                                                                                                                                                                                                       |
   |                       |                       | -  **DRIFT**                                                                                                                                                                                                                                                                       |
   |                       |                       | -  **SUMMARY**                                                                                                                                                                                                                                                                     |
   |                       |                       | -  **CREATION_IN_PROGRESS**                                                                                                                                                                                                                                                        |
   |                       |                       | -  **CREATION_FAILED**                                                                                                                                                                                                                                                             |
   |                       |                       | -  **CREATION_COMPLETE**                                                                                                                                                                                                                                                           |
   |                       |                       | -  **DELETION_IN_PROGRESS**                                                                                                                                                                                                                                                        |
   |                       |                       | -  **DELETION_FAILED**                                                                                                                                                                                                                                                             |
   |                       |                       | -  **DELETION_COMPLETE**                                                                                                                                                                                                                                                           |
   |                       |                       | -  **UPDATE_IN_PROGRESS**                                                                                                                                                                                                                                                          |
   |                       |                       | -  **UPDATE_FAILED**                                                                                                                                                                                                                                                               |
   |                       |                       | -  **UPDATE_COMPLETE**                                                                                                                                                                                                                                                             |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | event_message         | String                | Details about a stack event.                                                                                                                                                                                                                                                       |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | elapsed_seconds       | Integer               | Event execution duration (Unit: seconds)                                                                                                                                                                                                                                           |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

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

-  Use filter to obtain stack events with the specified event_type and resource_name.

   .. code-block:: text

      GET https://{endpoint}/v1/ba2b9930c977f71edaeaa3a5e96a8ff1/stacks/my_hello_world_stack/events?filter=event_type==LOG,resource_name==my_hello_world_resource

-  Use field to select the following returned attributes: resource_key, resource_name, and event_type. The event_type attribute is automatically selected even if you do not select it.

   .. code-block:: text

      GET https://{endpoint}/v1/ba2b9930c977f71edaeaa3a5e96a8ff1/stacks/my_hello_world_stack/events?field=resource_key,resource_name

-  Obtain stack events of a specified deployment using deployment_id.

   .. code-block:: text

      GET https://{endpoint}/v1/ba2b9930c977f71edaeaa3a5e96a8ff1/stacks/my_hello_world_stack/events?deployment_id=81edbb3e-00d9-42fd-94c8-59c7525d0f28

Example Responses
-----------------

**Status code: 200**

Stack events listed.

.. code-block::

   {
     "stack_events" : [ {
       "event_message" : "Apply required resource success. ",
       "event_type" : "LOG",
       "time" : "2023-05-17T11:56:47Z"
     }, {
       "event_message" : "Apply complete! Resources: 1 added, 0 changed, 0 destroyed.",
       "event_type" : "SUMMARY",
       "time" : "2023-05-17T11:56:45Z"
     }, {
       "resource_type" : "opentelekomcloud_vpc_v1",
       "resource_name" : "vpc",
       "elapsed_seconds" : 8,
       "event_message" : "opentelekomcloud_vpc_v1.vpc: Creation complete after 8s [id=38d617da-9b7f-4550-9ff7-d0e271dd4735]",
       "event_type" : "CREATION_COMPLETE",
       "resource_id_key" : "id",
       "resource_id_value" : "38d617da-9b7f-4550-9ff7-d0e271dd4735",
       "time" : "2023-05-17T11:56:40Z"
     }, {
       "resource_type" : "opentelekomcloud_vpc_v1",
       "resource_name" : "vpc",
       "event_message" : "opentelekomcloud_vpc_v1.vpc: Creating...",
       "event_type" : "CREATION_IN_PROGRESS",
       "time" : "2023-05-17T11:56:32Z"
     }, {
       "event_message" : "Creating required resource now",
       "event_type" : "LOG",
       "time" : "2023-05-17T11:56:31Z"
     } ]
   }

Status Codes
------------

=========== =======================================================
Status Code Description
=========== =======================================================
200         Stack events listed.
400         Invalid request.
401         Authentication failed.
403         The user does not have the permission to call this API.
404         The stack or the specified deployment does not exist.
429         Too frequent requests.
500         Internal server error.
=========== =======================================================
