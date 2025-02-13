:original_name: en-us_topic_0000002119375338.html

.. _en-us_topic_0000002119375338:

Constraints and Limitations
===========================

Permissions
-----------

If it is needed, :ref:`create an agency <en-us_topic_0000001991890817>`.

.. note::

   If no agency is configured, RFS will have the permissions of the current user for deployment. An agency limits RFS's permissions on cloud service resoures, preventing undesired operations caused by incorrect templates or parameters.

Constraints
-----------

The following are basic constraints of RFS.

+----------------+------------------------------------------------------------------------------------------------------------------------+--------------------------+
| Resource       | Item                                                                                                                   | Limit                    |
+================+========================================================================================================================+==========================+
| Template       | Maximum length of a template name                                                                                      | 128 characters           |
+----------------+------------------------------------------------------------------------------------------------------------------------+--------------------------+
|                | Maximum length of a template file name                                                                                 | 255 bytes                |
+----------------+------------------------------------------------------------------------------------------------------------------------+--------------------------+
|                | Maximum length of a template URL                                                                                       | 2048 bytes               |
+----------------+------------------------------------------------------------------------------------------------------------------------+--------------------------+
|                | Maximum size of the file pointed to by the **template_uri** used in APIs for creating a template or a template version | 1 MB after decompression |
+----------------+------------------------------------------------------------------------------------------------------------------------+--------------------------+
|                | Maximum size of the file containing **template_body** used in APIs for creating a template or template version         | 50 KB                    |
+----------------+------------------------------------------------------------------------------------------------------------------------+--------------------------+
| Stack          | Timeout interval for creating a stack                                                                                  | 6 hours                  |
+----------------+------------------------------------------------------------------------------------------------------------------------+--------------------------+
|                | Maximum length of a stack name                                                                                         | 128 characters           |
+----------------+------------------------------------------------------------------------------------------------------------------------+--------------------------+
| Execution plan | Maximum length of an execution plan name                                                                               | 128 characters           |
+----------------+------------------------------------------------------------------------------------------------------------------------+--------------------------+
