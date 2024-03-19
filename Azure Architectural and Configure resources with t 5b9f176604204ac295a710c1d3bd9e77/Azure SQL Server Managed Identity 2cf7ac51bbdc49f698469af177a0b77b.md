# Azure SQL Server Managed Identity

To complete this activity, you should create a web app and an Azure SQL server and connect both of them services with traditional connection string and with managed identity.

Please refer at the bottom of this document to validate all the evidences.

1. First we need create local ASP.NET Core app cloning the sample application

```bash
# I have created a new folder to work
# Run the following commands to clone the sample...
# repository and change to its root.
genaroparedes@GenaroParedes-MacBook-Pro AzureSQL % git clone https://github.com/azure-samples/dotnetcore-sqldb-tutorial
Cloning into 'dotnetcore-sqldb-tutorial'...
remote: Enumerating objects: 271, done.
remote: Counting objects: 100% (3/3), done.
remote: Compressing objects: 100% (3/3), done.
remote: Total 271 (delta 0), reused 1 (delta 0), pack-reused 268
Receiving objects: 100% (271/271), 1.19 MiB | 2.39 MiB/s, done.
Resolving deltas: 100% (95/95), done.
genaroparedes@GenaroParedes-MacBook-Pro AzureSQL % cd dotnetcore-sqldb-tutorial

```

1. Run the application 

```bash
# It is mandatory install .NET Core befor to proceed
genaroparedes@GenaroParedes-MacBook-Pro dotnetcore-sqldb-tutorial % curl -sSL https://dot.net/v1/dotnet-install.sh | bash /dev/stdin --channel LTS              dotnet-install: Note that the intended use of this script is for Continuous Integration (CI) scenarios, where:
dotnet-install: - The SDK needs to be installed without user interaction and without admin rights.
dotnet-install: - The SDK installation doesn\'t need to persist across multiple CI runs.
dotnet-install: To set up a development environment or to run apps, use installers rather than this script. Visit https://dotnet.microsoft.com/download to get the installer.

dotnet-install: Downloading primary link https://dotnetcli.azureedge.net/dotnet/Sdk/3.1.413/dotnet-sdk-3.1.413-osx-x64.tar.gz
dotnet-install: Extracting zip from https://dotnetcli.azureedge.net/dotnet/Sdk/3.1.413/dotnet-sdk-3.1.413-osx-x64.tar.gz
dotnet-install: Adding to current process PATH: `/Users/genaroparedes/.dotnet`. Note: This change will be visible only when sourcing script.
dotnet-install: Note that the script does not resolve dependencies during installation.
dotnet-install: To check the list of dependencies, go to https://docs.microsoft.com/dotnet/core/install, select your operating system and check the "Dependencies" section.
dotnet-install: Installation finished successfully.

# Run the following commands to install the required packages... 
# run database migrations, and start the application.

#dotnet tool install -g dotnet-ef
genaroparedes@GenaroParedes-MacBook-Pro ~ % dotnet tool install -g dotnet-ef

Welcome to .NET 5.0!
---------------------
SDK Version: 5.0.401

#dotnet ef database update
genaroparedes@GenaroParedes-MacBook-Pro dotnetcore-sqldb-tutorial % dotnet ef database update
Build started...
Build succeeded.

#dotnet run
genaroparedes@GenaroParedes-MacBook-Pro dotnetcore-sqldb-tutorial % dotnet run
info: Microsoft.AspNetCore.DataProtection.KeyManagement.XmlKeyManager[62]
      User profile is available. Using '/Users/genaroparedes/.aspnet/DataProtection-Keys' as key repository; keys will not be encrypted at rest.
info: Microsoft.Hosting.Lifetime[0]
      Now listening on: http://localhost:5000
info: Microsoft.Hosting.Lifetime[0]
      Now listening on: https://localhost:5001
info: Microsoft.Hosting.Lifetime[0]
      Application started. Press Ctrl+C to shut down.
info: Microsoft.Hosting.Lifetime[0]
      Hosting environment: Production
info: Microsoft.Hosting.Lifetime[0]
      Content root path: /Users/genaroparedes/Documents/devops/AzureSQL/dotnetcore-sqldb-tutorial
```

### Application Running

![Screen Shot 2021-10-11 at 14.41.22.png](Azure%20SQL%20Server%20Managed%20Identity%202cf7ac51bbdc49f698469af177a0b77b/Screen_Shot_2021-10-11_at_14.41.22.png)

**Our app is working now we can proceed to create production SQL Database:**

We will create a Resource Group to handle all our new resources for this activity

