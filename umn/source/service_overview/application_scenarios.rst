:original_name: en-us_topic_0000002154657153.html

.. _en-us_topic_0000002154657153:

Application Scenarios
=====================

Migrating Applications to the Cloud
-----------------------------------

**Description**

Migrating applications to the cloud involves repetitive manual work, such as the destruction and rebuild of environments and configuring new instances one by one when scaling out applications. These manual operations are error-prone.

Some operations, such as creating databases or VMs, could be time-consuming. You may have to wait for a long time when these demanding operations need to be performed one by one.

**Solution**

RFS implements tool-based and process-based work for the preceding scenarios. It uses templates to describe resources required by applications in a unified manner. The stack management function enables automatic deployment or destruction for various resources. RFS allows you to define a large number of resource instances of different services and specifications in a template. You can also use RFS to realize automatic creation, quick deployment, and flexible configuration of resources.

**Advantages**

-  **Easy to use**

   Design your applications and schedule resources by writing templates. Organize and manage the service easily and efficiently.

-  **Highly efficient**

   Automatically deploy or delete a template with a wizard to reduce repetitive work and manual misoperations.

-  **Quick replication of applications**

   Replicate a template to automatically deploy the same applications and resources to different data centers, improving efficiency.


**Figure 1** Migrating applications to the cloud

|image1|

ISV Resource Provisioning
-------------------------

**Description**

Independent software vendors (ISVs) need to deploy resources required by software on the cloud for their customers to use. The traditional delivery method is that ISVs provide the software code and platform building guides on their official websites for customers to download. This could be time demanding and costly, because ISVs have to configure networks, deliver resources, and deploy software all on themselves.

**Solution**

RFS enables ISVs to deliver software and required resources in a standard manner. ISVs can convert software services to templates. The stack deployment capability of RFS enables quick service provisioning and streamlines the delivery process. RFS uses a code template to describe the entire delivery environment, facilitating ISVs to integrate delivery with the CI/CD process.

**Advantages**

-  **Standardized delivery**

   Templates and stacks standardize software delivery processes, which can be summarized into best practices for wider use.

-  **Better efficiency**

   Templates are used to automatically provision resources. ISVs only need to deploy stacks to complete service delivery, improving delivery efficiency.

-  **Error-proof creation**

   ISV software and resources required for the software are defined in a template to prevent mistakes introduced through manual work.

-  **CI/CD integration**

   RFS can be integrated into the existing tool chain to improve automation.


**Figure 2** ISV resource provisioning scenario

|image2|

.. |image1| image:: /_static/images/en-us_image_0000002119222466.png
.. |image2| image:: /_static/images/en-us_image_0000002119380574.png
