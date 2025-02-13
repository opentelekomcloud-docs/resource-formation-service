:original_name: en-us_topic_0000002046740822.html

.. _en-us_topic_0000002046740822:

Creating a Template
===================

#. Log in to the management console.

#. In the upper left corner of the page, click |image1|, and then click **Management & Deployment** > **Resource Formation Service**.

   The \ **Dashboard**\  page is displayed.


   .. figure:: /_static/images/en-us_image_0000002121900840.png
      :alt: **Figure 1** RFS Dashboard

      **Figure 1** RFS Dashboard

#. In the left navigation pane, choose \ **Templates**\  -> **Private Templates**\ .


   .. figure:: /_static/images/en-us_image_0000002158823486.png
      :alt: **Figure 2** RFS Private Templates

      **Figure 2** RFS Private Templates

#. On the \ **Private Templates**\  page, click \ **Create Template**\  in the upper right corner.


   **Figure 3** Creating a template

   |image2|

5. On the **Create Template** page, select the **Source**:

   a. **URL**\ : Enter a URL of an OBS template. When the OBS URL is correct, the corresponding template content from OBS will be displayed in the content section below. (The URL must contain at least the deployment code file or zip, and the file size cannot exceed 1 MB.)


      .. figure:: /_static/images/en-us_image_0000002158820394.png
         :alt: **Figure 4** Template URL

         **Figure 4** Template URL

   b. **Upload Template**: Upload a local template file or zip. After your upload, the corresponding template content will be displayed in the content section below. (The files in the format of .tf, .tf.json, and .zip are supported. At least the deployment code file needs to be uploaded. The size of a file cannot exceed 50 KB. The size of a decompressed .zip file cannot exceed 1 MB.)


      .. figure:: /_static/images/en-us_image_0000002194187417.png
         :alt: **Figure 5** Upload template

         **Figure 5** Upload template

   c. **Input Template**: Input template. You can create, rename, and delete files and folders here, which helps in organizing the template file structure better, and you can also export the templates.


      .. figure:: /_static/images/en-us_image_0000002157144325.png
         :alt: **Figure 6** Input template

         **Figure 6** Input template

6. Next, you can modify the template name, description and version description, as shown in :ref:`Figure 7 <en-us_topic_0000002046740822__fig197685819172>`.

   .. _en-us_topic_0000002046740822__fig197685819172:

   **Figure 7** Configuring parameters

   |image3|

   .. note::

      -  The template name must start with a letter and can contain a maximum of 128 characters, including letters, digits, underscores (_), and hyphens (-). The name must be unique.
      -  The template name cannot be changed after the template is created.
      -  A template description can contain a maximum of 1024 characters.
      -  A template version description can contain a maximum of 1024 characters.

7. Click **Create Now** to create a template.


   .. figure:: /_static/images/en-us_image_0000002158823498.png
      :alt: **Figure 8** Template list

      **Figure 8** Template list

.. |image1| image:: /_static/images/en-us_image_0000002194220973.png
.. |image2| image:: /_static/images/en-us_image_0000002157056257.png
.. |image3| image:: /_static/images/en-us_image_0000002121739696.png
