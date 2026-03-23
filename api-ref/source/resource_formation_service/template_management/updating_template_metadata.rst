:original_name: UpdateTemplateMetadata.html

.. _UpdateTemplateMetadata:

Updating Template Metadata
==========================

Function
--------

This API updates template metadata.

-  This API only updates template description.

URI
---

PATCH /v1/{project_id}/templates/{template_name}/metadata

.. table:: **Table 1** Path Parameters

   +-----------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                                                                                                                                                            |
   +=================+=================+=================+========================================================================================================================================================================================================================================+
   | project_id      | Yes             | String          | Project ID. It can be obtained by calling an API or from the console.                                                                                                                                                                  |
   |                 |                 |                 |                                                                                                                                                                                                                                        |
   |                 |                 |                 | Minimum: **3**                                                                                                                                                                                                                         |
   |                 |                 |                 |                                                                                                                                                                                                                                        |
   |                 |                 |                 | Maximum: **64**                                                                                                                                                                                                                        |
   +-----------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | template_name   | Yes             | String          | Name of the template to be updated. Name is unique within its domain (domain_id), region, and project (project_id). It is case-sensitive and starts with a letter. Only letters, digits, underscores (_), and hyphens (-) are allowed. |
   |                 |                 |                 |                                                                                                                                                                                                                                        |
   |                 |                 |                 | Minimum: **1**                                                                                                                                                                                                                         |
   |                 |                 |                 |                                                                                                                                                                                                                                        |
   |                 |                 |                 | Maximum: **128**                                                                                                                                                                                                                       |
   +-----------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

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

   +----------------------+-----------------+-----------------+--------------------------------------------------------------------------------+
   | Parameter            | Mandatory       | Type            | Description                                                                    |
   +======================+=================+=================+================================================================================+
   | template_id          | No              | String          | Unique template ID. It is randomly generated by the template service.          |
   |                      |                 |                 |                                                                                |
   |                      |                 |                 | Minimum: **36**                                                                |
   |                      |                 |                 |                                                                                |
   |                      |                 |                 | Maximum: **36**                                                                |
   +----------------------+-----------------+-----------------+--------------------------------------------------------------------------------+
   | template_description | Yes             | String          | Template description. It can be used by users to identify their own templates. |
   |                      |                 |                 |                                                                                |
   |                      |                 |                 | Minimum: **0**                                                                 |
   |                      |                 |                 |                                                                                |
   |                      |                 |                 | Maximum: **1024**                                                              |
   +----------------------+-----------------+-----------------+--------------------------------------------------------------------------------+

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

Update template metadata.

.. code-block::

   PATCH https://{endpoint}/v1/c364070ab35041ddae68cf8b4839b60f/templates/my_template/metadata

   {
     "template_id" : "1b15e005-bdbb-4bd7-8f9a-a09b6774b4b3",
     "template_description" : "my template description"
   }

Example Responses
-----------------

None

Status Codes
------------

=========== =======================================================
Status Code Description
=========== =======================================================
204         Template metadata updated. No data returned.
400         Invalid request.
401         Authentication failed.
403         The user does not have the permission to call this API.
404         The template does not exist.
429         Too frequent requests.
500         Internal server error.
=========== =======================================================
