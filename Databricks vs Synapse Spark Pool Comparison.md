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

### Cluster 

