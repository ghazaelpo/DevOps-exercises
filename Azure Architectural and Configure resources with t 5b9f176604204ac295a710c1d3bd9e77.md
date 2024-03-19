# Azure Architectural and Configure resources with tools

# Activity 1

In this Mind Map I covered the basic Azure Architecture and as second part of this activity I will explain how to create an Azure Account.

Regarding the below Mind Map I would like to mention a quick and basic overview about the Azure Architecture. This infrastructure is divided by geographical areas such as USA, Canada, India; these geographies are divided in regions and then a region is compose by three availability zones but if we put together two regions will call "Region Pair", availability zones are physically separate Datacenters within an Azure region. The Datacenters stage will be the last physical infrastructure to then pass to all cloud services, this cloud services are hosted by all the infrastructure mentioned. If we have an Azure account this will the key to access and use cloud resources and start to work.

![Azure architecture concepts.jpg](Azure%20Architectural%20and%20Configure%20resources%20with%20t%205b9f176604204ac295a710c1d3bd9e77/Azure_architecture_concepts.jpg)

### Steps to create an Azure Account

If you want to create an Azure account and start to work just follow the below steps:

- Choose an account to begin the register
    
    ![Screen Shot 2021-09-30 at 10.10.10.png](Azure%20Architectural%20and%20Configure%20resources%20with%20t%205b9f176604204ac295a710c1d3bd9e77/Screen_Shot_2021-09-30_at_10.10.10.png)
    

- The page will suggest you options to get a Subscription if you don’t have one, in this case I will choose "Access student benefits", if your account is not student account just select "Start with an Azure free trial", the procedure is the same.
    
    ![Screen Shot 2021-09-30 at 10.11.10.png](Azure%20Architectural%20and%20Configure%20resources%20with%20t%205b9f176604204ac295a710c1d3bd9e77/Screen_Shot_2021-09-30_at_10.11.10.png)
    

- Once you had chosen the "Access student benefits", the browser show you an education page web, here just click on "Claim your Azure credit now"
    
    ![Screen Shot 2021-09-30 at 10.19.02.png](Azure%20Architectural%20and%20Configure%20resources%20with%20t%205b9f176604204ac295a710c1d3bd9e77/Screen_Shot_2021-09-30_at_10.19.02.png)
    

- Then just click on "Start free"
    
    ![Screen Shot 2021-09-30 at 10.20.08.png](Azure%20Architectural%20and%20Configure%20resources%20with%20t%205b9f176604204ac295a710c1d3bd9e77/Screen_Shot_2021-09-30_at_10.20.08.png)
    

***Finally you just have to fill out some personal information and that is all.***

# Activity 2

**Configure Azure resources with tools** such as Azure portal Azure PowerShell, Azure CLI or Azure Cloud Shell.