```bash
genaroparedes@GenaroParedes-MacBook-Pro dotnetcore-sqldb-tutorial % az group create --name Activity7 --location "CentralUS"
{
  "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity7",
  "location": "centralus",
  "managedBy": null,
  "name": "Activity7",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null,
  "type": "Microsoft.Resources/resourceGroups"
}
```

After the resource group created we will create a SQL Database logical server with the `az sql server create` command

```bash
genaroparedes@GenaroParedes-MacBook-Pro dotnetcore-sqldb-tutorial % az sql server create --name Act7SQL --resource-group Activity7 --location "CentralUS" --admin-user genaro --admin-password HazaHaza10#
None
{
  "administratorLogin": "genaro",
  "administratorLoginPassword": null,
  "administrators": null,
  "federatedClientId": null,
  "fullyQualifiedDomainName": "act7sql.database.windows.net",
  "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity7/providers/Microsoft.Sql/servers/act7sql",
  "identity": null,
  "keyId": null,
  "kind": "v12.0",
  "location": "centralus",
  "minimalTlsVersion": null,
  "name": "act7sql",
  "primaryUserAssignedIdentityId": null,
  "privateEndpointConnections": [],
  "publicNetworkAccess": "Enabled",
  "resourceGroup": "Activity7",
  "restrictOutboundNetworkAccess": "Disabled",
  "state": "Ready",
  "tags": null,
  "type": "Microsoft.Sql/servers",
  "version": "12.0",
  "workspaceFeature": null
}
```

Once we have the SQL server is necessary configure a server firewall rule

```bash
genaroparedes@GenaroParedes-MacBook-Pro dotnetcore-sqldb-tutorial % az sql server firewall-rule create --resource-group Activity7 --server act7sql --name AllowAzureIps --start-ip-address 0.0.0.0 --end-ip-address 0.0.0.0
{
  "endIpAddress": "0.0.0.0",
  "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity7/providers/Microsoft.Sql/servers/act7sql/firewallRules/AllowAzureIps",
  "name": "AllowAzureIps",
  "resourceGroup": "Activity7",
  "startIpAddress": "0.0.0.0",
  "type": "Microsoft.Sql/servers/firewallRules"
}

# run the command again to allow access from your local computer by replacing...
# <your-ip-address> with your local IPv4 IP address.
genaroparedes@GenaroParedes-MacBook-Pro dotnetcore-sqldb-tutorial % az sql server firewall-rule create --name AllowLocalClient --server act7sql --resource-group Activity7 --start-ip-address=187.189.155.49 --end-ip-address=187.189.155.49
{
  "endIpAddress": "187.189.155.49",
  "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity7/providers/Microsoft.Sql/servers/act7sql/firewallRules/AllowLocalClient",
  "name": "AllowLocalClient",
  "resourceGroup": "Activity7",
  "startIpAddress": "187.189.155.49",
  "type": "Microsoft.Sql/servers/firewallRules"
}
```

Create a database with an S0 performance level in the server using the `az sql db create` command

