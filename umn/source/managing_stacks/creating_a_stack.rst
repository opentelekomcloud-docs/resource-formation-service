:original_name: en-us_topic_0000001955571466.html

.. _en-us_topic_0000001955571466:

Creating a Stack
================

#. Log in to the management console.

#. In the upper left corner of the page, click |image1|, and then click **Management & Deployment** > **Resource Formation Service**\ .

   The **Dashboard** page is displayed.


   .. figure:: /_static/images/en-us_image_0000002160009781.png
      :alt: **Figure 1** RFS Dashboard

      **Figure 1** RFS Dashboard

#. There are several ways to start creating a stack

   a. On the **Dashboard** page:

      -  click **Create Stack** in the upper right corner.
      -  click **Create Stack** in the **Select Template** tile of the **Guide to Create a Stack** flow chart.

   b. On the **Stacks** page, click **Create Stack** in the upper right corner.


      **Figure 2** Creating a stack on Stacks page

      |image2|

   c. On the **Templates** -> **Private Templates** page:

      -  click **Create Stack** under the **Operation** column associated with an existing template.


         .. figure:: /_static/images/en-us_image_0000002194226997.png
            :alt: **Figure 3** Creating a stack on Private Templates page

            **Figure 3** Creating a stack on Private Templates page

      -  click the name of the desired template to navigate to its details page, and then click **Create Stack** under the **Operation** column associated with a specific template version.


         .. figure:: /_static/images/en-us_image_0000002194091653.png
            :alt: **Figure 4** Creating a stack on Template Details page

            **Figure 4** Creating a stack on Template Details page