1. **Create a resource Group from Azure Portal**
    - Go to [portal.azure.com](https://portal.azure.com/#home)
    - In the home page click on Resource groups icon
        
        ![Screen Shot 2021-09-30 at 10.41.45.png](Azure%20Architectural%20and%20Configure%20resources%20with%20t%205b9f176604204ac295a710c1d3bd9e77/Screen_Shot_2021-09-30_at_10.41.45.png)
        
    - Then click on Create and start with the process
        
        ![Screen Shot 2021-09-30 at 10.45.20.png](Azure%20Architectural%20and%20Configure%20resources%20with%20t%205b9f176604204ac295a710c1d3bd9e77/Screen_Shot_2021-09-30_at_10.45.20.png)
        
- Select the subscription you will use, the name and the region. Once you have filled out, click on "Review + create" button.
    
    ![Screen Shot 2021-09-30 at 10.46.42.png](Azure%20Architectural%20and%20Configure%20resources%20with%20t%205b9f176604204ac295a710c1d3bd9e77/Screen_Shot_2021-09-30_at_10.46.42.png)
    
- If your project details passed the validation, click on "Create" button.
    
    ![Screen Shot 2021-09-30 at 10.49.39.png](Azure%20Architectural%20and%20Configure%20resources%20with%20t%205b9f176604204ac295a710c1d3bd9e77/Screen_Shot_2021-09-30_at_10.49.39.png)
    
- Here is our resource group created "Activity2_DOU"
    
    ![Screen Shot 2021-09-30 at 10.51.41.png](Azure%20Architectural%20and%20Configure%20resources%20with%20t%205b9f176604204ac295a710c1d3bd9e77/Screen_Shot_2021-09-30_at_10.51.41.png)
    

1. **Create a Virtual Network from Azure Portal**

The process is similar to create a resource group, please try to relation between each other 

- In the home page click on Virtual Network icon
    
    ![Screen Shot 2021-09-30 at 12.23.05.png](Azure%20Architectural%20and%20Configure%20resources%20with%20t%205b9f176604204ac295a710c1d3bd9e77/Screen_Shot_2021-09-30_at_12.23.05.png)
    
- Then click on Create and start with the process
    
    ![Screen Shot 2021-09-30 at 12.24.59.png](Azure%20Architectural%20and%20Configure%20resources%20with%20t%205b9f176604204ac295a710c1d3bd9e77/Screen_Shot_2021-09-30_at_12.24.59.png)
    
- Select the subscription you will use and the resource group that will virtual network belong, the name and the region. Once you have filled out, click on "Review + create" button.
    
    ![Screen Shot 2021-09-30 at 12.28.27.png](Azure%20Architectural%20and%20Configure%20resources%20with%20t%205b9f176604204ac295a710c1d3bd9e77/Screen_Shot_2021-09-30_at_12.28.27.png)
    
- If your project details passed the validation, click on "Create" button
    
    ![Screen Shot 2021-09-30 at 12.30.34.png](Azure%20Architectural%20and%20Configure%20resources%20with%20t%205b9f176604204ac295a710c1d3bd9e77/Screen_Shot_2021-09-30_at_12.30.34.png)
    
- Here we have our virtual network created and deployed
    
    
    ![Screen Shot 2021-09-30 at 12.30.58.png](Azure%20Architectural%20and%20Configure%20resources%20with%20t%205b9f176604204ac295a710c1d3bd9e77/Screen_Shot_2021-09-30_at_12.30.58.png)
    
1. **Install Azure CLI**

If you are using MAC as in my case, you follow the below steps:

```bash
# If you don't have installed Homebrew just use this command
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# You can install the Azure CLI on macOS by updating your brew repository information, 
# and then running the install command:
brew update && brew install azure-cli

# You can then run the Azure CLI with the az command. 
# To sign in, use az login command.
# A web page will display and ask your account information
az login

# Follow all these steps as per I described
```

1. **Create a resource Group with Azure CLI**

```bash
# You have to specify the name and the region using -n for name and 
# -l for location 
# This is the command you have to use to create a Resource Group...
# Using CLI 
# az group create -n name -l region
# az group create -n newResourceExample -l westus
genaroparedes@GenaroParedes-MacBook-Pro ~ % az group create -n newResourceExample -l westus
{
  "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/newResourceExample",
  "location": "westus",
  "managedBy": null,
  "name": "newResourceExample",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null,
  "type": "Microsoft.Resources/resourceGroups"
}
```

1. **Create a Virtual Network with Azure CLI**

```bash
# Create a virtual Network is similar to create a resource group
# the format is:
# az network vnet create -n NAME -g GROUP_RESOURCE --subnet-name DEFAULT
genaroparedes@GenaroParedes-MacBook-Pro ~ % az network vnet create -n VirNetExample -g Activity2_DOU --subnet-name default
{
  "newVNet": {
    "addressSpace": {
      "addressPrefixes": [
        "10.0.0.0/16"
      ]
    },
    "bgpCommunities": null,
    "ddosProtectionPlan": null,
    "dhcpOptions": {
      "dnsServers": []
    },
    "enableDdosProtection": false,
    "enableVmProtection": null,
    "etag": "W/\"f92e95c0-44bc-42c1-9a37-cc507da9fed1\"",
    "extendedLocation": null,
    "flowTimeoutInMinutes": null,
    "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity2_DOU/providers/Microsoft.Network/virtualNetworks/VirNetExample",
    "ipAllocations": null,
    "location": "centralus",
    "name": "VirNetExample",
    "provisioningState": "Succeeded",
    "resourceGroup": "Activity2_DOU",
    "resourceGuid": "56b54afd-8127-426a-847d-71b535c0bd95",
    "subnets": [
      {
        "addressPrefix": "10.0.0.0/24",
        "addressPrefixes": null,
        "applicationGatewayIpConfigurations": null,
        "delegations": [],
        "etag": "W/\"f92e95c0-44bc-42c1-9a37-cc507da9fed1\"",
        "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity2_DOU/providers/Microsoft.Network/virtualNetworks/VirNetExample/subnets/default",
        "ipAllocations": null,
        "ipConfigurationProfiles": null,
        "ipConfigurations": null,
        "name": "default",
        "natGateway": null,
        "networkSecurityGroup": null,
        "privateEndpointNetworkPolicies": "Enabled",
        "privateEndpoints": null,
        "privateLinkServiceNetworkPolicies": "Enabled",
        "provisioningState": "Succeeded",
        "purpose": null,
        "resourceGroup": "Activity2_DOU",
        "resourceNavigationLinks": null,
        "routeTable": null,
        "serviceAssociationLinks": null,
        "serviceEndpointPolicies": null,
        "serviceEndpoints": null,
        "type": "Microsoft.Network/virtualNetworks/subnets"
      }
    ],
    "tags": {},
    "type": "Microsoft.Network/virtualNetworks",
    "virtualNetworkPeerings": []
  }
}
```

1. **Install Az PowerShell module**

```bash
# First we have to install Homebrew as we downloaded and...
# installed Azure CLI
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Now, you can install PowerShell
brew install --cask powershell

# Finally, verify that your install is working properly:
pwsh
```

1. **Create a resource Group with PowerShell**

```bash
# Execute Powershell on your terminal
genaroparedes@GenaroParedes-MacBook-Pro ~ % pwsh
PowerShell 7.1.4
Copyright (c) Microsoft Corporation.

https://aka.ms/powershell
Type 'help' to get help.

PS /Users/genaroparedes>

# Start the resource group creation using the below command
# Use -Name flag to set a resource name
# Use -Location flag to set a region name
# Add the flags to New-AzResourceGroup command
PS /Users/genaroparedes> New-AzResourceGroup -Name NewResourceGroup-pwsh -Location "East US"

ResourceGroupName : NewResourceGroup-pwsh
Location          : eastus
ProvisioningState : Succeeded
Tags              : 
ResourceId        : /subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/NewResourceGroup-pwsh
```

1. **Create a Virtual Network with PowerShell**

```bash
# Execute Powershell on your terminal
genaroparedes@GenaroParedes-MacBook-Pro ~ % pwsh
PowerShell 7.1.4
Copyright (c) Microsoft Corporation.

https://aka.ms/powershell
Type 'help' to get help.

PS /Users/genaroparedes>

# Start the Virtual Network creation using the below command
# Use -n flag to set a name
# Use -ResourceGroupName flag to defines a group name to attach our VN
# Use -Location flag to set a region name
# Use -AddressPrefix to defines the Address space
PS /Users/genaroparedes> New-AzVirtualNetwork -n VirtNetpwsh -ResourceGroupName newResourceGroup-pwsh -Location "East US" -AddressPrefix 10.0.0.0/24

Name                   : VirtNetpwsh
ResourceGroupName      : newResourceGroup-pwsh
Location               : eastus
Id                     : /subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/newResourceGroup-pwsh/providers/Microsoft
                         .Network/virtualNetworks/VirtNetpwsh
Etag                   : W/"5bdc8ccf-7a22-4663-b209-3c7ed92e7126"
ResourceGuid           : 180ad9fe-279c-4158-9f4e-088034fb3352
ProvisioningState      : Succeeded
Tags                   : 
AddressSpace           : {
                           "AddressPrefixes": [
                             "10.0.0.0/24"
                           ]
                         }
DhcpOptions            : {}
FlowTimeoutInMinutes   : null
Subnets                : []
VirtualNetworkPeerings : []
EnableDdosProtection   : false
DdosProtectionPlan     : null
ExtendedLocation       : null
```

Note: Use Diferentes Locations for each Resource Group.

[First Azure Infrastructure ](Azure%20Architectural%20and%20Configure%20resources%20with%20t%205b9f176604204ac295a710c1d3bd9e77/First%20Azure%20Infrastructure%204565bb7683fa4b3ba8d66e54e8df5342.md)

[Creating a Virtual Machine](Azure%20Architectural%20and%20Configure%20resources%20with%20t%205b9f176604204ac295a710c1d3bd9e77/Creating%20a%20Virtual%20Machine%2034695dcc34ab4036b911a8a13b83c7dc.md)

[Azure SQL Server Managed Identity](Azure%20Architectural%20and%20Configure%20resources%20with%20t%205b9f176604204ac295a710c1d3bd9e77/Azure%20SQL%20Server%20Managed%20Identity%202cf7ac51bbdc49f698469af177a0b77b.md)

[Azure Identity Access Management and Storage](Azure%20Architectural%20and%20Configure%20resources%20with%20t%205b9f176604204ac295a710c1d3bd9e77/Azure%20Identity%20Access%20Management%20and%20Storage%209cab5b3353e344eda51467348743bbe3.md)

[Azure Container Registry and Web App for containers](Azure%20Architectural%20and%20Configure%20resources%20with%20t%205b9f176604204ac295a710c1d3bd9e77/Azure%20Container%20Registry%20and%20Web%20App%20for%20container%2065e37339b84549eb90d5b2abef98830f.md)