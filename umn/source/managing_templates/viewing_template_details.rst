:original_name: en-us_topic_0000002119404102.html

.. _en-us_topic_0000002119404102:

Viewing Template Details
========================

#. Log in to the management console.

#. In the upper left corner of the page, click |image1|, and then click **Management & Deployment** > **Resource Formation Service**.

   The \ **Dashboard**\  page is displayed.


   .. figure:: /_static/images/en-us_image_0000002157147725.png
      :alt: **Figure 1** RFS Dashboard

      **Figure 1** RFS Dashboard

#. In the left navigation pane, choose \ **Templates**\  -> **Private Templates**\ . You can see all the templates created under the current account.


   .. figure:: /_static/images/en-us_image_0000002158823546.png
      :alt: **Figure 2** RFS Private Templates

      **Figure 2** RFS Private Templates

#. Click the name of the desired template to view its details.

   There are three function modules on the template details page:

   a. **Basic Information**: displays basic information about the template, such as \ **Template Name**\ , \ **Template ID**\ , \ **Template Description**\ , etc, as shown in :ref:`Figure Template Details <en-us_topic_0000002119404102__fig045261413418>`. You can modify the template description here.
   b. **Version Info**: displays all the version information of this template. You can view the content of any version in **Version** **Preview** by clicking the preview icon for that version. You can also perform different operations on the template versions, such as edit, delete, export or create a stack.
   c. **Version Preview**: displays the template content of the specified version

   .. _en-us_topic_0000002119404102__fig045261413418:

   .. figure:: /_static/images/en-us_image_0000002158983038.png
      :alt: **Figure 3** Template Details

      **Figure 3** Template Details

   You can perform the following operations on the template versions:

   -  **Editing a version**: this will create a new template version based on the selected version. To start editing a specific template version, click **Edit** in the **Operation** column of the desired version.
   -  **Exporting a version**: this will export the selected template version in a zip file format. The naming convention of the export file is: “{TEMPLATE_NAME}-{TEMPLATE_VERSION}.zip”. To export a specific template version, click **More** -> **Export** in the **Operation** column of the desired version.
   -  **Deleting a version**: this will delete the selected template version. You can delete a single version or multiple versions in batches:

      a. To delete a single template version, click **More** -> **Delete** in the **Operation** column.
      b. To delete multiple template versions in batches, select the desired template versions and click the **Delete** in the upper left corner above the version table.

         .. caution::

            -  The deletion cannot be undone.
            -  If a template has only one version, the deletion of that version will result in the deletion of the entire template.

   -  **Creating a stack**: this will initiate the creation of a new stack based on the selected template version. To start creating a stack based on a specific template version, click **Create Stack** in the **Operation** column of the desired version. For more information about the entire stack creation procedure, check :ref:`Creating a Stack from a Template. <en-us_topic_0000002046584002>`

.. |image1| image:: /_static/images/en-us_image_0000002158979846.png
