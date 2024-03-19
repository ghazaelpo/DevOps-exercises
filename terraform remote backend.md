# terraform remote backend

# 🎳 Working on teams and managing backends

## 🤠 By Genaro Paredes, Octavio Palacios, Mario Robles

### Creating a storage account and a blob container in azure using AZ CLI commands

```bash
#!/bin/bashRESOURCE_GROUP_NAME=tfstaterg
STORAGE_ACCOUNT_NAME=tfstateac
CONTAINER_NAME=tfstatecn

# Create resource groupaz group create --name $RESOURCE_GROUP_NAME --location eastus

# Create storage accountaz storage account create --resource-group $RESOURCE_GROUP_NAME --name $STORAGE_ACCOUNT_NAME --sku Standard_LRS --encryption-services blob

# Create blob containeraz storage container create --name $CONTAINER_NAME --account-name $STORAGE_ACCOUNT_NAME
```

### Output after have executed the above script

```bash
genaroparedes@GenaroParedes-MacBook-Pro azure-backend % bash storageA-blobC.sh
{  "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/tfstaterg",
  "location": "eastus",
  "managedBy": null,
  "name": "tfstaterg",
  "properties": {    "provisioningState": "Succeeded"  },
  "tags": null,
  "type": "Microsoft.Resources/resourceGroups"}{  "accessTier": "Hot",
  "allowBlobPublicAccess": null,
  "allowCrossTenantReplication": null,
  "allowSharedKeyAccess": null,
  "azureFilesIdentityBasedAuthentication": null,
  "blobRestoreStatus": null,
  "creationTime": "2021-10-15T03:40:53.924075+00:00",
  "customDomain": null,
  "enableHttpsTrafficOnly": true,
  "enableNfsV3": null,
  "encryption": {    "encryptionIdentity": null,
    "keySource": "Microsoft.Storage",
    "keyVaultProperties": null,
    "requireInfrastructureEncryption": null,
    "services": {      "blob": {        "enabled": true,
        "keyType": "Account",
        "lastEnabledTime": "2021-10-15T03:40:54.033423+00:00"      },
      "file": {        "enabled": true,
        "keyType": "Account",
        "lastEnabledTime": "2021-10-15T03:40:54.033423+00:00"      },
      "queue": null,
      "table": null
    }  },
  "extendedLocation": null,
  "failoverInProgress": null,
  "geoReplicationStats": null,
  "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/tfstaterg/providers/Microsoft.Storage/storageAccounts/tfstateac",
  "identity": null,
  "isHnsEnabled": null,
  "keyCreationTime": {    "key1": "2021-10-15T03:40:54.017812+00:00",
    "key2": "2021-10-15T03:40:54.017812+00:00"  },
  "keyPolicy": null,
  "kind": "StorageV2",
  "largeFileSharesState": null,
  "lastGeoFailoverTime": null,
  "location": "eastus",
  "minimumTlsVersion": null,
  "name": "tfstateac",
  "networkRuleSet": {    "bypass": "AzureServices",
    "defaultAction": "Allow",
    "ipRules": [],
    "resourceAccessRules": null,
    "virtualNetworkRules": []  },
  "primaryEndpoints": {    "blob": "https://tfstateac.blob.core.windows.net/",
    "dfs": "https://tfstateac.dfs.core.windows.net/",
    "file": "https://tfstateac.file.core.windows.net/",
    "internetEndpoints": null,
    "microsoftEndpoints": null,
    "queue": "https://tfstateac.queue.core.windows.net/",
    "table": "https://tfstateac.table.core.windows.net/",
    "web": "https://tfstateac.z13.web.core.windows.net/"  },
  "primaryLocation": "eastus",
  "privateEndpointConnections": [],
  "provisioningState": "Succeeded",
  "resourceGroup": "tfstaterg",
  "routingPreference": null,
  "sasPolicy": null,
  "secondaryEndpoints": null,
  "secondaryLocation": null,
  "sku": {    "name": "Standard_LRS",
    "tier": "Standard"  },
  "statusOfPrimary": "available",
  "statusOfSecondary": null,
  "tags": {},
  "type": "Microsoft.Storage/storageAccounts"}There are no credentials provided in your command and environment, we will query for account key for your storage account.
It is recommended to provide --connection-string, --account-key or --sas-token in your command as credentials.

You also can add `--auth-mode login` in your command to use Azure Active Directory (Azure AD) for authorization if your login account is assigned required RBAC roles.
For more information about RBAC roles in storage, visit https://docs.microsoft.com/en-us/azure/storage/common/storage-auth-aad-rbac-cli.

In addition, setting the corresponding environment variables can avoid inputting credentials in your command. Please use --help to get more information about environment variable usage.
{  "created": true}
```

### Creating a Service principal in azure:

```bash
genaroparedes@GenaroParedes-MacBook-Pro azure-backend % az ad sp create-for-rbac -n servprin --role Contributor --scopes /subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/tfstaterg
Creating 'Contributor' role assignment under scope '/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/tfstaterg'The output includes credentials that you must protect. Be sure that you do not include these credentials in your code or check the credentials into your source control. For more information, see https://aka.ms/azadsp-cli
'name' property in the output is deprecated and will be removed in the future. Use 'appId' instead.
{  "appId": "5ac8ffbc-5a72-4ed0-b6c8-28ad2f6cd1a6",
  "displayName": "servprin",
  "name": "5ac8ffbc-5a72-4ed0-b6c8-28ad2f6cd1a6",
  "password": "7MOwHuYqnt54VS5MaL-_GXh4MFa0C7qlum",
  "tenant": "c8cd0425-e7b7-4f3d-9215-7e5fa3f439e8"}
```

