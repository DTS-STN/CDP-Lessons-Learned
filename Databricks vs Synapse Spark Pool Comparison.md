# Databricks vs Synapse Spark Pool Comaprison

Authors: Arpit Dhindsa

## Overview

This "Lessons Learned" document is meant to be a repository of institutional memory for hard-won insights and understanding around the tools and technologies used to develop the SAEB architecture.                              

## Context
Apache Spark is a unified engine designed for large-scale distributed data processing. It incorporates libraries for machine learning, SQL for interactive queries and stream processing for interactive real-time data and graph processing. The two main tools in Azure Cloud that provide Spark as a service are Azure Databricks and Azure Synapse. 

Azure Databricks is a collaborative Apache Spark-based Big Data analytics platform 

Azure Synapse is an analytics service that brings together enterprise data warehousing and Big Data analytics.

## Goals
To better understand the differences between these two tools in how they leverage Spark (Python), tests were conducted to capture the differences of:
- Performance
- Cost
- Usability by a Data scientists

## Comparison
The document below outlines key differences between the two Spark services in Azure Cloud.

### Cluster/Spark Pool Setup
In Synpase Analytics, spark applications run on a Apache Spark Pool. Currently, we can only create pools with Memory Optimized nodes and choose from one of two available Spark versions: _Spark 2.4_ and _Spark 3.1_. There are 6 different node sizes available from Small (4vCores / 32 GB) to XXLarge (64 vCores / 432 GB).

Whereas in Databricks, we run spark applications on a cluster. The three available cluster modes are Single Node, Standard and High Concurrency. There are multiple Databricks Runtime Versions to choose from having different Scala and Spark versions. Additionallly, there is large selection of different worker types.

### Pricing
For both services, pricing is based on the number of virtual machines provisioned and their sizing. With Databricks, there is an additional fee for Databricks Units (DBUs). A DBU is a unit of processing capability, billed on a per-second usage. The DBU consumption depends on the size and type of instance running Azure Databricks. 
See these links for [Databricks](https://azure.microsoft.com/en-ca/pricing/details/databricks/) and [Synapse](https://azure.microsoft.com/en-us/pricing/details/synapse-analytics/) pricing.

### Notebook Evironment
Databricks provides collaborative notebooks with real time co-authoring and automatic versioning. Whereas Synapse requires you to save the changes to your notebook before the other person can see them. There is no automatic versioning in Synapse notebooks.

### Git Integration
Both services offer GIT integration.

### Performance/Speed
To test the performance of Synapse and Databricks Spark, NYC Taxi & Limousine Commission's - yellow and green taxi trip datasets were used from Azure ML Open Datasets. To have same test conditions for both the technologies, a similar Spark Pool and Databricks cluster were provisioned. Synapse Spark Pool with 3-15 nodes, each node with 64 GB RAM and 8vCores (medium size) with Autoscaling enabled was created. Similarly, a cluster with Databricks Runtime 9.0 (having Spark version 3.1) and 3-15 memory-optimized workers/nodes, each with 64 GB RAM and 8vCores was created.



