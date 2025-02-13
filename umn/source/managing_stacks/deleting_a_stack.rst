:original_name: en-us_topic_0000001991890809.html

.. _en-us_topic_0000001991890809:

Deleting a Stack
================

If a stack is no longer needed, you can perform the following steps to delete it:

#. Log in to the management console.

#. In the upper left corner of the page, click |image1|, and then click **Management & Deployment** > **Resource Formation Service**.

   The \ **Dashboard**\  page is displayed.


   .. figure:: /_static/images/en-us_image_0000002157142509.png
      :alt: **Figure 1** RFS Dashboard

      **Figure 1** RFS Dashboard

#. In the left navigation pane, choose **Stacks**.


   .. figure:: /_static/images/en-us_image_0000002121742716.png
      :alt: **Figure 2** RFS Stacks

      **Figure 2** RFS Stacks

4. (Optional) Check whether the deletion protection is enabled for the stack.

   Those stacks, where the deletion protection is enabled, cannot be deleted. If you attempt to delete such stack, an error message will be displayed, as shown in :ref:`Figure Deletion failed <en-us_topic_0000001991890809____d0e1513>`.

   .. _en-us_topic_0000001991890809____d0e1513:

   .. figure:: /_static/images/en-us_image_0000002121667372.png
      :alt: **Figure 3** Deletion failed

      **Figure 3** Deletion failed

   a. Click the name of the desired stack to view its details and check the **Deletion Protection** value in the **Basic Information** tab.


   .. figure:: /_static/images/en-us_image_0000002156909017.png
      :alt: **Figure 4** Deletion protection

      **Figure 4** Deletion protection

   b. If it is enabled, click **Edit** in the top right corner of the **Basic Information** tab, disable the deletion protection and click **Save** in the top right corner of the **Basic Information** tab.


   .. figure:: /_static/images/en-us_image_0000002121663600.png
      :alt: **Figure 5** Edit basic information

      **Figure 5** Edit basic information

5. On the stack list page, locate the stack to be deleted and click **Delete** in the **Operation** column.

   Alternatively, go to the stack details page by clicking the name of the stack and click **Delete** in the upper right corner

6. In the dialog box displayed, as shown in \ :ref:`Figure Dialog box for deleting a stack <en-us_topic_0000001991890809__fig172072292519>`,

   a. select the desired deletion option:

      If you choose to delete resources, RFS will destroy all the resources in the stack. If you choose to retain resources, we will only delete the stack without destroying the resources. Therefore, these resources will no longer be managed by RFS.

   b. and confirm the deletion by entering **Delete** in the text box and click **OK**.

      .. _en-us_topic_0000001991890809__fig172072292519:

      .. figure:: /_static/images/en-us_image_0000002166698096.png
         :alt: **Figure 6** Dialog box for deleting a stack

         **Figure 6** Dialog box for deleting a stack

.. warning::

   Stacks cannot be restored after being deleted. Exercise caution when performing this operation.

.. |image1| image:: /_static/images/en-us_image_0000002158817102.png
