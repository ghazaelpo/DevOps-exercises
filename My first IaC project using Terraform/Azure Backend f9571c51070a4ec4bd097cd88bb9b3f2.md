# Azure Backend

1. Create a storage account and a blob container in azure using az cli commands

```bash
#!/bin/bash
RESOURCE_GROUP_NAME=tfstaterg
STORAGE_ACCOUNT_NAME=tfstateac
CONTAINER_NAME=tfstatecn

# Create resource group
az group create --name $RESOURCE_GROUP_NAME --location eastus

# Create storage account
az storage account create --resource-group $RESOURCE_GROUP_NAME --name $STORAGE_ACCOUNT_NAME --sku Standard_LRS --encryption-services blob

# Create blob container
az storage container create --name $CONTAINER_NAME --account-name $STORAGE_ACCOUNT_NAME
```

Output after have executed the above script

```bash
genaroparedes@GenaroParedes-MacBook-Pro azure-backend % bash storageA-blobC.sh 
{
  "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/tfstaterg",
  "location": "eastus",
  "managedBy": null,
  "name": "tfstaterg",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null,
  "type": "Microsoft.Resources/resourceGroups"
}
{
  "accessTier": "Hot",
  "allowBlobPublicAccess": null,
  "allowCrossTenantReplication": null,
  "allowSharedKeyAccess": null,
  "azureFilesIdentityBasedAuthentication": null,
  "blobRestoreStatus": null,
  "creationTime": "2021-10-15T03:40:53.924075+00:00",
  "customDomain": null,
  "enableHttpsTrafficOnly": true,
  "enableNfsV3": null,
  "encryption": {
    "encryptionIdentity": null,
    "keySource": "Microsoft.Storage",
    "keyVaultProperties": null,
    "requireInfrastructureEncryption": null,
    "services": {
      "blob": {
        "enabled": true,
        "keyType": "Account",
        "lastEnabledTime": "2021-10-15T03:40:54.033423+00:00"
      },
      "file": {
        "enabled": true,
        "keyType": "Account",
        "lastEnabledTime": "2021-10-15T03:40:54.033423+00:00"
      },
      "queue": null,
      "table": null
    }
  },
  "extendedLocation": null,
  "failoverInProgress": null,
  "geoReplicationStats": null,
  "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/tfstaterg/providers/Microsoft.Storage/storageAccounts/tfstateac",
  "identity": null,
  "isHnsEnabled": null,
  "keyCreationTime": {
    "key1": "2021-10-15T03:40:54.017812+00:00",
    "key2": "2021-10-15T03:40:54.017812+00:00"
  },
  "keyPolicy": null,
  "kind": "StorageV2",
  "largeFileSharesState": null,
  "lastGeoFailoverTime": null,
  "location": "eastus",
  "minimumTlsVersion": null,
  "name": "tfstateac",
  "networkRuleSet": {
    "bypass": "AzureServices",
    "defaultAction": "Allow",
    "ipRules": [],
    "resourceAccessRules": null,
    "virtualNetworkRules": []
  },
  "primaryEndpoints": {
    "blob": "https://tfstateac.blob.core.windows.net/",
    "dfs": "https://tfstateac.dfs.core.windows.net/",
    "file": "https://tfstateac.file.core.windows.net/",
    "internetEndpoints": null,
    "microsoftEndpoints": null,
    "queue": "https://tfstateac.queue.core.windows.net/",
    "table": "https://tfstateac.table.core.windows.net/",
    "web": "https://tfstateac.z13.web.core.windows.net/"
  },
  "primaryLocation": "eastus",
  "privateEndpointConnections": [],
  "provisioningState": "Succeeded",
  "resourceGroup": "tfstaterg",
  "routingPreference": null,
  "sasPolicy": null,
  "secondaryEndpoints": null,
  "secondaryLocation": null,
  "sku": {
    "name": "Standard_LRS",
    "tier": "Standard"
  },
  "statusOfPrimary": "available",
  "statusOfSecondary": null,
  "tags": {},
  "type": "Microsoft.Storage/storageAccounts"
}

There are no credentials provided in your command and environment, we will query for account key for your storage account.
It is recommended to provide --connection-string, --account-key or --sas-token in your command as credentials.

You also can add `--auth-mode login` in your command to use Azure Active Directory (Azure AD) for authorization if your login account is assigned required RBAC roles.
For more information about RBAC roles in storage, visit https://docs.microsoft.com/en-us/azure/storage/common/storage-auth-aad-rbac-cli.

In addition, setting the corresponding environment variables can avoid inputting credentials in your command. Please use --help to get more information about environment variable usage.
{
  "created": true
}
```

