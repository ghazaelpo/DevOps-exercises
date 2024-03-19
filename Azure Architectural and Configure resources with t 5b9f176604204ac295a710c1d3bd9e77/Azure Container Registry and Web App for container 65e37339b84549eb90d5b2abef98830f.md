# Azure Container Registry and Web App for containers

### Activity 1

You will create an Azure Container Registry and push an Image

1. First I will create An Azure Container Registry

"Create an Azure Container registry. You can use azure portal, Azure CLI or Azure Powershell. SKU: Basic."

```bash
# Create a Resource group to handle all the resoruces for this activity
genaroparedes@GenaroParedes-MacBook-Pro ~ % az group create --name Activity6 --location eastus
{
  "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity6",
  "location": "eastus",
  "managedBy": null,
  "name": "Activity6",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null,
  "type": "Microsoft.Resources/resourceGroups"
}

# Then we need create a Container Registry, this is the main resource...
# for this activity
genaroparedes@GenaroParedes-MacBook-Pro ~ % az acr create --resource-group Activity6 --name ContRegAct6 --sku Basic
{
  "adminUserEnabled": false,
  "anonymousPullEnabled": false,
  "creationDate": "2021-10-08T15:22:11.673223+00:00",
  "dataEndpointEnabled": false,
  "dataEndpointHostNames": [],
  "encryption": {
    "keyVaultProperties": null,
    "status": "disabled"
  },
  "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity6/providers/Microsoft.ContainerRegistry/registries/ContRegAct6",
  "identity": null,
  "location": "eastus",
  "loginServer": "contregact6.azurecr.io",
  "name": "ContRegAct6",
  "networkRuleBypassOptions": "AzureServices",
  "networkRuleSet": null,
  "policies": {
    "exportPolicy": {
      "status": "enabled"
    },
    "quarantinePolicy": {
      "status": "disabled"
    },
    "retentionPolicy": {
      "days": 7,
      "lastUpdatedTime": "2021-10-08T15:22:13.660210+00:00",
      "status": "disabled"
    },
    "trustPolicy": {
      "status": "disabled",
      "type": "Notary"
    }
  },
  "privateEndpointConnections": [],
  "provisioningState": "Succeeded",
  "publicNetworkAccess": "Enabled",
  "resourceGroup": "Activity6",
  "sku": {
    "name": "Basic",
    "tier": "Basic"
  },
  "status": null,
  "systemData": {
    "createdAt": "2021-10-08T15:22:11.673223+00:00",
    "createdBy": "genaro.paredes@digitalonus.com",
    "createdByType": "User",
    "lastModifiedAt": "2021-10-08T15:22:11.673223+00:00",
    "lastModifiedBy": "genaro.paredes@digitalonus.com",
    "lastModifiedByType": "User"
  },
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries",
  "zoneRedundancy": "Disabled"
}

# Before pushing and pulling container images, we must log in to the registry.
# Don't forget activate Docker to avoid any error

genaroparedes@GenaroParedes-MacBook-Pro ~ % az acr login --name ContRegAct6
Login Succeeded

```

1. Once we have already created our Container Registry is necessary pull an image before to push it

"Pull the Docker image [ASP.NET](http://asp.net/)"