4. .. _en-us_topic_0000001955571466__li7334814113611:

   There are three ways to select a template.


   .. figure:: /_static/images/en-us_image_0000002194180509.png
      :alt: **Figure 5** Selecting a template

      **Figure 5** Selecting a template

   a. Select a template from **Private Templates**: Template name and version selector dropdowns.

   b. Enter a URL of an OBS template: Template URL dropdown. (The URL must contain at least the deployment code file, and the file size cannot exceed 1 MB.)

      Example: https://test-stack-template.obs.eu-de.otc.t-systems.com/main.tf

   c. Upload a local template file or zip by clicking **Add File**\  button.

      .. important::

         -  The .tf, .tf.json, and .zip files are supported.
         -  At least the deployment code file needs to be uploaded.
         -  The size of a file cannot exceed 50 KB.
         -  The size of a decompressed .zip file cannot exceed 1 MB.

   Then click **Next** to go to the parameter configuration page.

   .. caution::

      -  A stack is created using a template. The template must contain the deployment code file which file name extension is tf or tf.json.
      -  The deployment code file must use the open source HCL syntax. After the file is imported, the corresponding resource configuration table is generated for users to configure resource parameters. This file must be provided in URL or via template upload.
      -  When using the RFS service, users do not need to specify the "access_key" and "secret_key" fields under the **provider block** in the template.
      -  RFS only uses the data you upload for resource management.

   The following is an example of uploading a local template file. In this example, the **ecs_test.tf.json** file is uploaded. The template content is as follows:

   .. code-block::

      {
          "terraform": {
              "required_providers": {
                  "opentelekomcloud": {
                      "source": "opentelekomcloud/provider/opentelekomcloud",
                      "version": "1.35.13"
                   }
              }
          },
          "provider": {
              "opentelekomcloud": {
                  "region": "eu-de",
                  "insecure": true,
                  "auth_url": "https://iam.eu-de.otc.t-systems.com/v3",
                  "tenant_name": "eu-de",
                  "domain_name": "OTC-EU-DE-xxxxxxxxxxxxxxxxxxxx",
                  "user_name": "xxxxxxxxxx"
              }
          },
          "variable": {
              "vpc_name": {
                  "type": "string",
                  "description": "vpc name",
                  "default": "rf_test_stack_example_vpc",
                  "sensitive": true,
                  "nullable": false
              },
              "subnet_name": {
                  "type": "string",
                  "description": "subnet name",
                  "default": "rf_test_stack_example_subnet"
              },
              "ecs_name": {
                  "type": "string",
                  "description": "ecs name",
                  "default": "rf_test_stack_example_ecs"
              },
              "compute_keypair_name": {
                  "type": "string",
                  "description": "ecs compute key pair name",
                  "default": "rf_test_stack_example_keypair"
              },
              "storage_volume_name": {
                  "type": "string",
                  "description": "storage volume name",
                  "default": "rf_test_stack_example_volume"
              }
          },
          "resource": {
              "opentelekomcloud_vpc_v1": {
                  "rf_doc_vpc": {
                      "name": "${var.vpc_name}",
                      "cidr": "192.168.0.0/16"
                  }
              },
              "opentelekomcloud_vpc_subnet_v1": {
                  "rf_doc_subnet": {
                      "name": "${var.subnet_name}",
                      "vpc_id": "${opentelekomcloud_vpc_v1.rf_doc_vpc.id}",
                      "cidr": "192.168.1.0/24",
                      "gateway_ip": "192.168.1.1"
                  }
              },
              "opentelekomcloud_compute_keypair_v2": {
                  "rf_doc_keypair": {
                      "name": "${var.compute_keypair_name}"
                  }
              },
              "opentelekomcloud_compute_instance_v2": {
                  "rf_doc_ecs": {
                      "name": "${var.ecs_name}",
                      "flavor_id": "s2.large.1",
                      "image_id": "bf0f71bd-f08a-4cd0-9594-ca2caa00b9d7",
                      "availability_zone": "eu-de-01",
                      "key_pair": "${opentelekomcloud_compute_keypair_v2.rf_doc_keypair.name}",
                      "security_groups": ["default"],
                      "network": {
                          "uuid": "${opentelekomcloud_vpc_subnet_v1.rf_doc_subnet.id}"
                      }
                  }
              },
              "opentelekomcloud_blockstorage_volume_v2": {
                  "rf_doc_volume": {
                      "name": "${var.storage_volume_name}",
                      "size": 4,
                      "availability_zone": "eu-de-01"
                  }
              },
              "opentelekomcloud_compute_volume_attach_v2": {
                  "rf_doc_volume_attach": {
                      "instance_id": "${opentelekomcloud_compute_instance_v2.rf_doc_ecs.id}",
                      "volume_id": "${opentelekomcloud_blockstorage_volume_v2.rf_doc_volume.id}"
                  }
              }
          },
          "output": {
              "ecs_address": {
                  "value": "${opentelekomcloud_compute_instance_v2.rf_doc_ecs.access_ip_v4}",
                  "description": "The ecs private address."
              },
              "ecs_id": {
                  "value": "${opentelekomcloud_compute_instance_v2.rf_doc_ecs.id}",
                  "description": "The ecs resource id."
              }
          }
      }

   .. caution::

      The sample template contains charged resources. Check whether resources need to be enabled before using the template.

   The template consists of eight parts:

   -  **opentelekomcloud_vpc_v1** in **resource** indicates VPC information.
   -  **opentelekomcloud_vpc_subnet_v1** in **resource** indicates information about a subnet defined in the VPC.
   -  **opentelekomcloud_compute_keypair_v2** in **resource** indicates information about compute keypair defined in the template.
   -  **opentelekomcloud_compute_instance_v2** in **resource** indicates information about an ECS defined in the template.
   -  **opentelekomcloud_blockstorage_volume_v2** in **resource** indicates information about an EVS storage volume defined in the template.
   -  **opentelekomcloud_compute_volume_attach_v2** in **resource** indicates the binding relationship between EVS storage volume and ECS.
   -  **variable** indicates variables defined by users in templates during stack creation and deployment.
   -  **output** defines the outputs of templates. After a stack is created, its output is generated based on the definition and displayed on the :ref:`Outputs <en-us_topic_0000001991770629__li167036103014>` tab page.

   For detailed usage of other resources, please refer to `OpenTelekom Cloud Provider <https://registry.terraform.io/providers/opentelekomcloud/opentelekomcloud/latest/docs>`__.

