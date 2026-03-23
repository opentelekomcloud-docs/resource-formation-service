:original_name: en-us_topic_0000001847241570.html

.. _en-us_topic_0000001847241570:

Creating a Template
===================

Function
--------

This API creates a template and generates its first version.

-  The request must contain either template_uri or template_body. The former is the OBS link of the template content, and the latter is the template content.
-  Template name is unique, if you create template with name ‘HelloWorld’, the same name cannot be used for another template until original template is deleted.
-  When a template is created, the template version V1 is automatically generated.
-  The template has at least one version.

URI
---

POST /v1/{project_id}/templates

.. table:: **Table 1** Path Parameters

   +-----------------+-----------------+-----------------+-----------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                           |
   +=================+=================+=================+=======================================================================+
   | project_id      | Yes             | String          | Project ID. It can be obtained by calling an API or from the console. |
   |                 |                 |                 |                                                                       |
   |                 |                 |                 | Minimum: **3**                                                        |
   |                 |                 |                 |                                                                       |
   |                 |                 |                 | Maximum: **64**                                                       |
   +-----------------+-----------------+-----------------+-----------------------------------------------------------------------+

Request Parameters
------------------

.. table:: **Table 2** Request header parameters

   +-------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------+
   | Parameter         | Mandatory       | Type            | Description                                                                                        |
   +===================+=================+=================+====================================================================================================+
   | Client-Request-Id | Yes             | String          | Unique request ID. It is specified by a user and is used to locate a request. UUID is recommended. |
   |                   |                 |                 |                                                                                                    |
   |                   |                 |                 | Minimum: **36**                                                                                    |
   |                   |                 |                 |                                                                                                    |
   |                   |                 |                 | Maximum: **128**                                                                                   |
   +-------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------+

.. table:: **Table 3** Request body parameters

   +----------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter            | Mandatory       | Type            | Description                                                                                                                                                                                                                            |
   +======================+=================+=================+========================================================================================================================================================================================================================================+
   | version_description  | No              | String          | Description of a template version. It can be used by users to identify their own template versions.                                                                                                                                    |
   |                      |                 |                 |                                                                                                                                                                                                                                        |
   |                      |                 |                 | Minimum: **0**                                                                                                                                                                                                                         |
   |                      |                 |                 |                                                                                                                                                                                                                                        |
   |                      |                 |                 | Maximum: **1024**                                                                                                                                                                                                                      |
   +----------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | template_body        | No              | String          | HCL template. It describes the resources used in the template. You can specify either template_body or template_uri, but not both.                                                                                                     |
   |                      |                 |                 |                                                                                                                                                                                                                                        |
   |                      |                 |                 | Minimum: **0**                                                                                                                                                                                                                         |
   |                      |                 |                 |                                                                                                                                                                                                                                        |
   |                      |                 |                 | Maximum: **51200**                                                                                                                                                                                                                     |
   +----------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | template_uri         | No              | String          | OBS link of an HCL template. The template describes the target status of a resource.                                                                                                                                                   |
   |                      |                 |                 |                                                                                                                                                                                                                                        |
   |                      |                 |                 | The corresponding file must be a pure **.tf** file or a **.zip** package.                                                                                                                                                              |
   |                      |                 |                 |                                                                                                                                                                                                                                        |
   |                      |                 |                 | A pure **.tf** file must end with **.tf** or **.tf.json** and comply with the HCL syntax.                                                                                                                                              |
   |                      |                 |                 |                                                                                                                                                                                                                                        |
   |                      |                 |                 | Currently, only the **.zip** package is supported. The file name extension must be **.zip**. The decompressed files cannot contain **.tfvars** files.                                                                                  |
   |                      |                 |                 |                                                                                                                                                                                                                                        |
   |                      |                 |                 | You can specify either template_body or template_uri, but not both.                                                                                                                                                                    |
   |                      |                 |                 |                                                                                                                                                                                                                                        |
   |                      |                 |                 | Minimum: **0**                                                                                                                                                                                                                         |
   |                      |                 |                 |                                                                                                                                                                                                                                        |
   |                      |                 |                 | Maximum: **1**                                                                                                                                                                                                                         |
   +----------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | template_name        | Yes             | String          | Name of the template to be created. Name is unique within its domain (domain_id), region, and project (project_id). It is case-sensitive and starts with a letter. Only letters, digits, underscores (_), and hyphens (-) are allowed. |
   |                      |                 |                 |                                                                                                                                                                                                                                        |
   |                      |                 |                 | Minimum: **1**                                                                                                                                                                                                                         |
   |                      |                 |                 |                                                                                                                                                                                                                                        |
   |                      |                 |                 | Maximum: **128**                                                                                                                                                                                                                       |
   +----------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | template_description | No              | String          | Template description. It can be used by users to identify their own templates.                                                                                                                                                         |
   |                      |                 |                 |                                                                                                                                                                                                                                        |
   |                      |                 |                 | Minimum: **0**                                                                                                                                                                                                                         |
   |                      |                 |                 |                                                                                                                                                                                                                                        |
   |                      |                 |                 | Maximum: **1024**                                                                                                                                                                                                                      |
   +----------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 4** Response body parameters

   +-------------+--------+-----------------------------------------------------------------------+
   | Parameter   | Type   | Description                                                           |
   +=============+========+=======================================================================+
   | template_id | String | Unique template ID. It is randomly generated by the template service. |
   +-------------+--------+-----------------------------------------------------------------------+
   | version_id  | String | Template version ID.                                                  |
   +-------------+--------+-----------------------------------------------------------------------+

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

**Status code: 409**

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

-  Create a template with template_name.

   .. code-block:: text

      POST https://{endpoint}/v1/c364070ab35041ddae68cf8b4839b60f/templates

      {
        "template_name" : "my_hello_world_template_name"
      }

Example Responses
-----------------

**Status code: 200**

Template version metadata obtained.

.. code-block::

   {
     "template_id" : "1b15e005-bdbb-4bd7-8f9a-a09b6774b4b3",
     "version_id":"V1"
   }

Status Codes
------------

+-------------+---------------------------------------------------------------------------+
| Status Code | Description                                                               |
+=============+===========================================================================+
| 200         | Template created.                                                         |
+-------------+---------------------------------------------------------------------------+
| 400         | Invalid request.                                                          |
+-------------+---------------------------------------------------------------------------+
| 401         | Authentication failed.                                                    |
+-------------+---------------------------------------------------------------------------+
| 403         | The user does not have the permission to call this API.                   |
+-------------+---------------------------------------------------------------------------+
| 409         | Creation requests conflict. A template with the same name already exists. |
+-------------+---------------------------------------------------------------------------+
| 429         | Too frequent requests.                                                    |
+-------------+---------------------------------------------------------------------------+
| 500         | Internal server error.                                                    |
+-------------+---------------------------------------------------------------------------+