1. Create a Service principal in azure

```bash
genaroparedes@GenaroParedes-MacBook-Pro azure-backend % az ad sp create-for-rbac -n servprin --role Contributor --scopes /subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/tfstaterg
Creating 'Contributor' role assignment under scope '/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/tfstaterg'
The output includes credentials that you must protect. Be sure that you do not include these credentials in your code or check the credentials into your source control. For more information, see https://aka.ms/azadsp-cli
'name' property in the output is deprecated and will be removed in the future. Use 'appId' instead.
{
  "appId": "5ac8ffbc-5a72-4ed0-b6c8-28ad2f6cd1a6",
  "displayName": "servprin",
  "name": "5ac8ffbc-5a72-4ed0-b6c8-28ad2f6cd1a6",
  "password": "7MOwHuYqnt54VS5MaL-_GXh4MFa0C7qlum",
  "tenant": "c8cd0425-e7b7-4f3d-9215-7e5fa3f439e8"
}

az ad sp create-for-rbac -n servprin --role Contributor --scopes /subscriptions/276e60c3-8219-435f-be54-2e6446efe883/resourceGroups/Demo
```

1. Export the env variables of the service principal

```bash
export ARM_SUBSCRIPTION_ID=faf4b0cb-287e-4be0-818e-c4348b26c45e
export ARM_TENANT_ID=c8cd0425-e7b7-4f3d-9215-7e5fa3f439e8
export ARM_CLIENT_ID=5ac8ffbc-5a72-4ed0-b6c8-28ad2f6cd1a6
export ARM_CLIENT_SECRET=7MOwHuYqnt54VS5MaL-_GXh4MFa0C7qlum
```

1. Create the main.tf, variables.tf, provider.tf, and terraform.tf files

**main.tf**

![Screen Shot 2021-10-14 at 23.33.15.png](Azure%20Backend%20f9571c51070a4ec4bd097cd88bb9b3f2/Screen_Shot_2021-10-14_at_23.33.15.png)

**provider.tf**

![Screen Shot 2021-10-14 at 23.33.53.png](Azure%20Backend%20f9571c51070a4ec4bd097cd88bb9b3f2/Screen_Shot_2021-10-14_at_23.33.53.png)

**terraform.tf**

![Screen Shot 2021-10-14 at 23.34.12.png](Azure%20Backend%20f9571c51070a4ec4bd097cd88bb9b3f2/Screen_Shot_2021-10-14_at_23.34.12.png)

1. Add the code to build a vnet and a subnet in main.tf:
    
    ![Screen Shot 2021-10-14 at 23.35.38.png](Azure%20Backend%20f9571c51070a4ec4bd097cd88bb9b3f2/Screen_Shot_2021-10-14_at_23.35.38.png)
    

1. Run terraform init, plan and apply

**terraform init**

![Screen Shot 2021-10-14 at 23.36.17.png](Azure%20Backend%20f9571c51070a4ec4bd097cd88bb9b3f2/Screen_Shot_2021-10-14_at_23.36.17.png)

**terraform plan**

![Screen Shot 2021-10-14 at 23.36.59.png](Azure%20Backend%20f9571c51070a4ec4bd097cd88bb9b3f2/Screen_Shot_2021-10-14_at_23.36.59.png)

**terraform apply**

![Screen Shot 2021-10-14 at 23.37.49.png](Azure%20Backend%20f9571c51070a4ec4bd097cd88bb9b3f2/Screen_Shot_2021-10-14_at_23.37.49.png)

![Screen Shot 2021-10-14 at 23.38.03.png](Azure%20Backend%20f9571c51070a4ec4bd097cd88bb9b3f2/Screen_Shot_2021-10-14_at_23.38.03.png)

**Resources deployed**

![Screen Shot 2021-10-15 at 0.59.58.png](Azure%20Backend%20f9571c51070a4ec4bd097cd88bb9b3f2/Screen_Shot_2021-10-15_at_0.59.58.png)

**Name changed** 

![Screen Shot 2021-10-15 at 1.54.09.png](Azure%20Backend%20f9571c51070a4ec4bd097cd88bb9b3f2/Screen_Shot_2021-10-15_at_1.54.09.png)

![Screen Shot 2021-10-15 at 2.03.12.png](Azure%20Backend%20f9571c51070a4ec4bd097cd88bb9b3f2/Screen_Shot_2021-10-15_at_2.03.12.png)

![Screen Shot 2021-10-15 at 2.03.46.png](Azure%20Backend%20f9571c51070a4ec4bd097cd88bb9b3f2/Screen_Shot_2021-10-15_at_2.03.46.png)