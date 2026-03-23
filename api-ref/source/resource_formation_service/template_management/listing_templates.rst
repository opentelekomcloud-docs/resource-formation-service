:original_name: ListTemplates.html

.. _ListTemplates:

Listing Templates
=================

Function
--------

This API lists all your templates at the current region.

-  By default, the templates are sorted by creation time. The template created latest is displayed on the top.
-  Currently, all templates are returned. Pagination is not supported.
-  If no template is available, an empty list will be returned.
-  To obtain details about template versions, call :ref:`ListTemplateVersions <listtemplateversions>`.

ListTemplates returns only summaries of templates. You can obtain details about the summaries by referring to :ref:`Response Parameters <listtemplates__section87104512437>`. For details about a particular template, call :ref:`ShowTemplateMetadata <showtemplatemetadata>`.

URI
---

GET /v1/{project_id}/templates

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

.. _listtemplates__section87104512437:

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 3** Response body parameters

   +-----------+--------------------------------------------------------------------------------------------------+----------------+
   | Parameter | Type                                                                                             | Description    |
   +===========+==================================================================================================+================+
   | templates | Array of :ref:`Template <listtemplates__en-us_topic_0000001757158493_response_template>` objects | Template list. |
   +-----------+--------------------------------------------------------------------------------------------------+----------------+

.. _listtemplates__en-us_topic_0000001757158493_response_template:

.. table:: **Table 4** Template

   +----------------------------+--------+---------------------------------------------------------------------------------------------------------------------------+
   | Parameter                  | Type   | Description                                                                                                               |
   +============================+========+===========================================================================================================================+
   | template_id                | String | Unique template ID. It is randomly generated by the template service.                                                     |
   +----------------------------+--------+---------------------------------------------------------------------------------------------------------------------------+
   | template_name              | String | Name of the template to be created.                                                                                       |
   +----------------------------+--------+---------------------------------------------------------------------------------------------------------------------------+
   | template_description       | String | Template description. It can be used by users to identify their own templates.                                            |
   +----------------------------+--------+---------------------------------------------------------------------------------------------------------------------------+
   | create_time                | String | Creation time of a template. The format complies with RFC 3339 (YYYY-MM-DDTHH:MM:SSZ), for example, 1970-01-01T00:00:00Z. |
   +----------------------------+--------+---------------------------------------------------------------------------------------------------------------------------+
   | update_time                | String | Update time of a template. The format complies with RFC 3339 (YYYY-MM-DDTHH:MM:SSZ), for example, 1970-01-01T00:00:00Z.   |
   +----------------------------+--------+---------------------------------------------------------------------------------------------------------------------------+
   | latest_version_id          | String | ID of the latest template version.                                                                                        |
   +----------------------------+--------+---------------------------------------------------------------------------------------------------------------------------+
   | latest_version_description | String | Description of the latest template version.                                                                               |
   +----------------------------+--------+---------------------------------------------------------------------------------------------------------------------------+

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

List all your templates at the current region.

.. code-block:: text

   GET https://{endpoint}/v1/c364070ab35041ddae68cf8b4839b60f/templates

Example Responses
-----------------

**Status code: 200**

Templates listed.

.. code-block::

   {
     "templates" : [ {
       "template_id" : "69f8d5ea-eaa4-4a3b-a96d-bae9230e97c8",
       "template_name" : "my_first_template",
       "template_description" : "Template description",
       "create_time" : "2023-05-09T08:00:00Z",
       "update_time" : "2023-05-09T09:00:00Z",
       "latest_version_description" : "Latest version description",
       "latest_version_id" : "V10"
     }, {
       "template_id" : "69f8d5ea-eaa4-4a3b-a96d-bae9230e97c9",
       "template_name" : "my_second_template",
       "template_description" : "Description",
       "create_time" : "2023-05-09T09:00:00Z",
       "update_time" : "2023-05-09T10:00:00Z",
       "latest_version_description" : "Latest version description",
       "latest_version_id" : "V10"
     } ]
   }

Status Codes
------------

=========== =======================================================
Status Code Description
=========== =======================================================
200         Templates listed.
400         Invalid request.
401         Authentication failed.
403         The user does not have the permission to call this API.
429         Too frequent requests.
500         Internal server error.
=========== =======================================================
