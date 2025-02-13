:original_name: en-us_topic_0000002121421892.html

.. _en-us_topic_0000002121421892:

Deploying an Execution Plan
===========================

#. Log in to the management console.

#. In the upper left corner of the page, click |image1|, and then click **Management & Deployment** > **Resource Formation Service**.

   The \ **Dashboard**\  page is displayed.


   .. figure:: /_static/images/en-us_image_0000002159891453.png
      :alt: **Figure 1** RFS Dashboard

      **Figure 1** RFS Dashboard

#. In the left navigation pane, choose **Stacks**.


   .. figure:: /_static/images/en-us_image_0000002124611734.png
      :alt: **Figure 2** RFS Stacks

      **Figure 2** RFS Stacks

#. Click the name of the desired stack and navigate to the **Execution Plans** tab.


   **Figure 3** Execution plan list

   |image2|

#. Locate the row that contains the desired execution plan and click **Deploy** in the **Operation** column. Alternatively, you can click the name of the desired execution plan to navigate to its details page and then click **Deploy** in the **Basic Information** section.

   After an execution plan is executed, its status changes from Available to Applied and the Deploy options will no longer be available for the plan.

.. caution::

   -  Execution plan can only be deployed once. However, if it fails, it is allowed to retry the deployment on the Stack List page by clicking on the \ **Continue Deployment**\  link under the \ **Operation**\  column.
   -  If there are multiple execution plans in the available state, deploying one of them will cause the other execution plans to expire, even though they remain in the available state.

.. |image1| image:: /_static/images/en-us_image_0000002194218013.png
.. |image2| image:: /_static/images/en-us_image_0000002124769898.png
