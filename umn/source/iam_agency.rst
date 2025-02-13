:original_name: en-us_topic_0000001991890817.html

.. _en-us_topic_0000001991890817:

IAM Agency
==========

By creating an agency, you can share your resources with another account, or delegate an individual or team to manage your resources. You do not need to share your security credentials (the password and access keys) with the delegated party. Instead, the delegated party can log in with its own account credentials and then switches the role to your account and manage your resources.

With RFS, you can create a stack to bind an agency with a provider and update the binding relationship by updating the stack.

RFS uses an agency only in resource operation requests, such as creating a stack (triggering deployment), creating an execution plan, deploying a stack, and deleting a stack. The agency applies only to resource operations performed by the bound provider. If the permissions provided by the agency are insufficient, resource operations may fail.

**Procedure**

#. Log in to the IAM console.
#. On the IAM console, choose **Agencies** from the navigation pane on the left, and click **Create Agency** in the upper right corner.


.. figure:: /_static/images/en-us_image_0000001955571530.png
   :alt: **Figure 1** Creating an agency

   **Figure 1** Creating an agency

3. Enter an agency name,

   -  the \ **Agency Type**\  is set to \ **Cloud Service**

   -  the **Cloud Service** is set to **RFS**.


      .. figure:: /_static/images/en-us_image_0000002202025297.png
         :alt: **Figure 2** Create an agency

         **Figure 2** Create an agency

.. caution::

   The agency name is user-defined.

   If **op_svc_iac** has been used for registration, you are advised to change it to **RFS**.

4. Click **Next**. The **Authorize Agency** page is displayed. You can grant permissions to the agency on this page. Filter specific permissions and grant them to the agency.


.. figure:: /_static/images/en-us_image_0000001955571534.png
   :alt: **Figure 3** Selecting policies and roles

   **Figure 3** Selecting policies and roles

You can determine the permissions to be granted to an agency. OpenTelekom cloud best practices do not advise you to automatically create agencies with the Tenant Administrator permission for users. The best practice is to grant management permissions (including read and write operations) to resources that may be used in a stack.

5. Set the authorization scope. You can select **All resources** or **Region-specific projects**.


.. figure:: /_static/images/en-us_image_0000001991890873.png
   :alt: **Figure 4** Authorization scope

   **Figure 4** Authorization scope

6. Click **OK**. The agency is created. Now you can use it in \ :ref:`Configure the stack. <en-us_topic_0000001955571466__li459mcpsimp>`

   |image1|\ For more information about IAM Agencies, see: `Cloud Service Agency <https://docs.otc.t-systems.com/identity-access-management/umn/user_guide/agencies/cloud_service_agency.html#iam-06-0004>`__.

.. |image1| image:: /_static/images/en-us_image_0000001991770693.png