```bash
genaroparedes@GenaroParedes-MacBook-Pro dotnetcore-sqldb-tutorial % az sql db create --resource-group Activity7 --server act7sql --name act7DB --service-objective S0
{
  "autoPauseDelay": null,
  "catalogCollation": "SQL_Latin1_General_CP1_CI_AS",
  "collation": "SQL_Latin1_General_CP1_CI_AS",
  "createMode": null,
  "creationDate": "2021-10-11T20:54:55.623000+00:00",
  "currentBackupStorageRedundancy": "Geo",
  "currentServiceObjectiveName": "S0",
  "currentSku": {
    "capacity": 10,
    "family": null,
    "name": "Standard",
    "size": null,
    "tier": "Standard"
  },
  "databaseId": "83877e7b-1482-44ce-ab65-f237ac738a35",
  "defaultSecondaryLocation": "eastus2",
  "earliestRestoreDate": null,
  "edition": "Standard",
  "elasticPoolId": null,
  "elasticPoolName": null,
  "failoverGroupId": null,
  "highAvailabilityReplicaCount": null,
  "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity7/providers/Microsoft.Sql/servers/act7sql/databases/act7DB",
  "isInfraEncryptionEnabled": false,
  "kind": "v12.0,user",
  "ledgerOn": false,
  "licenseType": null,
  "location": "centralus",
  "longTermRetentionBackupResourceId": null,
  "maintenanceConfigurationId": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/providers/Microsoft.Maintenance/publicMaintenanceConfigurations/SQL_Default",
  "managedBy": null,
  "maxLogSizeBytes": null,
  "maxSizeBytes": 268435456000,
  "minCapacity": null,
  "name": "act7DB",
  "pausedDate": null,
  "readScale": "Disabled",
  "recoverableDatabaseId": null,
  "recoveryServicesRecoveryPointId": null,
  "requestedBackupStorageRedundancy": "Geo",
  "requestedServiceObjectiveName": "S0",
  "resourceGroup": "Activity7",
  "restorableDroppedDatabaseId": null,
  "restorePointInTime": null,
  "resumedDate": null,
  "sampleName": null,
  "secondaryType": null,
  "sku": {
    "capacity": 10,
    "family": null,
    "name": "Standard",
    "size": null,
    "tier": "Standard"
  },
  "sourceDatabaseDeletionDate": null,
  "sourceDatabaseId": null,
  "status": "Online",
  "tags": null,
  "type": "Microsoft.Sql/servers/databases",
  "zoneRedundant": false
}

#Get the connection string using the az sql db show-connection-string command.
genaroparedes@GenaroParedes-MacBook-Pro dotnetcore-sqldb-tutorial % az sql db show-connection-string --client ado.net --server act7sql --name act7DB
"Server=tcp:act7sql.database.windows.net,1433;Database=act7DB;User ID=<username>;Password=<password>;Encrypt=true;Connection Timeout=30;"

# In the command output, replace <username>, and <password> with the database...
# administrator credentials you used earlier.
# This is the connection string for your ASP.NET Core app. 
# Copy it for use later.
```

Run database migrations to the production database. 

Your app currently connects to a local Sqlite database. Now that you configured an Azure SQL Database, recreate the initial migration to target it.

From the repository root, run the following commands. 

```bash
genaroparedes@GenaroParedes-MacBook-Pro dotnetcore-sqldb-tutorial % export ConnectionStrings__MyDbConnection="Server=tcp:act7sql.database.windows.net,1433;Database=act7DB;User ID=genaro;Password=HazaHaza10#;Encrypt=true;Connection Timeout=30;"
genaroparedes@GenaroParedes-MacBook-Pro dotnetcore-sqldb-tutorial % dotnet ef database update
Build started...
Build succeeded.
info: Microsoft.EntityFrameworkCore.Infrastructure[10403]
      Entity Framework Core 5.0.10 initialized 'MyDatabaseContext' using provider 'Microsoft.EntityFrameworkCore.SqlServer' with options: None
info: Microsoft.EntityFrameworkCore.Database.Command[20101]
      Executed DbCommand (101ms) [Parameters=[], CommandType='Text', CommandTimeout='30']
      SELECT 1
info: Microsoft.EntityFrameworkCore.Database.Command[20101]
      Executed DbCommand (87ms) [Parameters=[], CommandType='Text', CommandTimeout='30']
      SELECT OBJECT_ID(N'[__EFMigrationsHistory]');
info: Microsoft.EntityFrameworkCore.Database.Command[20101]
      Executed DbCommand (73ms) [Parameters=[], CommandType='Text', CommandTimeout='30']
      SELECT 1
info: Microsoft.EntityFrameworkCore.Database.Command[20101]
      Executed DbCommand (88ms) [Parameters=[], CommandType='Text', CommandTimeout='30']
      CREATE TABLE [__EFMigrationsHistory] (
          [MigrationId] nvarchar(150) NOT NULL,
          [ProductVersion] nvarchar(32) NOT NULL,
          CONSTRAINT [PK___EFMigrationsHistory] PRIMARY KEY ([MigrationId])
      );
info: Microsoft.EntityFrameworkCore.Database.Command[20101]
      Executed DbCommand (61ms) [Parameters=[], CommandType='Text', CommandTimeout='30']
      SELECT 1
info: Microsoft.EntityFrameworkCore.Database.Command[20101]
      Executed DbCommand (65ms) [Parameters=[], CommandType='Text', CommandTimeout='30']
      SELECT OBJECT_ID(N'[__EFMigrationsHistory]');
info: Microsoft.EntityFrameworkCore.Database.Command[20101]
      Executed DbCommand (90ms) [Parameters=[], CommandType='Text', CommandTimeout='30']
      SELECT [MigrationId], [ProductVersion]
      FROM [__EFMigrationsHistory]
      ORDER BY [MigrationId];
info: Microsoft.EntityFrameworkCore.Migrations[20405]
      No migrations were applied. The database is already up to date.
No migrations were applied. The database is already up to date.
Done.
```

**Run app with new configuration**