5. .. _en-us_topic_0000001955571466__li43272049164914:

   Configure parameters

   On the parameter configuration page, you can modify the stack name and description and configure the template parameters.

   .. caution::

      The stack name must start with a letter and can contain a maximum of 128 characters, including letters, digits, underscores (_), and hyphens (-). The name must be unique.

      A stack description can contain a maximum of 255 characters.


   .. figure:: /_static/images/en-us_image_0000002120705156.png
      :alt: **Figure 6** Configuring parameters

      **Figure 6** Configuring parameters

   Parameters whose **nullable** field is set to **false** in template are marked with a red asterisk (``*``) as mandatory. Valid values must be set to these parameters.

   If there are variables whose **sensitive** field is set to **true** in template, KMS encryption can be selected, as shown in :ref:`Figure Encrypt requirements <en-us_topic_0000001955571466__fig15774183016141>`. If encryption is enabled, RFS will use KMS to encrypt those senstitive parameters to ensure their secure transmission and storage.

   .. _en-us_topic_0000001955571466__fig15774183016141:

   .. figure:: /_static/images/en-us_image_0000002156056533.png
      :alt: **Figure 7** Encrypt requirements

      **Figure 7** Encrypt requirements

   If a value is invalid, the corresponding text box will turn red (as shown in :ref:`Figure 8 <en-us_topic_0000001955571466____d0e644>`) and page redirection will not be triggered after you click **Next**.

   .. _en-us_topic_0000001955571466____d0e644:

   .. figure:: /_static/images/en-us_image_0000001991770641.png
      :alt: **Figure 8** Text box with an invalid value

      **Figure 8** Text box with an invalid value

   Check whether the default VPC, subnet, and ECS names used on this page already exist on the corresponding consoles. If the names already exist, change them to unique ones to prevent creation failures.

   Then click **Next** and the **Configure Stack** page is displayed.

6. .. _en-us_topic_0000001955571466__li459mcpsimp:

   Configure the stack.


   .. figure:: /_static/images/en-us_image_0000002158816238.png
      :alt: **Figure 9** Configuring the stack

      **Figure 9** Configuring the stack

   **IAM Agency (Optional)**: An agency can clearly define operation permissions of RFS (such as creation, update, and deletion) on stack resources. If the agency permissions are insufficient, subsequent operations may fail. For more details of how to create agency, see :ref:`create an agency <en-us_topic_0000001991890817>`.

   **Deletion Protection**: prevents the stack from being deleted accidentally. After a stack is created, You can modify it on the stack details page.

   **Auto-Rollback**: If auto-rollback is enabled, the stack automatically rolls back to the previous successful resource status when an operation fails.

   After the stack is created, you can modify the stack configurations on its details page, see \ :ref:`Modifying the basic parameters of a Stack <en-us_topic_0000002154604281>`.

   Click **Next** to go to the **Confirm Configurations** page.


   .. figure:: /_static/images/en-us_image_0000002158975806.png
      :alt: **Figure 10** Confirm Configurations

      **Figure 10** Confirm Configurations