```bash
# Before to continue is necessary pull an image, for this example will pull...
# ASP.NET
genaroparedes@GenaroParedes-MacBook-Pro ~ % docker pull mcr.microsoft.com/dotnet/core/samples:aspnetapp
aspnetapp: Pulling from dotnet/core/samples
bd897bb914af: Pull complete 
0f8bc71d5d86: Pull complete 
8cb7a49ba121: Pull complete 
e7ac35d102ab: Pull complete 
a72680bef715: Pull complete 
198562d3ade3: Pull complete 
93be773f8497: Pull complete 
Digest: sha256:2fe03aeb8af9ff49b6bc927fd342aa1b036881392b7f5b90026ee6ee6f6dd839
Status: Downloaded newer image for mcr.microsoft.com/dotnet/core/samples:aspnetapp
mcr.microsoft.com/dotnet/core/samples:aspnetapp

# Before you can push an image to your registry, you must tag it with...
# the fully qualified name of your registry login server.
# Tag the image using the docker tag command.
genaroparedes@GenaroParedes-MacBook-Pro ~ % docker tag mcr.microsoft.com/dotnet/core/samples:aspnetapp contregact6.azurecr.io/asp.net:v1
# As you can see the first element is the new tag version
genaroparedes@GenaroParedes-MacBook-Pro ~ % docker images
REPOSITORY                              TAG         IMAGE ID       CREATED       SIZE
contregact6.azurecr.io/asp.net          v1          b18dcc37d54e   7 days ago    216MB
mcr.microsoft.com/dotnet/core/samples   aspnetapp   b18dcc37d54e   7 days ago    216MB
terraform_azure_cli                     latest      6d50b5ea2a6c   10 days ago   1.09GB
ghazaelpo/terraform-azure-cli           v1          6d50b5ea2a6c   10 days ago   1.09GB
ghazaelpo/aws_cli_terraform             v1          d59148de6382   10 days ago   471MB
aws-cli-terraform                       latest      d59148de6382   10 days ago   471MB
docker_compose_flask-example            latest      8dc14d5970ad   11 days ago   922MB
nginx                                   latest      ad4c705f24d3   4 weeks ago   133MB

# Now we can proceed to push our image to the registry instance 
genaroparedes@GenaroParedes-MacBook-Pro ~ % docker push contregact6.azurecr.io/asp.net:v1
The push refers to repository [contregact6.azurecr.io/asp.net]
c47eae4a010d: Pushed 
eddd1d6f91d4: Pushed 
762b3f2d3c1f: Pushed 
22f8f5ea66d5: Pushed 
ba04b46fbea9: Pushed 
954169280011: Pushed 
a548c9107c3a: Pushed 
v1: digest: sha256:272503fab4c7fa2235069df881f47db2e851efcadd08814edb0e5910a1efff84 size: 1788

# After pushing the image to your container registry, remove the...
# image from your local Docker environment.
genaroparedes@GenaroParedes-MacBook-Pro ~ % docker rmi contregact6.azurecr.io/asp.net:v1
Untagged: contregact6.azurecr.io/asp.net:v1
Untagged: contregact6.azurecr.io/asp.net@sha256:272503fab4c7fa2235069df881f47db2e851efcadd08814edb0e5910a1efff84
genaroparedes@GenaroParedes-MacBook-Pro ~ % docker images                               
REPOSITORY                              TAG         IMAGE ID       CREATED       SIZE
mcr.microsoft.com/dotnet/core/samples   aspnetapp   b18dcc37d54e   7 days ago    216MB
ghazaelpo/terraform-azure-cli           v1          6d50b5ea2a6c   10 days ago   1.09GB
terraform_azure_cli                     latest      6d50b5ea2a6c   10 days ago   1.09GB
ghazaelpo/aws_cli_terraform             v1          d59148de6382   10 days ago   471MB
aws-cli-terraform                       latest      d59148de6382   10 days ago   471MB
docker_compose_flask-example            latest      8dc14d5970ad   11 days ago   922MB
nginx                                   latest      ad4c705f24d3   4 weeks ago   133MB

# If you already pushed the image you can list it
# As you can see here is our uploaded image 
genaroparedes@GenaroParedes-MacBook-Pro ~ % az acr repository list --name ContRegAct6 --output table
Result
--------
asp.net
```

On the Azure portal we can find our registry container

![Screen Shot 2021-10-08 at 11.02.55.png](Azure%20Container%20Registry%20and%20Web%20App%20for%20container%2065e37339b84549eb90d5b2abef98830f/Screen_Shot_2021-10-08_at_11.02.55.png)

And even our created repository 

![Screen Shot 2021-10-08 at 11.04.14.png](Azure%20Container%20Registry%20and%20Web%20App%20for%20container%2065e37339b84549eb90d5b2abef98830f/Screen_Shot_2021-10-08_at_11.04.14.png)

![Screen Shot 2021-10-08 at 11.05.00.png](Azure%20Container%20Registry%20and%20Web%20App%20for%20container%2065e37339b84549eb90d5b2abef98830f/Screen_Shot_2021-10-08_at_11.05.00.png)