Now that database migrations is run on the production database, test your app by running:

```bash
genaroparedes@GenaroParedes-MacBook-Pro dotnetcore-sqldb-tutorial % dotnet run
info: Microsoft.AspNetCore.DataProtection.KeyManagement.XmlKeyManager[62]
      User profile is available. Using '/Users/genaroparedes/.aspnet/DataProtection-Keys' as key repository; keys will not be encrypted at rest.
info: Microsoft.Hosting.Lifetime[0]
      Now listening on: http://localhost:5000
info: Microsoft.Hosting.Lifetime[0]
      Now listening on: https://localhost:5001
info: Microsoft.Hosting.Lifetime[0]
      Application started. Press Ctrl+C to shut down.
info: Microsoft.Hosting.Lifetime[0]
      Hosting environment: Production
info: Microsoft.Hosting.Lifetime[0]
```

# Deploy app to Azure

In this step, you deploy your SQL Database-connected ASP.NET Core application to App Service

```bash
# Configure local git deployment
genaroparedes@GenaroParedes-MacBook-Pro dotnetcore-sqldb-tutorial % az webapp deployment user set --user-name genaza --password HazaHaza10#
{
  "id": null,
  "kind": null,
  "name": "web",
  "publishingPassword": null,
  "publishingPasswordHash": null,
  "publishingPasswordHashSalt": null,
  "publishingUserName": "genaza",
  "scmUri": null,
  "systemData": null,
  "type": "Microsoft.Web/publishingUsers/web"
}

# Create an App Service plan
genaroparedes@GenaroParedes-MacBook-Pro dotnetcore-sqldb-tutorial % az appservice plan create --name  myAppServicePlan --resource-group Activity7 --sku FREE --is-linux
{
  "freeOfferExpirationTime": null,
  "geoRegion": "Central US",
  "hostingEnvironmentProfile": null,
  "hyperV": false,
  "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity7/providers/Microsoft.Web/serverfarms/myAppServicePlan",
  "isSpot": false,
  "isXenon": false,
  "kind": "linux",
  "location": "centralus",
  "maximumElasticWorkerCount": 1,
  "maximumNumberOfWorkers": 0,
  "name": "myAppServicePlan",
  "numberOfSites": 0,
  "perSiteScaling": false,
  "provisioningState": "Succeeded",
  "reserved": true,
  "resourceGroup": "Activity7",
  "sku": {
    "capabilities": null,
    "capacity": 1,
    "family": "U",
    "locations": null,
    "name": "U13",
    "size": "U13",
    "skuCapacity": null,
    "tier": "LinuxFree"
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

## Create a web app

Create a web app in the myAppServicePlan App Service plan

```bash
genaroparedes@GenaroParedes-MacBook-Pro dotnetcore-sqldb-tutorial % az webapp create --resource-group Activity7 --plan myAppServicePlan --name NetApp7 --runtime "DOTNET|5.0" --deployment-local-git
Local git is configured with url of 'https://genaza@netapp7.scm.azurewebsites.net/NetApp7.git'
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
  "defaultHostName": "netapp7.azurewebsites.net",
  "deploymentLocalGitUrl": "https://genaza@netapp7.scm.azurewebsites.net/NetApp7.git",
  "enabled": true,
  "enabledHostNames": [
    "netapp7.azurewebsites.net",
    "netapp7.scm.azurewebsites.net"
  ],
  "ftpPublishingUrl": "ftp://waws-prod-dm1-185.ftp.azurewebsites.windows.net/site/wwwroot",
  "hostNameSslStates": [
    {
      "hostType": "Standard",
      "ipBasedSslResult": null,
      "ipBasedSslState": "NotConfigured",
      "name": "netapp7.azurewebsites.net",
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
      "name": "netapp7.scm.azurewebsites.net",
      "sslState": "Disabled",
      "thumbprint": null,
      "toUpdate": null,
      "toUpdateIpBasedSsl": null,
      "virtualIp": null
    }
  ],
  "hostNames": [
    "netapp7.azurewebsites.net"
  ],
  "hostNamesDisabled": false,
  "hostingEnvironmentProfile": null,
  "httpsOnly": false,
  "hyperV": false,
  "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity7/providers/Microsoft.Web/sites/NetApp7",
  "identity": null,
  "inProgressOperationId": null,
  "isDefaultContainer": null,
  "isXenon": false,
  "kind": "app,linux",
  "lastModifiedTimeUtc": "2021-10-12T04:36:35.193333",
  "location": "Central US",
  "maxNumberOfWorkers": null,
  "name": "NetApp7",
  "outboundIpAddresses": "52.158.212.237,52.158.213.228,52.185.65.42,52.185.65.124,52.185.65.130,52.185.65.157,20.40.202.4",
  "possibleOutboundIpAddresses": "52.158.212.237,52.158.213.228,52.185.65.42,52.185.65.124,52.185.65.130,52.185.65.157,52.185.65.226,52.185.65.229,52.185.65.230,52.185.66.4,52.185.66.34,52.185.66.95,52.185.66.119,52.185.66.134,52.185.66.170,52.185.66.215,52.185.66.217,52.185.66.228,13.89.139.85,13.89.139.116,13.89.140.32,13.89.140.117,13.86.101.226,13.86.102.128,20.40.202.4",
  "redundancyMode": "None",
  "repositorySiteName": "NetApp7",
  "reserved": true,
  "resourceGroup": "Activity7",
  "scmSiteAlsoStopped": false,
  "serverFarmId": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity7/providers/Microsoft.Web/serverfarms/myAppServicePlan",
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

