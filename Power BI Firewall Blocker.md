# Power BI Firewall Blocker

Authors: Arpit Dhindsa

## Overview

This "Lessons Learned" document is meant to be a repository of institutional memory for hard-won insights and understanding around the tools and technologies used to develop the SAEB architecture.                              

## Context

Currently there is a problem with PowerBI connections being blocked on some firewall. Regardless of the data source (whether its Databricks Spark Tables or Synapse Analytics), Power BI Desktop is required to create reports. In order to build these reports in Power BI Desktop requires establishing connection to these sources which fails with an error due to firewall setup.

Attempting to connect Power BI desktop with Azure Databricks using Azure Databricks connector and Spark connector results in the following error

![Azure Databricks Connection Error](assets/images/az-databricks-connection-error.png)

Additionally, attempting to connect Power BI Desktop to Synapse SQL DW using Azure Synapse Analytics connector and the SQL Server Database connector also results in the following error

![Synapse SQL DW Connection Error](assets/images/synapse-sql-dw-connection-error.png)

Resolving this issue will involve stakeholders form both ESDC and SSC so, the focus of this exercise is to discover the possible workarounds to the problem before seeking networking help to open Ports and IPs in the Firewall.

## Goals
The goal of this exercise is to have a reliable solution in place. 

To do this, following questions need to be answered.
- What is the suggested workaround? What other workarounds might there be?
- What are the implications of the workaround?
- Is it sustainable? For how long?
- How will it effect the SAEB architecture? 
- Will it have security implications? 
- What is the firewall blocking? 
- What can we determine on our own though debugging tools?
- What do we actually need help determining? Who, might that be?


## Workarounds
One workaround is to connect to Azure Synapse Analytics or Databricks Spark Tables from Power BI Desktop off-network (off-VPN) to build reports. Once the report has been created, log back into VPN and upload the report on Power BI Report Server so, it can be viewed by other memebers of the team.

This workaround was used for the Nov29 deliverable.

The implications of this workaround include:
- 
