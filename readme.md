
pip install azure-storage-file-datalake azure-identity

https://learn.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-directory-file-acl-python?tabs=azure-ad

connection:
You can authorize access to data using your account access keys (Shared Key). The following code example creates a DataLakeServiceClient instance that is authorized with the account key:
def get_service_client_account_key(self, account_name, account_key) -> DataLakeServiceClient:
    account_url = f"https://{account_name}.dfs.core.windows.net"
    service_client = DataLakeServiceClient(account_url, credential=account_key)

    return service_client

To use a shared access signature (SAS) token, provide the token as a string and initialize a DataLakeServiceClient object. If your account URL includes the SAS token, omit the credential parameter.
def get_service_client_sas(self, account_name: str, sas_token: str) -> DataLakeServiceClient:
    account_url = f"https://{account_name}.dfs.core.windows.net"

    # The SAS token string can be passed in as credential param or appended to the account URL
    service_client = DataLakeServiceClient(account_url, credential=sas_token)

    return service_client
    
from azure.identity import ClientSecretCredential
from azure.storage.blob import BlobServiceClient

from adlfs import AzureBlobFileSystem


Prerequisite
For this post, it is required to have:

Azure Data Lake Storage
Azure Databricks
Solution
In order to access ADLS Gen2 data in Spark, we need ADLS Gen2 details like Connection String, Key, Storage Name, etc.

There are multiple ways to access the ADLS Gen2 file like directly using shared access key, configuration, mount, mount using SPN, etc. Here in this post, we are going to use mount to access the Gen2 Data Lake files in Azure Databricks.

You can refer to the below post to

Create Mount in Azure Databricks
Create Mount in Azure Databricks using Service Principal & OAuth
In our last post, we had already created a mount point on Azure Data Lake Gen2 storage. Here, we are going to use the mount point to read a file from Azure Data Lake Gen2 using Spark Scala.

https://thisismeetpatel.medium.com/read-csv-file-from-azure-blob-storage-to-directly-to-data-frame-using-python-83d34c4cbe57

https://github.com/TEAM-QUANDO/my-python-function/tree/29f4f05686743ed20604d5dd0cdd7b7675920e3a

https://github.com/OrlinAndreev90/AzureFunctions/tree/e0af3a41a4da84ae409cc1e34a1036a2283ce38f