To set connection strings for your Azure app, use the az webapp config appsettings set command in the Cloud Shell. In the following command, replace <app-name>, as well as the <connection-string> parameter with the connection string you created earlier

```bash
genaroparedes@GenaroParedes-MacBook-Pro dotnetcore-sqldb-tutorial % az webapp config connection-string set --resource-group Activity7 --name NetApp7 --settings MyDbConnection="Server=tcp:act7sql.database.windows.net,1433;Database=act7DB;User ID=genaro;Password=HazaHaza10#;Encrypt=true;Connection Timeout=30;" --connection-string-type SQLAzure
{
  "MyDbConnection": {
    "type": "SQLAzure",
    "value": "Server=tcp:act7sql.database.windows.net,1433;Database=act7DB;User ID=genaro;Password=HazaHaza10#;Encrypt=true;Connection Timeout=30;"
  }
}
```

### Push to Azure from Git

Since you're deploying the main branch, you need to set the default deployment branch for your App Service app to main (see Change deployment branch). In the Cloud Shell, set the DEPLOYMENT_BRANCH app setting with the az webapp config appsettings set command.

```bash
genaroparedes@GenaroParedes-MacBook-Pro dotnetcore-sqldb-tutorial % az webapp config appsettings set --name NetApp7 --resource-group Activity7 --settings DEPLOYMENT_BRANCH="main"
[
  {
    "name": "DEPLOYMENT_BRANCH",
    "slotSetting": false,
    "value": "main"
  }
]

genaroparedes@GenaroParedes-MacBook-Pro dotnetcore-sqldb-tutorial % git remote add azure https://genaza@netapp7.scm.azurewebsites.net/NetApp7.git 
genaroparedes@GenaroParedes-MacBook-Pro dotnetcore-sqldb-tutorial % git push azure main
```

## Update locally and redeploy

![Screen Shot 2021-10-12 at 0.32.38.png](Azure%20SQL%20Server%20Managed%20Identity%202cf7ac51bbdc49f698469af177a0b77b/Screen_Shot_2021-10-12_at_0.32.38.png)

### Publish changes to Azure

![Screen Shot 2021-10-12 at 0.39.31.png](Azure%20SQL%20Server%20Managed%20Identity%202cf7ac51bbdc49f698469af177a0b77b/Screen_Shot_2021-10-12_at_0.39.31.png)

### Resources created

![Screen Shot 2021-10-12 at 0.39.59.png](Azure%20SQL%20Server%20Managed%20Identity%202cf7ac51bbdc49f698469af177a0b77b/Screen_Shot_2021-10-12_at_0.39.59.png)

**Explain the difference of two different purchasing model of SQL: Database Transaction Unit (DTU) and vCore.**

DTU-based

This model is based on a bundled measure of compute, storage, and I/O resources. Compute sizes are expressed in DTUs for single databases and in elastic database transaction units (eDTUs) for elastic pools.

Best for customers who want simple, preconfigured resource options.

vCore-based

This model allows you to independently choose compute and storage resources. The vCore-based purchasing model also allows you to use Azure Hybrid Benefit for SQL Server to save costs.

Best for customers who value flexibility, control, and transparency.

**Explain the difference between use manage Identity and the connection-string of sql server to connect our web app with our database.**

If you want to connect to a DataBase using Connection-String you must generate the string using your ID and password, this is just necessary perform one time but you have to save your connection-string for future connections and this could expose your data, but if you use Manage Identity I think is more secure, maybe is more complex and take more time to work with it but is more secure, even passwordless.