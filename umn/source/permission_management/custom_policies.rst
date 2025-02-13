:original_name: en-us_topic_0000002158636644.html

.. _en-us_topic_0000002158636644:

Custom Policies
===============

The following lists examples of custom policies for RFS.

**Example Custom Policies**

-  Example 1: Granting permission to view stacks

   .. code-block::

      {
          "Version": "1.1",
          "Statement": [
              {
                  "Effect": "Allow",
                  "Action": [
                      "rf:stack:listStacks"
                  ]
              }
          ]
      }

-  Example 2: Granting permission to deny stack deletion

   “Deny” permissions should be used together with “Allow” permissions. If “Deny” and “Allow” permissions are both assigned, the “Deny” permissions take precedence over the “Allow” permissions.

   Assume that you want to grant the **RF FullAccess** permissions to users but do not want them to delete stacks. You can create a custom policy for denying stack deletion, and attach this policy together with the **RF FullAccess** policy to the users. As an explicit deny in any policy overrides any allows, the users can perform all operations on stacks except deleting them. The following shows an example policy for denying stack deletion.

   .. code-block::

      {
          "Version": "1.1",
          "Statement": [
              {
                  "Effect": "Deny",
                  "Action": [
                      "rf:stack:deleteStack"
                  ]
              }
          ]
      }

-  Example 3: Creating a custom policy containing multiple actions.

   A custom policy can contain actions of one or more services. To grant permissions of multiple services in a policy, ensure that the services are all of the same level (global or project).

   The following shows an example policy that contains multiple actions.

   .. code-block::

      {
          "Version": "1.1",
          "Statement": [
              {
                  "Effect": "Allow",
                  "Action": [
                      "rf:stack:updateStack",
                      "rf:stack:createStack",
                      "rf:stack:deployStack",
                      "rf:stack:deleteStack",
                      "rf:stack:listStacks"
                  ]
              },
              {
                  "Effect": "Allow",
                  "Action": [
                      "kms:dek:create",
                      "kms:cmk:list"
                  ]
              }
          ]
      }