If clicked in v1 tag will see our [ASP.NET](http://ASP.NET) image 

![Screen Shot 2021-10-08 at 11.06.28.png](Azure%20Container%20Registry%20and%20Web%20App%20for%20container%2065e37339b84549eb90d5b2abef98830f/Screen_Shot_2021-10-08_at_11.06.28.png)

### Activity 2

Create a web app and deploy from the Docker Image that you push to the ACR in the Activity. Create with Azure CLI is a nice to have.

```bash
# If we run the previous container from Activity 1
genaroparedes@GenaroParedes-MacBook-Pro ~ % docker run -p 8080:80 -d mcr.microsoft.com/dotnet/core/samples:aspnetapp
562c0a2041ef1618b7c0a509528df9266dcd6c0a7cd6df96782412d6f92d6004

# We can see the below home page from the image
# But this is running locally 
# The goal is deploy and run a containerized web app with Azure App Service
```

![Screen Shot 2021-10-08 at 11.20.51.png](Azure%20Container%20Registry%20and%20Web%20App%20for%20container%2065e37339b84549eb90d5b2abef98830f/Screen_Shot_2021-10-08_at_11.20.51.png)

### Deploy a web app by using an image from an Azure Container Registry repository

First we need enable Docker access to the Azure Container Registry

![Screen Shot 2021-10-08 at 12.23.43.png](Azure%20Container%20Registry%20and%20Web%20App%20for%20container%2065e37339b84549eb90d5b2abef98830f/Screen_Shot_2021-10-08_at_12.23.43.png)

**Now we are ready to create our Web App:**

To deploy a container to Azure App Service, you first create a web app on App Service, then connect the web app to the container registry. When the web app starts, App Service automatically pulls the image from the registry.

1. Create an App Service plan using the az appservice plan create command.

```bash
genaroparedes@GenaroParedes-MacBook-Pro ~ % az appservice plan create --name myApp6SerPlan --resource-group Activity6 --is-linux
{
  "freeOfferExpirationTime": "2021-11-07T21:05:04.900000",
  "geoRegion": "East US",
  "hostingEnvironmentProfile": null,
  "hyperV": false,
  "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity6/providers/Microsoft.Web/serverfarms/myApp6SerPlan",
  "isSpot": false,
  "isXenon": false,
  "kind": "linux",
  "location": "eastus",
  "maximumElasticWorkerCount": 1,
  "maximumNumberOfWorkers": 0,
  "name": "myApp6SerPlan",
  "numberOfSites": 0,
  "perSiteScaling": false,
  "provisioningState": "Succeeded",
  "reserved": true,
  "resourceGroup": "Activity6",
  "sku": {
    "capabilities": null,
    "capacity": 1,
    "family": "B",
    "locations": null,
    "name": "B1",
    "size": "B1",
    "skuCapacity": null,
    "tier": "Basic"
  },
  "spotExpirationTime": null,
  "status": "Ready",
  "subscription": "faf4b0cb-287e-4be0-818e-c4348b26c45e",
  "systemData": null,
  "tags": null,
  "targetWorkerCount": 0,
  "targetWorkerSizeId": 0,
  "type": "Microsoft.Web/serverfarms",
  "workerTierName": null
}
```

1. Create the web app with the az webpp create command.

```bash
genaroparedes@GenaroParedes-MacBook-Pro ~ % az webapp create --resource-group Activity6 --plan myApp6SerPlan --name testapp6 --deployment-container-image-name contregact6.azurecr.io/asp.net:v1
No credential was provided to access Azure Container Registry. Trying to look up...
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "clientCertExclusionPaths": null,
  "clientCertMode": "Required",
  "cloningInfo": null,
  "containerSize": 0,
  "customDomainVerificationId": "EE39B4ABEBD77323234F2A092175E36BC91D8A46CA9E083C7DBFD301FA57EEBE",
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "testapp6.azurewebsites.net",
  "enabled": true,
  "enabledHostNames": [
    "testapp6.azurewebsites.net",
    "testapp6.scm.azurewebsites.net"
  ],
  "ftpPublishingUrl": "ftp://waws-prod-blu-191.ftp.azurewebsites.windows.net/site/wwwroot",
  "hostNameSslStates": [
    {
      "hostType": "Standard",
      "ipBasedSslResult": null,
      "ipBasedSslState": "NotConfigured",
      "name": "testapp6.azurewebsites.net",
      "sslState": "Disabled",
      "thumbprint": null,
      "toUpdate": null,
      "toUpdateIpBasedSsl": null,
      "virtualIp": null
    },
    {
      "hostType": "Repository",
      "ipBasedSslResult": null,
      "ipBasedSslState": "NotConfigured",
      "name": "testapp6.scm.azurewebsites.net",
      "sslState": "Disabled",
      "thumbprint": null,
      "toUpdate": null,
      "toUpdateIpBasedSsl": null,
      "virtualIp": null
    }
  ],
  "hostNames": [
    "testapp6.azurewebsites.net"
  ],
  "hostNamesDisabled": false,
  "hostingEnvironmentProfile": null,
  "httpsOnly": false,
  "hyperV": false,
  "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity6/providers/Microsoft.Web/sites/testapp6",
  "identity": null,
  "inProgressOperationId": null,
  "isDefaultContainer": null,
  "isXenon": false,
  "kind": "app,linux,container",
  "lastModifiedTimeUtc": "2021-10-11T07:28:50.086666",
  "location": "East US",
  "maxNumberOfWorkers": null,
  "name": "testapp6",
  "outboundIpAddresses": "52.188.143.242,40.71.235.172,40.71.236.147,40.71.236.232,40.71.238.92,52.142.34.225,20.49.104.3",
  "possibleOutboundIpAddresses": "52.188.143.242,40.71.235.172,40.71.236.147,40.71.236.232,40.71.238.92,52.142.34.225,52.149.246.34,52.179.115.42,52.179.118.77,52.191.94.124,52.224.89.255,52.224.92.113,52.226.52.76,52.226.52.105,52.226.52.106,52.226.53.47,52.226.53.100,52.226.54.47,104.45.183.144,104.45.183.219,52.186.162.43,104.45.183.209,52.186.162.106,52.186.163.7,20.49.104.3",
  "redundancyMode": "None",
  "repositorySiteName": "testapp6",
  "reserved": true,
  "resourceGroup": "Activity6",
  "scmSiteAlsoStopped": false,
  "serverFarmId": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity6/providers/Microsoft.Web/serverfarms/myApp6SerPlan",
  "siteConfig": {
    "acrUseManagedIdentityCreds": false,
    "acrUserManagedIdentityID": null,
    "alwaysOn": false,
    "apiDefinition": null,
    "apiManagementConfig": null,
    "appCommandLine": null,
    "appSettings": null,
    "autoHealEnabled": null,
    "autoHealRules": null,
    "autoSwapSlotName": null,
    "azureMonitorLogCategories": null,
    "azureStorageAccounts": null,
    "connectionStrings": null,
    "cors": null,
    "customAppPoolIdentityAdminState": null,
    "customAppPoolIdentityTenantState": null,
    "defaultDocuments": null,
    "detailedErrorLoggingEnabled": null,
    "documentRoot": null,
    "experiments": null,
    "fileChangeAuditEnabled": null,
    "ftpsState": null,
    "functionAppScaleLimit": 0,
    "functionsRuntimeScaleMonitoringEnabled": null,
    "handlerMappings": null,
    "healthCheckPath": null,
    "http20Enabled": false,
    "httpLoggingEnabled": null,
    "ipSecurityRestrictions": [
      {
        "action": "Allow",
        "description": "Allow all access",
        "headers": null,
        "ipAddress": "Any",
        "name": "Allow all",
        "priority": 1,
        "subnetMask": null,
        "subnetTrafficTag": null,
        "tag": null,
        "vnetSubnetResourceId": null,
        "vnetTrafficTag": null
      }
    ],
    "javaContainer": null,
    "javaContainerVersion": null,
    "javaVersion": null,
    "keyVaultReferenceIdentity": null,
    "limits": null,
    "linuxFxVersion": "",
    "loadBalancing": null,
    "localMySqlEnabled": null,
    "logsDirectorySizeLimit": null,
    "machineKey": null,
    "managedPipelineMode": null,
    "managedServiceIdentityId": null,
    "metadata": null,
    "minTlsVersion": null,
    "minimumElasticInstanceCount": 0,
    "netFrameworkVersion": null,
    "nodeVersion": null,
    "numberOfWorkers": 1,
    "phpVersion": null,
    "powerShellVersion": null,
    "preWarmedInstanceCount": null,
    "publicNetworkAccess": null,
    "publishingPassword": null,
    "publishingUsername": null,
    "push": null,
    "pythonVersion": null,
    "remoteDebuggingEnabled": null,
    "remoteDebuggingVersion": null,
    "requestTracingEnabled": null,
    "requestTracingExpirationTime": null,
    "routingRules": null,
    "runtimeADUser": null,
    "runtimeADUserPassword": null,
    "scmIpSecurityRestrictions": [
      {
        "action": "Allow",
        "description": "Allow all access",
        "headers": null,
        "ipAddress": "Any",
        "name": "Allow all",
        "priority": 1,
        "subnetMask": null,
        "subnetTrafficTag": null,
        "tag": null,
        "vnetSubnetResourceId": null,
        "vnetTrafficTag": null
      }
    ],
    "scmIpSecurityRestrictionsUseMain": null,
    "scmMinTlsVersion": null,
    "scmType": null,
    "sitePort": null,
    "tracingOptions": null,
    "use32BitWorkerProcess": null,
    "virtualApplications": null,
    "vnetName": null,
    "vnetPrivatePortsCount": null,
    "vnetRouteAllEnabled": null,
    "webSocketsEnabled": null,
    "websiteTimeZone": null,
    "winAuthAdminState": null,
    "winAuthTenantState": null,
    "windowsFxVersion": null,
    "xManagedServiceIdentityId": null
  },
  "slotSwapStatus": null,
  "state": "Running",
  "suspendedTill": null,
  "systemData": null,
  "tags": null,
  "targetSwapSlot": null,
  "trafficManagerHostNames": null,
  "type": "Microsoft.Web/sites",
  "usageState": "Normal"
}
```

1. Use the az webapp config container set command to specify the container registry and the image to deploy for the web app

```bash
genaroparedes@GenaroParedes-MacBook-Pro ~ % az webapp config container set --name testapp6 --resource-group Activity6 --docker-custom-image-name ContRegAct6.azurecr.io/asp.net:v1 --docker-registry-server-url https://ContRegAct6.azurecr.io
No credential was provided to access Azure Container Registry. Trying to look up...
Retrieving credentials failed with an exception:'No resource or more than one were found with name 'ContRegAct6'.'
[
  {
    "name": "WEBSITES_ENABLE_APP_SERVICE_STORAGE",
    "slotSetting": false,
    "value": "false"
  },
  {
    "name": "DOCKER_REGISTRY_SERVER_URL",
    "slotSetting": false,
    "value": "https://ContRegAct6.azurecr.io"
  },
  {
    "name": "DOCKER_REGISTRY_SERVER_USERNAME",
    "slotSetting": false,
    "value": "ContRegAct6"
  },
  {
    "name": "DOCKER_REGISTRY_SERVER_PASSWORD",
    "slotSetting": false,
    "value": null
  },
  {
    "name": "DOCKER_CUSTOM_IMAGE_NAME",
    "value": "DOCKER|ContRegAct6.azurecr.io/asp.net:v1"
  }
]
```

1. Once our image is deployed go to App Servcices and select the name chosen to see an overview from the created resource and get the URL to access it

```bash
https://testapp6.azurewebsites.net
```

![Screen Shot 2021-10-11 at 2.36.06.png](Azure%20Container%20Registry%20and%20Web%20App%20for%20container%2065e37339b84549eb90d5b2abef98830f/Screen_Shot_2021-10-11_at_2.36.06.png)

![Screen Shot 2021-10-11 at 2.38.15.png](Azure%20Container%20Registry%20and%20Web%20App%20for%20container%2065e37339b84549eb90d5b2abef98830f/Screen_Shot_2021-10-11_at_2.38.15.png)

### **Resources created**

Resources from Activity6 resource group

![Screen Shot 2021-10-11 at 2.41.12.png](Azure%20Container%20Registry%20and%20Web%20App%20for%20container%2065e37339b84549eb90d5b2abef98830f/Screen_Shot_2021-10-11_at_2.41.12.png)

Registry settings from testapp6

![Screen Shot 2021-10-11 at 2.42.53.png](Azure%20Container%20Registry%20and%20Web%20App%20for%20container%2065e37339b84549eb90d5b2abef98830f/Screen_Shot_2021-10-11_at_2.42.53.png)

[Azure Monitoring](Azure%20Container%20Registry%20and%20Web%20App%20for%20container%2065e37339b84549eb90d5b2abef98830f/Azure%20Monitoring%208b5d3650775f4d69924c13ee57b6263c.md)