:original_name: en-us_topic_0000002158796408.html

.. _en-us_topic_0000002158796408:

Creating a User and Granting Permissions
========================================

This section describes how to use IAM to implement fine-grained permissions control for RF service. With IAM, you can:

-  Create IAM users for employees based on your organizational structure. Each IAM user has their own security credentials for accessing RF service.
-  Granting users only the permissions required to perform a given task based on their job responsibilities.
-  Entrust an account or a cloud service to perform operations for your RF service.

If your account does not need indivitual IAM users, skip this section.

:ref:`Figure 1 <en-us_topic_0000002158796408__fig14490220011>` shows the process flow for granting permissions.

**Prerequisites**

Before granting permissions, learn about the RFS permissions and select the permissions as required. For details about the system-defined permissions supported by RFS, see :ref:`RFS Permissions <en-us_topic_0000002154657157>`. To grant permissions for other services, you can see `permissions <https://docs.otc.t-systems.com/identity-access-management/permissions/permissions.html>`__.

**Flowchart**

.. _en-us_topic_0000002158796408__fig14490220011:

.. figure:: /_static/images/en-us_image_0000002159668284.png
   :alt: **Figure 1** Granting RFS permissions

   **Figure 1** Granting RFS permissions

#. On the IAM console, `create a user group and assigning permissions <https://docs.otc.t-systems.com/usermanual/iam/iam_01_0030.html>`__. Here, **RFS ReadOnlyAccess** permissions are used as an example.

#. `Create an IAM user and add it to the created user group <https://docs.otc.t-systems.com/usermanual/iam/iam_01_0031.html>`__.

#. `Log in <https://docs.otc.t-systems.com/usermanual/iam/iam_01_0032.html>`__ and verify permissions.

   The created user logs in to the console and verifies permissions as described below:

   -  Choose **Service List** > **Resource Formation Service**. In the navigation pane on the left, click on **Stacks**. If you can view the stack list successfully, the RFS ReadOnlyAccess policy is in effect. If you click on **Create Stack** in the upper right corner of the displayed page, you should receive a notification message indicating your insufficient permissions.
   -  Choose another service from **Service List**. If a message appears indicating that you have insufficient permissions to access the service, it also reflects the **RFS ReadOnlyAccess** policy.