### Exporting the env variables of the service principal

```bash
export ARM_SUBSCRIPTION_ID=faf4b0cb-287e-4be0-818e-c4348b26c45e
export ARM_TENANT_ID=c8cd0425-e7b7-4f3d-9215-7e5fa3f439e8
export ARM_CLIENT_ID=5ac8ffbc-5a72-4ed0-b6c8-28ad2f6cd1a6
export ARM_CLIENT_SECRET=7MOwHuYqnt54VS5MaL-_GXh4MFa0C7qlum
```

## Creating the main.tf, variables.tf, provider.tf, and terraform.tf files:

**main.tf**

![Untitled](terraform%20remote%20backend%209ab817e136e6456db5d23c888f339ef1/Untitled.png)

**provider.tf**

![Untitled](terraform%20remote%20backend%209ab817e136e6456db5d23c888f339ef1/Untitled%201.png)

**terraform.tf**

![Untitled](terraform%20remote%20backend%209ab817e136e6456db5d23c888f339ef1/Untitled%202.png)

### Adding the code to build a vnet and a subnet in main.tf:

![Untitled](terraform%20remote%20backend%209ab817e136e6456db5d23c888f339ef1/Untitled%203.png)

## Running terraform init, plan and apply:

**terraform init**

![Untitled](terraform%20remote%20backend%209ab817e136e6456db5d23c888f339ef1/Untitled%204.png)

**terraform plan**

![Untitled](terraform%20remote%20backend%209ab817e136e6456db5d23c888f339ef1/Untitled%205.png)

**terraform apply**

![Untitled](terraform%20remote%20backend%209ab817e136e6456db5d23c888f339ef1/Untitled%206.png)

![Untitled](terraform%20remote%20backend%209ab817e136e6456db5d23c888f339ef1/Untitled%207.png)

**Resources deployed:**

![Untitled](terraform%20remote%20backend%209ab817e136e6456db5d23c888f339ef1/Untitled%208.png)

# First remote part:

### Repo cloned:

![Screen Shot 2021-10-15 at 7.25.51.png](terraform%20remote%20backend%209ab817e136e6456db5d23c888f339ef1/Screen_Shot_2021-10-15_at_7.25.51.png)

### Adding the NSG:

![Screen Shot 2021-10-15 at 7.03.50.png](terraform%20remote%20backend%209ab817e136e6456db5d23c888f339ef1/Screen_Shot_2021-10-15_at_7.03.50.png)

**Resource deployed**

![Screen Shot 2021-10-15 at 8.02.35.png](terraform%20remote%20backend%209ab817e136e6456db5d23c888f339ef1/Screen_Shot_2021-10-15_at_8.02.35.png)

### Exporting credentials:

![Screen Shot 2021-10-15 at 7.04.15.png](terraform%20remote%20backend%209ab817e136e6456db5d23c888f339ef1/Screen_Shot_2021-10-15_at_7.04.15.png)

### Applying the changes:

![Screen Shot 2021-10-15 at 7.06.35.png](terraform%20remote%20backend%209ab817e136e6456db5d23c888f339ef1/Screen_Shot_2021-10-15_at_7.06.35.png)

![Screen Shot 2021-10-15 at 7.06.40.png](terraform%20remote%20backend%209ab817e136e6456db5d23c888f339ef1/Screen_Shot_2021-10-15_at_7.06.40.png)

![Screen Shot 2021-10-15 at 7.08.08.png](terraform%20remote%20backend%209ab817e136e6456db5d23c888f339ef1/Screen_Shot_2021-10-15_at_7.08.08.png)

# Second remote part:

### Repo cloned and credentials exported:

![Screen Shot 2021-10-15 at 8.37.20 2.png](terraform%20remote%20backend%209ab817e136e6456db5d23c888f339ef1/Screen_Shot_2021-10-15_at_8.37.20_2.png)

### **Terraform init and plan last changes into the infrastructure**

![Screen Shot 2021-10-15 at 8.39.31.png](terraform%20remote%20backend%209ab817e136e6456db5d23c888f339ef1/Screen_Shot_2021-10-15_at_8.39.31.png)

![Screen Shot 2021-10-15 at 8.39.41.png](terraform%20remote%20backend%209ab817e136e6456db5d23c888f339ef1/Screen_Shot_2021-10-15_at_8.39.41.png)

### **Terraform apply last changes into the infrastructure**

![Screen Shot 2021-10-15 at 8.41.12 2.png](terraform%20remote%20backend%209ab817e136e6456db5d23c888f339ef1/Screen_Shot_2021-10-15_at_8.41.12_2.png)

![Screen Shot 2021-10-15 at 8.41.16.png](terraform%20remote%20backend%209ab817e136e6456db5d23c888f339ef1/Screen_Shot_2021-10-15_at_8.41.16.png)

# Resources in the portal:

![Screen Shot 2021-10-15 at 8.43.29.png](terraform%20remote%20backend%209ab817e136e6456db5d23c888f339ef1/Screen_Shot_2021-10-15_at_8.43.29.png)