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
### Connecting to Azure Synapse and Databricks off VPN
One workaround is to connect to Azure Synapse Analytics or Databricks Spark Tables from Power BI Desktop off-network (off-VPN) to build reports. Once the report has been created, log back into VPN and upload the report on Power BI Report Server so, it can be viewed by other memebers of the team.

This workaround was used for the Nov29 deliverable.

The implication of this workaround is that if access to ESDC Azure gets restricted to VPN, then the user will not be able to connect to the source and create Power BI reports as Power BI Desktop application running on VPN cannot establish connection to these services to date due to firewall setup.

### Configure a Azure VM and data gateways in the Power BI service
Alternatively, configuring VNets and the Power BI Gateway (in a VM) provides secure access between Power BI and Azure SQL database without opening up the firewall to all Azure Services. The steps on how to set this up are listed in this [Microsoft blog](https://devblogs.microsoft.com/premier-developer/secure-access-to-azure-sql-servers-for-power-bi/).

## Connect to Synapse from your own network
To connect to SQL resources (dedicated SQL pools and serverless SQL pool) in Synapse workspace using Power BI, make sure that the firewall on your network and local computer allows outgoing communication on TCP ports 1443. Also allow outgoing communication to TCP ports 80 and 443.

See this [Microsoft documentation](https://docs.microsoft.com/en-us/power-bi/connect-data/service-admin-troubleshooting-scheduled-refresh-azure-sql-databases) for reference.