7. .. _en-us_topic_0000001955571466__li7775101171312:

   Check the configuration and make sure everything is set correctly.

   After you confirm the configurations, you can click either **Create Execution Plan** or **Directly Deploy Stack**.

   -  If you click **Directly Deploy Stack**, a :ref:`confirmation dialog box <en-us_topic_0000001955571466__fig38972020557>` will be displayed.

      .. _en-us_topic_0000001955571466__fig38972020557:

      .. figure:: /_static/images/en-us_image_0000002156063229.png
         :alt: **Figure 11** Directly deploy stack

         **Figure 11** Directly deploy stack

      a. Click **Yes**. A new stack is generated and its status is **Deployment In Progress**, as shown in :ref:`Figure 12 <en-us_topic_0000001955571466____d0e756>`. And it will redirect to the stack events page, as shown in :ref:`Figure Stack Events <en-us_topic_0000001955571466__fig173401257402>`.

         .. _en-us_topic_0000001955571466____d0e756:

         **Figure 12** Deployment in progress

         |image3|

         .. _en-us_topic_0000001955571466__fig173401257402:

         .. figure:: /_static/images/en-us_image_0000002120746402.png
            :alt: **Figure 13** Stack Events

            **Figure 13** Stack Events

      b. If everything goes well, the status will change to **Deployment Complete**, as shown in :ref:`Figure Deployment complete <en-us_topic_0000001955571466__fig73237820229>`.

         .. _en-us_topic_0000001955571466__fig73237820229:

         **Figure 14** Deployment complete

         |image4|

   -  If you click **Create Execution Plan**, a dialog box of creating execution plan will be displayed. In this dialog box, you can set the name and description of the execution plan.


      .. figure:: /_static/images/en-us_image_0000002158816218.png
         :alt: **Figure 15** Create Execution Plan dialog box

         **Figure 15** Create Execution Plan dialog box

      .. caution::

         The execution plan name must start with a letter and can contain a maximum of 128 characters, including only letters, digits, underscores (_), and hyphens (-).

      a. Click **OK**. The **Execution Plans** tab page is displayed.

      b. Wait until the execution plan is created and refresh the page. The execution plan status will change to **Available**, as shown in :ref:`Figure Execution Plan Available <en-us_topic_0000001955571466__fig432318842212>`.

         .. _en-us_topic_0000001955571466__fig432318842212:

         **Figure 16** Execution Plan Available

         |image5|

      c. Return to the stack list page. A stack is generated and its stack status is **Creation Complete**, as shown in :ref:`Figure 17 <en-us_topic_0000001955571466____d0e813>`.

         .. _en-us_topic_0000001955571466____d0e813:

         **Figure 17** Stack list

         |image6|

         .. caution::

            **Creating an execution plan** can preview the resource attribute changes of the entire stack and evaluate the impact. If the execution plan meets your expectations, you can execute the plan. Creating an execution plan does not incur fees. The system changes your stack only when you execute the plan.

      d. Go back to the **Execution Plans** tab page of the stack and click **Deploy** in the **Operation** column of the execution plan to deploy it, as shown in :ref:`Figure 18 <en-us_topic_0000001955571466____d0e835>`.

         .. _en-us_topic_0000001955571466____d0e835:

         .. figure:: /_static/images/en-us_image_0000002120743398.png
            :alt: **Figure 18** Execution plan dialog box

            **Figure 18** Execution plan dialog box

         #. In the **Execution Plan** dialog box, click **Execute**. A message indicating that the execution plan is being deployed is displayed in the upper right corner. Return to the stack list page. The stack status is **Deployment In Progress**, as shown in :ref:`Figure Deployment in progress <en-us_topic_0000001955571466__fig65231214111516>`.

            .. _en-us_topic_0000001955571466__fig65231214111516:

            .. figure:: /_static/images/en-us_image_0000002156141613.png
               :alt: **Figure 19** Deployment in progress

               **Figure 19** Deployment in progress

         #. Then, the stack status changes to **Deployment Complete**, as shown in :ref:`Figure 20 <en-us_topic_0000001955571466____d0e866>`.

            .. _en-us_topic_0000001955571466____d0e866:

            **Figure 20** Deployment complete

            |image7|

      e. On the **Execution Plans** tab page of the stack details page, the execution plan status is **Applied**, as shown in :ref:`Figure 21 <en-us_topic_0000001955571466____d0e882>`.

         .. _en-us_topic_0000001955571466____d0e882:

         .. figure:: /_static/images/en-us_image_0000002120901494.png
            :alt: **Figure 21** Applied

            **Figure 21** Applied

8. Click the **Resources** tab. The resource list shows that resources of the stack are deployed, as shown in :ref:`Figure 22 <en-us_topic_0000001955571466____d0e895>`.

   .. _en-us_topic_0000001955571466____d0e895:

   **Figure 22** Resources deployed

   |image8|

   You can view additional details on the console of the corresponding cloud service. (:ref:`Figure ECS <en-us_topic_0000001955571466__fig1268133163913>`\  shows the deployed resources on the ECS console for the above example).

   .. _en-us_topic_0000001955571466__fig1268133163913:

   .. figure:: /_static/images/en-us_image_0000002120901474.png
      :alt: **Figure 23** ECS

      **Figure 23** ECS

.. |image1| image:: /_static/images/en-us_image_0000002194091645.png
.. |image2| image:: /_static/images/en-us_image_0000002158650788.png
.. |image3| image:: /_static/images/en-us_image_0000002120901486.png
.. |image4| image:: /_static/images/en-us_image_0000002120743394.png
.. |image5| image:: /_static/images/en-us_image_0000002156064705.png
.. |image6| image:: /_static/images/en-us_image_0000002158975566.png
.. |image7| image:: /_static/images/en-us_image_0000002156063237.png
.. |image8| image:: /_static/images/en-us_image_0000002120743374.png
