:original_name: en-us_topic_0000002154653061.html

.. _en-us_topic_0000002154653061:

Auditing
========

Scenario
--------

Cloud Trace Service (CTS) records all operations performed on cloud services, providing data support for customers in fault locating, resource management, and security auditing. When you enable CTS, it begins to record operations performed on RFS resource

Prerequisites
-------------

You have enabled CTS.

Supported RFS Operations
------------------------

.. table:: **Table 1** RFS operations supported by CTS

   +------------------------+---------------+-------------------------------------------------------+
   | Trace Name             | Resource Type | Operation                                             |
   +========================+===============+=======================================================+
   | createStack            | stack         | Creating a stack                                      |
   +------------------------+---------------+-------------------------------------------------------+
   | deployStack            | stack         | Deploying a stack directly                            |
   +------------------------+---------------+-------------------------------------------------------+
   | deleteStack            | stack         | Deleting a stack started                              |
   +------------------------+---------------+-------------------------------------------------------+
   | deleteStackEnd         | stack         | Deleting a stack finished                             |
   +------------------------+---------------+-------------------------------------------------------+
   | updateStack            | stack         | Updating a stack                                      |
   +------------------------+---------------+-------------------------------------------------------+
   | continueRollbackStack  | stack         | Retrying a failed rollback. Available only via API.   |
   +------------------------+---------------+-------------------------------------------------------+
   | continueDeployStack    | stack         | Retrying a failed deployment. Available only via API. |
   +------------------------+---------------+-------------------------------------------------------+
   | createExecutionPlan    | executionPlan | Creating an execution plan                            |
   +------------------------+---------------+-------------------------------------------------------+
   | applyExecutionPlan     | executionPlan | Executing an execution plan                           |
   +------------------------+---------------+-------------------------------------------------------+
   | deleteExecutionPlan    | executionPlan | Deleting an execution plan                            |
   +------------------------+---------------+-------------------------------------------------------+
   | createTemplate         | rf-template   | Creating a template                                   |
   +------------------------+---------------+-------------------------------------------------------+
   | deleteTemplate         | rf-template   | Deleting a template                                   |
   +------------------------+---------------+-------------------------------------------------------+
   | updateTemplate         | rf-template   | Updating template metadata such as description        |
   +------------------------+---------------+-------------------------------------------------------+
   | createTemplateVersion  | rf-template   | Creating a template version                           |
   +------------------------+---------------+-------------------------------------------------------+
   | deleteTemplateVersion  | rf-template   | Deleting a template version                           |
   +------------------------+---------------+-------------------------------------------------------+
   | parseTemplateVariables | template      | Parsing template variables                            |
   +------------------------+---------------+-------------------------------------------------------+
   | useAgency              | agency        | Recording user agency                                 |
   +------------------------+---------------+-------------------------------------------------------+

Querying Traces
---------------

See \ `Querying Real-Time Traces <https://docs.otc.t-systems.com/cloud-trace-service/umn/getting_started/querying_real-time_traces.html>`__\ .
