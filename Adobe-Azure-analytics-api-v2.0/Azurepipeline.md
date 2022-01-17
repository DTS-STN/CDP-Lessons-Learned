
| title | description | ms.service|  author  | ms.date |
| --- | --- | --- | --- | --- 
|Ingest data by using Databricks in Azure Data Factory |This tutorial provides step-by-step instructions for ingesting data by using a databricks activity in Azure Data Factory |Data-Factory | Juntao Zou| 01/13/2021| 







# Transform and load data in the cloud by using a Databrick activity in Azure Data Factory



In this tutorial, you use the Azure portal to create an Azure Data Factory pipeline. This pipeline ingests data and does minimum transfomation by using a Databrick activity and Azure Key Vault linked service. 

You perform the following steps in this tutorial:

> * Access to a data factory. 
> * Access to a pipeline that uses a Databrick activity.
> * Integrate pipeline with Azure Key Vault.
> * Trigger a pipeline run.
> * Monitor the pipeline run.

If you don't have Azure portal access, please connect with the system administrator before you begin.

## Prerequisites


* **Azure storage account**. You create a Python script and an input file, and you upload them to Azure Storage. The output from the Spark program is stored in this storage account. The on-demand Spark cluster uses the same storage account as its primary storage.  




### Upload the Python script to your Blob storage account
1. Create a Python file  with the following content: 

    ```python

    
    if __name__ == "__main__":
        main()
    ```

## Cloud versus On-Prem

1.key difference between running python notebook on cloud versus on prem is that where private key is stored.

Read private key stored in Azure Key Vault
```python
    def _read_private_key(self):

        aa_private_key = dbutils.secrets.get(scope = "scope_name", key = "key_name")
        private_key = bytes('-----BEGIN PRIVATE KEY-----\n'+aa_private_key+'\n-----END PRIVATE KEY-----', 'utf-8')
        return private_key

```




## Access to a data factory

1. Launch **Microsoft Edge** or **Google Chrome** web browser. Currently, Data Factory UI is supported only in Microsoft Edge and Google Chrome web browsers,go to 
https://portal.azure.com login and then select **Data Factory**. 

![](/assets/images/AA-to-Azure-Python-Wrapper-Class/Azure-Data-Factory-access-portal.png)




## Create linked services
You author two linked services in this section: 
    
- An **Azure Storage linked service** that links an Azure storage account to the data factory.  


### Create an Azure Storage linked service

1. On the home page, switch to the **Manage** tab in the left panel. 



1. Select **Connections** at the bottom of the window, and then select **+ New**. 


1. In the **New Linked Service** window, select **Data Store** > **Azure Blob Storage**, and then select **Continue**. 


1. For **Storage account name**, select the name from the list, and then select **Save**. 




## Access to a pipeline


1.Click on 'Open' to launch Azure Data Factory Studio ,and click on the button shown below:
  
![](docs\images\Azure-Data-Factory-access-pipeline.png)

## Trigger a pipeline run

1.Select **Add Trigger** on the toolbar, and then select **Trigger Now**. 

![](/assets/images/AA-to-Azure-Python-Wrapper-Class/Azure-Data-Factory-trigger-now.png)

2.Select **Add Trigger** on the toolbar, and then select **Edit/New**. 

![](/assets/images/AA-to-Azure-Python-Wrapper-Class/Azure-Data-Factory-trigger-newedit.png)


## Monitor the pipeline run

1. Switch to the **Monitor** tab. Confirm that you see a pipeline run. 
![](/assets/images/AA-to-Azure-Python-Wrapper-Class/Azure-Data-Factory-monitor.png)
2. Select **Refresh** periodically to check the status of the pipeline run. 

  

3. To see activity runs associated with the pipeline run, select **View Activity Runs** in the **Actions** column.

  

   You can switch back to the pipeline runs view by selecting the **All Pipeline Runs** link at the top.

  

## Verify the output
Verify that the output file is created in the sclabs-site-analytics folder of the specified container based on parameter containerName below. 

```
blob = BlobClient.from_connection_string(conn_str=conn_string, container_name=containerName, blob_name="sclabs-site-analytics/blob_name.csv")
```

The file should have data in a given period (start_date to end_date based on input parameter). For example: 


![](/assets/images/AA-to-Azure-Python-Wrapper-Class/Azure-Data-Factory-result.png)

## Summary
The pipeline in this sample transforms data by using a Databrick activity and Azure Key Vault linked service. You learned how to: 

> * Create a data factory. 
> * Create a pipeline that uses a Databrick activity.
> * Trigger a pipeline run.
> * Monitor the pipeline run.

## Next Steps
To learn how to connect transformed data with Power BI in order to visualize: 

[Connect with Power BI](PowerBIReadme.md)



