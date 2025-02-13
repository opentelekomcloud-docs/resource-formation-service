:original_name: en-us_topic_0000001991770629.html

.. _en-us_topic_0000001991770629:

Viewing Stack Details
=====================

To navigate the details page of a stack, perform the following steps:

#. Log in to the management console.

#. In the upper left corner of the page, click |image1|, and then click **Management & Deployment** > **Resource Formation Service**.

   The \ **Dashboard**\  page is displayed.


   .. figure:: /_static/images/en-us_image_0000002121673112.png
      :alt: **Figure 1** RFS Dashboard

      **Figure 1** RFS Dashboard

#. In the left navigation pane, choose **Stacks**.


   .. figure:: /_static/images/en-us_image_0000002156993381.png
      :alt: **Figure 2** RFS Stacks

      **Figure 2** RFS Stacks

#. Click the name of the desired stack to view its details and select the tab needed.

Function modules on the stack details page
------------------------------------------

#. **Basic Information**: displays basic information about the stack, such as \ **Stack Name**\ , \ **Stack ID**\ , \ **Status**\ , \ **Auto-Rollback**\  and \ **Deletion Protection**\  settings, etc, as shown in :ref:`Figure 3 <en-us_topic_0000001991770629____d0e1560>`.

   .. _en-us_topic_0000001991770629____d0e1560:

   **Figure 3** Basic information

   |image2|

#. **Resources**: displays the elements of the stack, such as applications, cloud services or resources generated during deployment, as shown in :ref:`Figure 4 <en-us_topic_0000001991770629____d0e1571>`.

   .. _en-us_topic_0000001991770629____d0e1571:

   **Figure 4** Resources

   |image3|

#. .. _en-us_topic_0000001991770629__li167036103014:

   **Outputs**: displays the output parameters and their values defined in the stack template, as shown in :ref:`Figure 5 <en-us_topic_0000001991770629____d0e1595>`.

   .. _en-us_topic_0000001991770629____d0e1595:

   **Figure 5** Outputs

   |image4|

#. **Events**: displays log information about stack events (for example stack creation, or deployment related events), so that you can monitor the stack operation progress. The events are sorted in chronological order with the latest event being displayed at the top.

   For example, :ref:`Figure 6 <en-us_topic_0000001991770629____d0e1583>` shows the creation process of each resource.

   You can filter events by resource name or resource type in the top-right corner, as shown in :ref:`Figure Filter Events <en-us_topic_0000001991770629__fig1958919547213>`.

   .. _en-us_topic_0000001991770629____d0e1583:

   **Figure 6** Events

   |image5|

   .. _en-us_topic_0000001991770629__fig1958919547213:

   .. figure:: /_static/images/en-us_image_0000002121519232.png
      :alt: **Figure 7** Filter Events

      **Figure 7** Filter Events

#. **Template**: displays the latest template content, what has been deployed with the stack, as shown in :ref:`Figure 8 <en-us_topic_0000001991770629____d0e1606>`.

   .. _en-us_topic_0000001991770629____d0e1606:

   **Figure 8** Template

   |image6|

#. **Execution Plans**: displays the different execution plans associated with the stack, as shown in :ref:`Figure 9 <en-us_topic_0000001991770629____d0e1629>`. To see how to deploy or delete an execution plan, check :ref:`Creating, Deploying and Deleting an Execution Plan <en-us_topic_0000001955571470>`.

   .. _en-us_topic_0000001991770629____d0e1629:

   **Figure 9** Execution plans

   |image7|

   You can filter execution plans by execution plans name in the top-right corner, as shown in :ref:`Figure Filter Execution plans <en-us_topic_0000001991770629__fig17920107173512>`.

   .. _en-us_topic_0000001991770629__fig17920107173512:

   .. figure:: /_static/images/en-us_image_0000002121681612.png
      :alt: **Figure 10** Filter Execution plans

      **Figure 10** Filter Execution plans

   :ref:`Table 1 <en-us_topic_0000001991770629____d0e458>` describes the possible execution plan statuses.

   .. _en-us_topic_0000001991770629____d0e458:

   .. table:: **Table 1** Execution plan statuses

      +----------------------+-------------------------------------------------------------+
      | Status               | Description                                                 |
      +======================+=============================================================+
      | Creation In Progress | Execution plan creation is in progress.                     |
      +----------------------+-------------------------------------------------------------+
      | Creation Failed      | Execution plan creation failed.                             |
      +----------------------+-------------------------------------------------------------+
      | Available            | The execution plan is created and ready for the deployment. |
      +----------------------+-------------------------------------------------------------+
      | Applied              | The execution plan has been applied.                        |
      +----------------------+-------------------------------------------------------------+

   To check the details of an execution plan, you can click the execution plan name to open its details, as shown in :ref:`Figure 11 <en-us_topic_0000001991770629____d0e1639>`.

   .. _en-us_topic_0000001991770629____d0e1639:

   **Figure 11** Execution plan details

   |image8|

.. |image1| image:: /_static/images/en-us_image_0000002158817114.png
.. |image2| image:: /_static/images/en-us_image_0000002120707020.png
.. |image3| image:: /_static/images/en-us_image_0000002155947169.png
.. |image4| image:: /_static/images/en-us_image_0000002120549060.png
.. |image5| image:: /_static/images/en-us_image_0000002155947473.png
.. |image6| image:: /_static/images/en-us_image_0000002156029369.png
.. |image7| image:: /_static/images/en-us_image_0000002155948217.png
.. |image8| image:: /_static/images/en-us_image_0000002121525200.png
