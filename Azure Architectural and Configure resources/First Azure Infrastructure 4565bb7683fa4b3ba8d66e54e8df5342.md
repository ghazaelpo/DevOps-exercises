# First Azure Infrastructure

### Instructions

- To complete this activity, you should create two virtual machines, and both are them should be connected with a Load Balancer.
- Furthermore, the virtual machines must have an installation of one of the next tools:
    - Jenkins
    - Gitlab

For this, you can choose to install manually or with a script after creation, or include it with custom-data script in the creation process.

The activity must create an infrastructure that looks like the following diagram:

![activity3.png](First%20Azure%20Infrastructure%204565bb7683fa4b3ba8d66e54e8df5342/activity3.png)

We are going to follow a few steps to achieve the instructions above.

I decided use a script to create the load balancer and all the necessary resources such as Network Security Group, Virtual Machines, IP Public, etc.

For the required tool I decided install manually, logging into the server and execute the necessary commands.

These all will discussed below:

```bash
#!/bin/bash
# This is script generate all the necessary resources and...
# two Virtual Machines for the activity
# I will explain step by step

# Creating a new resource group to handle our Virtual Machines
# Our resource group is called Activity3_DOU
echo '---------------------------------------------------------'
echo 'Creating a New Resource Group'
az group create -n Activity3_DOU -l "Central US"

# Network Security Group to handle and filter the network traffic
# Our security group is called Activity3NSG
echo '---------------------------------------------------------'
echo 'Creating a Network Security Group'
az network nsg create --resource-group Activity3_DOU --name Activity3NSG

# IP public address to expose our resources
# Our public IP is called Activity3Jenkins
echo '---------------------------------------------------------'
echo 'Creating an IP public address'
az network public-ip create --resource-group Activity3_DOU --name Activity3Jenkins --sku Standard

# Creating a Virtual Network to use on our Virtual Machines
# Our Virtual Network is called Activity3-VN
echo '---------------------------------------------------------'
echo 'Creating a Virtual Network'
az network vnet create --name Activity3-VN --resource-group Activity3_DOU --network-security-group Activity3NSG --subnet-name Activity3_SubNet

# Network Security Group, adding inbound rule on port 8080
# This rule is neccesary to allow access on port 8080 through web
echo '---------------------------------------------------------'
echo 'Adding inbound rule on port 8080'
az network nsg rule create --resource-group Activity3_DOU --nsg-name Activity3NSG --name NSG-Jenkins-Rule --protocol '*' --direction inbound --source-address-prefix '*' --source-port-range '*' --destination-address-prefix '*' --destination-port-range 8080 --access allow --priority 200

# Creating another rule through port 22 to allow ssh connections
# This connection allow the incoming request to use SSH
echo '---------------------------------------------------------'
echo 'Adding inbound rule on port 22'
az network nsg rule create --resource-group Activity3_DOU --nsg-name Activity3NSG --name Activity3-SSH --protocol '*' --direction inbound --source-address-prefix '*' --source-port-range '*' --destination-address-prefix '*' --destination-port-range 22 --access allow --priority 100

# Creating the Load Balancer
# The main task from this activity, this load balancer will distribute...
# all the traffic between two Virtual Machines
echo '---------------------------------------------------------'
echo 'Creating a Load Balancer'
az network lb create --resource-group Activity3_DOU --name Activity3-Load-Balancer --sku Standard --public-ip-address Activity3Jenkins --frontend-ip-name FrontEnd --backend-pool-name BackEndPool

# Creating a Health probe
# Health probe is just available for Standard Load Balancer
echo '---------------------------------------------------------'
echo 'Creating a Health probe'
az network lb probe create --resource-group Activity3_DOU --lb-name Activity3-Load-Balancer --name Activity3-Probe-Health --protocol tcp --port 8080

# Creating a Load Balancer Rule to handle the incoming and receive traffic... 
# and the required source and destination port
echo '---------------------------------------------------------'
echo 'Creating a Load balancer Rule'
az network lb rule create --lb-name Activity3-Load-Balancer --resource-group Activity3_DOU --name LoadB-Rule --protocol tcp --frontend-port 8080 --backend-port 8080 --frontend-ip-name FrontEnd --backend-pool-name BackEndPool --probe-name Activity3-Probe-Health

# In this part we will create two virtual machines and network interfaces
# The for will iterate numVM variable, from 1 to 2
numVM=( 1 2 )
for i in "${numVM[@]}"
do
    echo '----------------------------'
    echo 'Creating Network Interface'
    echo '----------------------------'
    az network nic create \
        --resource-group Activity3_DOU \
        --name activity3-nic-$i \
        --vnet-name Activity3-VN \
        --subnet Activity3_SubNet \
        --ip-forwarding \
        --network-security-group Activity3NSG \
        --lb-name Activity3-Load-Balancer \
        --lb-address-pools BackEndPool

    echo '----------------------------'
    echo 'Creating Virtual Machine'
    echo '----------------------------'
    az vm create \
        --resource-group Activity3_DOU \
        --name activity3-vm-$i \
        --image UbuntuLTS \
        --admin-username genaroparedes \
        --nics activity3-nic-$i \
        --size Standard_D1_v2 \
        --storage-sku Standard_LRS \
        --os-disk-size-gb 63 \
        --custom-data jenkins-custom-installation.txt
done
```

**Output from the script**

```bash
genaroparedes@GenaroParedes-MacBook-Pro myowninfr % bash 03-FirstInfr.sh 
---------------------------------------------------------
Creating a New Resource Group
{
  "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity3_DOU",
  "location": "centralus",
  "managedBy": null,
  "name": "Activity3_DOU",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null,
  "type": "Microsoft.Resources/resourceGroups"
}
---------------------------------------------------------
Creating a Network Security Group
{
  "NewNSG": {
    "defaultSecurityRules": [
      {
        "access": "Allow",
        "description": "Allow inbound traffic from all VMs in VNET",
        "destinationAddressPrefix": "VirtualNetwork",
        "destinationAddressPrefixes": [],
        "destinationApplicationSecurityGroups": null,
        "destinationPortRange": "*",
        "destinationPortRanges": [],
        "direction": "Inbound",
        "etag": "W/\"5807fc44-afbf-4e5d-a919-c606a1f93b75\"",
        "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity3_DOU/providers/Microsoft.Network/networkSecurityGroups/Activity3NSG/defaultSecurityRules/AllowVnetInBound",
        "name": "AllowVnetInBound",
        "priority": 65000,
        "protocol": "*",
        "provisioningState": "Succeeded",
        "resourceGroup": "Activity3_DOU",
        "sourceAddressPrefix": "VirtualNetwork",
        "sourceAddressPrefixes": [],
        "sourceApplicationSecurityGroups": null,
        "sourcePortRange": "*",
        "sourcePortRanges": [],
        "type": "Microsoft.Network/networkSecurityGroups/defaultSecurityRules"
      },
      {
        "access": "Allow",
        "description": "Allow inbound traffic from azure load balancer",
        "destinationAddressPrefix": "*",
        "destinationAddressPrefixes": [],
        "destinationApplicationSecurityGroups": null,
        "destinationPortRange": "*",
        "destinationPortRanges": [],
        "direction": "Inbound",
        "etag": "W/\"5807fc44-afbf-4e5d-a919-c606a1f93b75\"",
        "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity3_DOU/providers/Microsoft.Network/networkSecurityGroups/Activity3NSG/defaultSecurityRules/AllowAzureLoadBalancerInBound",
        "name": "AllowAzureLoadBalancerInBound",
        "priority": 65001,
        "protocol": "*",
        "provisioningState": "Succeeded",
        "resourceGroup": "Activity3_DOU",
        "sourceAddressPrefix": "AzureLoadBalancer",
        "sourceAddressPrefixes": [],
        "sourceApplicationSecurityGroups": null,
        "sourcePortRange": "*",
        "sourcePortRanges": [],
        "type": "Microsoft.Network/networkSecurityGroups/defaultSecurityRules"
      },
      {
        "access": "Deny",
        "description": "Deny all inbound traffic",
        "destinationAddressPrefix": "*",
        "destinationAddressPrefixes": [],
        "destinationApplicationSecurityGroups": null,
        "destinationPortRange": "*",
        "destinationPortRanges": [],
        "direction": "Inbound",
        "etag": "W/\"5807fc44-afbf-4e5d-a919-c606a1f93b75\"",
        "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity3_DOU/providers/Microsoft.Network/networkSecurityGroups/Activity3NSG/defaultSecurityRules/DenyAllInBound",
        "name": "DenyAllInBound",
        "priority": 65500,
        "protocol": "*",
        "provisioningState": "Succeeded",
        "resourceGroup": "Activity3_DOU",
        "sourceAddressPrefix": "*",
        "sourceAddressPrefixes": [],
        "sourceApplicationSecurityGroups": null,
        "sourcePortRange": "*",
        "sourcePortRanges": [],
        "type": "Microsoft.Network/networkSecurityGroups/defaultSecurityRules"
      },
      {
        "access": "Allow",
        "description": "Allow outbound traffic from all VMs to all VMs in VNET",
        "destinationAddressPrefix": "VirtualNetwork",
        "destinationAddressPrefixes": [],
        "destinationApplicationSecurityGroups": null,
        "destinationPortRange": "*",
        "destinationPortRanges": [],
        "direction": "Outbound",
        "etag": "W/\"5807fc44-afbf-4e5d-a919-c606a1f93b75\"",
        "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity3_DOU/providers/Microsoft.Network/networkSecurityGroups/Activity3NSG/defaultSecurityRules/AllowVnetOutBound",
        "name": "AllowVnetOutBound",
        "priority": 65000,
        "protocol": "*",
        "provisioningState": "Succeeded",
        "resourceGroup": "Activity3_DOU",
        "sourceAddressPrefix": "VirtualNetwork",
        "sourceAddressPrefixes": [],
        "sourceApplicationSecurityGroups": null,
        "sourcePortRange": "*",
        "sourcePortRanges": [],
        "type": "Microsoft.Network/networkSecurityGroups/defaultSecurityRules"
      },
      {
        "access": "Allow",
        "description": "Allow outbound traffic from all VMs to Internet",
        "destinationAddressPrefix": "Internet",
        "destinationAddressPrefixes": [],
        "destinationApplicationSecurityGroups": null,
        "destinationPortRange": "*",
        "destinationPortRanges": [],
        "direction": "Outbound",
        "etag": "W/\"5807fc44-afbf-4e5d-a919-c606a1f93b75\"",
        "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity3_DOU/providers/Microsoft.Network/networkSecurityGroups/Activity3NSG/defaultSecurityRules/AllowInternetOutBound",
        "name": "AllowInternetOutBound",
        "priority": 65001,
        "protocol": "*",
        "provisioningState": "Succeeded",
        "resourceGroup": "Activity3_DOU",
        "sourceAddressPrefix": "*",
        "sourceAddressPrefixes": [],
        "sourceApplicationSecurityGroups": null,
        "sourcePortRange": "*",
        "sourcePortRanges": [],
        "type": "Microsoft.Network/networkSecurityGroups/defaultSecurityRules"
      },
      {
        "access": "Deny",
        "description": "Deny all outbound traffic",
        "destinationAddressPrefix": "*",
        "destinationAddressPrefixes": [],
        "destinationApplicationSecurityGroups": null,
        "destinationPortRange": "*",
        "destinationPortRanges": [],
        "direction": "Outbound",
        "etag": "W/\"5807fc44-afbf-4e5d-a919-c606a1f93b75\"",
        "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity3_DOU/providers/Microsoft.Network/networkSecurityGroups/Activity3NSG/defaultSecurityRules/DenyAllOutBound",
        "name": "DenyAllOutBound",
        "priority": 65500,
        "protocol": "*",
        "provisioningState": "Succeeded",
        "resourceGroup": "Activity3_DOU",
        "sourceAddressPrefix": "*",
        "sourceAddressPrefixes": [],
        "sourceApplicationSecurityGroups": null,
        "sourcePortRange": "*",
        "sourcePortRanges": [],
        "type": "Microsoft.Network/networkSecurityGroups/defaultSecurityRules"
      }
    ],
    "etag": "W/\"5807fc44-afbf-4e5d-a919-c606a1f93b75\"",
    "flowLogs": null,
    "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity3_DOU/providers/Microsoft.Network/networkSecurityGroups/Activity3NSG",
    "location": "centralus",
    "name": "Activity3NSG",
    "networkInterfaces": null,
    "provisioningState": "Succeeded",
    "resourceGroup": "Activity3_DOU",
    "resourceGuid": "8bc9d52a-6207-4d2f-a9f8-4356230cc653",
    "securityRules": [],
    "subnets": null,
    "tags": null,
    "type": "Microsoft.Network/networkSecurityGroups"
  }
}
---------------------------------------------------------
Creating an IP public address
[Coming breaking change] In the coming release, the default behavior will be changed as follows when sku is Standard and zone is not provided: For zonal regions, you will get a zone-redundant IP indicated by zones:["1","2","3"]; For non-zonal regions, you will get a non zone-redundant IP indicated by zones:null.
{
  "publicIp": {
    "ddosSettings": null,
    "deleteOption": null,
    "dnsSettings": null,
    "etag": "W/\"40f1e21a-471c-4fcd-a383-93d99dee8b39\"",
    "extendedLocation": null,
    "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity3_DOU/providers/Microsoft.Network/publicIPAddresses/Activity3Jenkins",
    "idleTimeoutInMinutes": 4,
    "ipAddress": "40.122.185.18",
    "ipConfiguration": null,
    "ipTags": [],
    "linkedPublicIpAddress": null,
    "location": "centralus",
    "migrationPhase": null,
    "name": "Activity3Jenkins",
    "natGateway": null,
    "provisioningState": "Succeeded",
    "publicIpAddressVersion": "IPv4",
    "publicIpAllocationMethod": "Static",
    "publicIpPrefix": null,
    "resourceGroup": "Activity3_DOU",
    "resourceGuid": "d54f10ac-c618-4594-99bd-68103d7688d7",
    "servicePublicIpAddress": null,
    "sku": {
      "name": "Standard",
      "tier": "Regional"
    },
    "tags": null,
    "type": "Microsoft.Network/publicIPAddresses",
    "zones": null
  }
}
---------------------------------------------------------
Creating a Virtual Network
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
    "etag": "W/\"22f2cee7-f03f-4c4a-8e43-f3f3820160af\"",
    "extendedLocation": null,
    "flowTimeoutInMinutes": null,
    "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity3_DOU/providers/Microsoft.Network/virtualNetworks/Activity3-VN",
    "ipAllocations": null,
    "location": "centralus",
    "name": "Activity3-VN",
    "provisioningState": "Succeeded",
    "resourceGroup": "Activity3_DOU",
    "resourceGuid": "fbb42007-d36f-437f-916e-cb45b8f2d5f2",
    "subnets": [
      {
        "addressPrefix": "10.0.0.0/24",
        "addressPrefixes": null,
        "applicationGatewayIpConfigurations": null,
        "delegations": [],
        "etag": "W/\"22f2cee7-f03f-4c4a-8e43-f3f3820160af\"",
        "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity3_DOU/providers/Microsoft.Network/virtualNetworks/Activity3-VN/subnets/Activity3_SubNet",
        "ipAllocations": null,
        "ipConfigurationProfiles": null,
        "ipConfigurations": null,
        "name": "Activity3_SubNet",
        "natGateway": null,
        "networkSecurityGroup": {
          "defaultSecurityRules": null,
          "etag": null,
          "flowLogs": null,
          "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity3_DOU/providers/Microsoft.Network/networkSecurityGroups/Activity3NSG",
          "location": null,
          "name": null,
          "networkInterfaces": null,
          "provisioningState": null,
          "resourceGroup": "Activity3_DOU",
          "resourceGuid": null,
          "securityRules": null,
          "subnets": null,
          "tags": null,
          "type": null
        },
        "privateEndpointNetworkPolicies": "Enabled",
        "privateEndpoints": null,
        "privateLinkServiceNetworkPolicies": "Enabled",
        "provisioningState": "Succeeded",
        "purpose": null,
        "resourceGroup": "Activity3_DOU",
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
---------------------------------------------------------
Adding inbound rule on port 8080
{
  "access": "Allow",
  "description": null,
  "destinationAddressPrefix": "*",
  "destinationAddressPrefixes": [],
  "destinationApplicationSecurityGroups": null,
  "destinationPortRange": "8080",
  "destinationPortRanges": [],
  "direction": "Inbound",
  "etag": "W/\"9198980a-2e94-45f0-8e54-7dd77b650cd0\"",
  "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity3_DOU/providers/Microsoft.Network/networkSecurityGroups/Activity3NSG/securityRules/NSG-Jenkins-Rule",
  "name": "NSG-Jenkins-Rule",
  "priority": 200,
  "protocol": "*",
  "provisioningState": "Succeeded",
  "resourceGroup": "Activity3_DOU",
  "sourceAddressPrefix": "*",
  "sourceAddressPrefixes": [],
  "sourceApplicationSecurityGroups": null,
  "sourcePortRange": "*",
  "sourcePortRanges": [],
  "type": "Microsoft.Network/networkSecurityGroups/securityRules"
}
---------------------------------------------------------
Adding inbound rule on port 22
{
  "access": "Allow",
  "description": null,
  "destinationAddressPrefix": "*",
  "destinationAddressPrefixes": [],
  "destinationApplicationSecurityGroups": null,
  "destinationPortRange": "22",
  "destinationPortRanges": [],
  "direction": "Inbound",
  "etag": "W/\"b9d3d97b-bbc9-4ac0-85c7-7d98d7915797\"",
  "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity3_DOU/providers/Microsoft.Network/networkSecurityGroups/Activity3NSG/securityRules/Activity3-SSH",
  "name": "Activity3-SSH",
  "priority": 100,
  "protocol": "*",
  "provisioningState": "Succeeded",
  "resourceGroup": "Activity3_DOU",
  "sourceAddressPrefix": "*",
  "sourceAddressPrefixes": [],
  "sourceApplicationSecurityGroups": null,
  "sourcePortRange": "*",
  "sourcePortRanges": [],
  "type": "Microsoft.Network/networkSecurityGroups/securityRules"
}
---------------------------------------------------------
Creating a Load Balancer
{
  "loadBalancer": {
    "backendAddressPools": [
      {
        "etag": "W/\"a013252a-9dbd-4f55-9ee9-c12afe473592\"",
        "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity3_DOU/providers/Microsoft.Network/loadBalancers/Activity3-Load-Balancer/backendAddressPools/BackEndPool",
        "name": "BackEndPool",
        "properties": {
          "loadBalancerBackendAddresses": [],
          "provisioningState": "Succeeded"
        },
        "resourceGroup": "Activity3_DOU",
        "type": "Microsoft.Network/loadBalancers/backendAddressPools"
      }
    ],
    "frontendIPConfigurations": [
      {
        "etag": "W/\"a013252a-9dbd-4f55-9ee9-c12afe473592\"",
        "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity3_DOU/providers/Microsoft.Network/loadBalancers/Activity3-Load-Balancer/frontendIPConfigurations/FrontEnd",
        "name": "FrontEnd",
        "properties": {
          "privateIPAllocationMethod": "Dynamic",
          "provisioningState": "Succeeded",
          "publicIPAddress": {
            "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity3_DOU/providers/Microsoft.Network/publicIPAddresses/Activity3Jenkins",
            "resourceGroup": "Activity3_DOU"
          }
        },
        "resourceGroup": "Activity3_DOU",
        "type": "Microsoft.Network/loadBalancers/frontendIPConfigurations"
      }
    ],
    "inboundNatPools": [],
    "inboundNatRules": [],
    "loadBalancingRules": [],
    "outboundRules": [],
    "probes": [],
    "provisioningState": "Succeeded",
    "resourceGuid": "535c426c-5319-40cc-82c0-36f9048c4266"
  }
}
---------------------------------------------------------
Creating a Health probe
{
  "etag": "W/\"02f0ba5c-c1b3-43db-b3ec-b8ce38d8c27a\"",
  "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity3_DOU/providers/Microsoft.Network/loadBalancers/Activity3-Load-Balancer/probes/Activity3-Probe-Health",
  "intervalInSeconds": 15,
  "loadBalancingRules": null,
  "name": "Activity3-Probe-Health",
  "numberOfProbes": 2,
  "port": 8080,
  "protocol": "Tcp",
  "provisioningState": "Succeeded",
  "requestPath": null,
  "resourceGroup": "Activity3_DOU",
  "type": "Microsoft.Network/loadBalancers/probes"
}
---------------------------------------------------------
Creating a Load balancer Rule
{
  "backendAddressPool": {
    "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity3_DOU/providers/Microsoft.Network/loadBalancers/Activity3-Load-Balancer/backendAddressPools/BackEndPool",
    "resourceGroup": "Activity3_DOU"
  },
  "backendAddressPools": [
    {
      "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity3_DOU/providers/Microsoft.Network/loadBalancers/Activity3-Load-Balancer/backendAddressPools/BackEndPool",
      "resourceGroup": "Activity3_DOU"
    }
  ],
  "backendPort": 8080,
  "disableOutboundSnat": false,
  "enableFloatingIp": false,
  "enableTcpReset": false,
  "etag": "W/\"655937f9-eccc-4611-afd9-3698da56df67\"",
  "frontendIpConfiguration": {
    "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity3_DOU/providers/Microsoft.Network/loadBalancers/Activity3-Load-Balancer/frontendIPConfigurations/FrontEnd",
    "resourceGroup": "Activity3_DOU"
  },
  "frontendPort": 8080,
  "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity3_DOU/providers/Microsoft.Network/loadBalancers/Activity3-Load-Balancer/loadBalancingRules/LoadB-Rule",
  "idleTimeoutInMinutes": 4,
  "loadDistribution": "Default",
  "name": "LoadB-Rule",
  "probe": {
    "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity3_DOU/providers/Microsoft.Network/loadBalancers/Activity3-Load-Balancer/probes/Activity3-Probe-Health",
    "resourceGroup": "Activity3_DOU"
  },
  "protocol": "Tcp",
  "provisioningState": "Succeeded",
  "resourceGroup": "Activity3_DOU",
  "type": "Microsoft.Network/loadBalancers/loadBalancingRules"
}
----------------------------
Creating Network Interface
----------------------------
{
  "NewNIC": {
    "dnsSettings": {
      "appliedDnsServers": [],
      "dnsServers": [],
      "internalDnsNameLabel": null,
      "internalDomainNameSuffix": "a2qlj41p0n5uheloznc1r2wv4c.gx.internal.cloudapp.net",
      "internalFqdn": null
    },
    "dscpConfiguration": null,
    "enableAcceleratedNetworking": false,
    "enableIpForwarding": true,
    "etag": "W/\"c8a07605-ff4f-4a07-97f5-5464225b178f\"",
    "extendedLocation": null,
    "hostedWorkloads": [],
    "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity3_DOU/providers/Microsoft.Network/networkInterfaces/activity3-nic-1",
    "ipConfigurations": [
      {
        "applicationGatewayBackendAddressPools": null,
        "applicationSecurityGroups": null,
        "etag": "W/\"c8a07605-ff4f-4a07-97f5-5464225b178f\"",
        "gatewayLoadBalancer": null,
        "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity3_DOU/providers/Microsoft.Network/networkInterfaces/activity3-nic-1/ipConfigurations/ipconfig1",
        "loadBalancerBackendAddressPools": [
          {
            "backendIpConfigurations": null,
            "etag": null,
            "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity3_DOU/providers/Microsoft.Network/loadBalancers/Activity3-Load-Balancer/backendAddressPools/BackEndPool",
            "loadBalancerBackendAddresses": null,
            "loadBalancingRules": null,
            "location": null,
            "name": null,
            "outboundRule": null,
            "outboundRules": null,
            "provisioningState": null,
            "resourceGroup": "Activity3_DOU",
            "tunnelInterfaces": null,
            "type": null
          }
        ],
        "loadBalancerInboundNatRules": null,
        "name": "ipconfig1",
        "primary": true,
        "privateIpAddress": "10.0.0.4",
        "privateIpAddressVersion": "IPv4",
        "privateIpAllocationMethod": "Dynamic",
        "privateLinkConnectionProperties": null,
        "provisioningState": "Succeeded",
        "publicIpAddress": null,
        "resourceGroup": "Activity3_DOU",
        "subnet": {
          "addressPrefix": null,
          "addressPrefixes": null,
          "applicationGatewayIpConfigurations": null,
          "delegations": null,
          "etag": null,
          "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity3_DOU/providers/Microsoft.Network/virtualNetworks/Activity3-VN/subnets/Activity3_SubNet",
          "ipAllocations": null,
          "ipConfigurationProfiles": null,
          "ipConfigurations": null,
          "name": null,
          "natGateway": null,
          "networkSecurityGroup": null,
          "privateEndpointNetworkPolicies": null,
          "privateEndpoints": null,
          "privateLinkServiceNetworkPolicies": null,
          "provisioningState": null,
          "purpose": null,
          "resourceGroup": "Activity3_DOU",
          "resourceNavigationLinks": null,
          "routeTable": null,
          "serviceAssociationLinks": null,
          "serviceEndpointPolicies": null,
          "serviceEndpoints": null,
          "type": null
        },
        "type": "Microsoft.Network/networkInterfaces/ipConfigurations",
        "virtualNetworkTaps": null
      }
    ],
    "location": "centralus",
    "macAddress": null,
    "migrationPhase": null,
    "name": "activity3-nic-1",
    "networkSecurityGroup": {
      "defaultSecurityRules": null,
      "etag": null,
      "flowLogs": null,
      "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity3_DOU/providers/Microsoft.Network/networkSecurityGroups/Activity3NSG",
      "location": null,
      "name": null,
      "networkInterfaces": null,
      "provisioningState": null,
      "resourceGroup": "Activity3_DOU",
      "resourceGuid": null,
      "securityRules": null,
      "subnets": null,
      "tags": null,
      "type": null
    },
    "nicType": "Standard",
    "primary": null,
    "privateEndpoint": null,
    "privateLinkService": null,
    "provisioningState": "Succeeded",
    "resourceGroup": "Activity3_DOU",
    "resourceGuid": "2fa411fc-9196-4209-bce3-dae760c58250",
    "tags": null,
    "tapConfigurations": [],
    "type": "Microsoft.Network/networkInterfaces",
    "virtualMachine": null,
    "workloadType": null
  }
}
----------------------------
Creating Virtual Machine
----------------------------
It is recommended to use parameter "--public-ip-sku Standard" to create new VM with Standard public IP. Please note that the default public IP used for VM creation will be changed from Basic to Standard in the future.
{
  "fqdns": "",
  "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity3_DOU/providers/Microsoft.Compute/virtualMachines/activity3-vm-1",
  "location": "centralus",
  "macAddress": "00-0D-3A-9E-EA-45",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "",
  "resourceGroup": "Activity3_DOU",
  "zones": ""
}
----------------------------
Creating Network Interface
----------------------------
{
  "NewNIC": {
    "dnsSettings": {
      "appliedDnsServers": [],
      "dnsServers": [],
      "internalDnsNameLabel": null,
      "internalDomainNameSuffix": "a2qlj41p0n5uheloznc1r2wv4c.gx.internal.cloudapp.net",
      "internalFqdn": null
    },
    "dscpConfiguration": null,
    "enableAcceleratedNetworking": false,
    "enableIpForwarding": true,
    "etag": "W/\"3ea67760-9c1c-46e0-867d-70dc6ae782eb\"",
    "extendedLocation": null,
    "hostedWorkloads": [],
    "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity3_DOU/providers/Microsoft.Network/networkInterfaces/activity3-nic-2",
    "ipConfigurations": [
      {
        "applicationGatewayBackendAddressPools": null,
        "applicationSecurityGroups": null,
        "etag": "W/\"3ea67760-9c1c-46e0-867d-70dc6ae782eb\"",
        "gatewayLoadBalancer": null,
        "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity3_DOU/providers/Microsoft.Network/networkInterfaces/activity3-nic-2/ipConfigurations/ipconfig1",
        "loadBalancerBackendAddressPools": [
          {
            "backendIpConfigurations": null,
            "etag": null,
            "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity3_DOU/providers/Microsoft.Network/loadBalancers/Activity3-Load-Balancer/backendAddressPools/BackEndPool",
            "loadBalancerBackendAddresses": null,
            "loadBalancingRules": null,
            "location": null,
            "name": null,
            "outboundRule": null,
            "outboundRules": null,
            "provisioningState": null,
            "resourceGroup": "Activity3_DOU",
            "tunnelInterfaces": null,
            "type": null
          }
        ],
        "loadBalancerInboundNatRules": null,
        "name": "ipconfig1",
        "primary": true,
        "privateIpAddress": "10.0.0.5",
        "privateIpAddressVersion": "IPv4",
        "privateIpAllocationMethod": "Dynamic",
        "privateLinkConnectionProperties": null,
        "provisioningState": "Succeeded",
        "publicIpAddress": null,
        "resourceGroup": "Activity3_DOU",
        "subnet": {
          "addressPrefix": null,
          "addressPrefixes": null,
          "applicationGatewayIpConfigurations": null,
          "delegations": null,
          "etag": null,
          "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity3_DOU/providers/Microsoft.Network/virtualNetworks/Activity3-VN/subnets/Activity3_SubNet",
          "ipAllocations": null,
          "ipConfigurationProfiles": null,
          "ipConfigurations": null,
          "name": null,
          "natGateway": null,
          "networkSecurityGroup": null,
          "privateEndpointNetworkPolicies": null,
          "privateEndpoints": null,
          "privateLinkServiceNetworkPolicies": null,
          "provisioningState": null,
          "purpose": null,
          "resourceGroup": "Activity3_DOU",
          "resourceNavigationLinks": null,
          "routeTable": null,
          "serviceAssociationLinks": null,
          "serviceEndpointPolicies": null,
          "serviceEndpoints": null,
          "type": null
        },
        "type": "Microsoft.Network/networkInterfaces/ipConfigurations",
        "virtualNetworkTaps": null
      }
    ],
    "location": "centralus",
    "macAddress": null,
    "migrationPhase": null,
    "name": "activity3-nic-2",
    "networkSecurityGroup": {
      "defaultSecurityRules": null,
      "etag": null,
      "flowLogs": null,
      "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity3_DOU/providers/Microsoft.Network/networkSecurityGroups/Activity3NSG",
      "location": null,
      "name": null,
      "networkInterfaces": null,
      "provisioningState": null,
      "resourceGroup": "Activity3_DOU",
      "resourceGuid": null,
      "securityRules": null,
      "subnets": null,
      "tags": null,
      "type": null
    },
    "nicType": "Standard",
    "primary": null,
    "privateEndpoint": null,
    "privateLinkService": null,
    "provisioningState": "Succeeded",
    "resourceGroup": "Activity3_DOU",
    "resourceGuid": "0f28cd43-e6e4-489b-8763-55cfc1d98a40",
    "tags": null,
    "tapConfigurations": [],
    "type": "Microsoft.Network/networkInterfaces",
    "virtualMachine": null,
    "workloadType": null
  }
}
----------------------------
Creating Virtual Machine
----------------------------
It is recommended to use parameter "--public-ip-sku Standard" to create new VM with Standard public IP. Please note that the default public IP used for VM creation will be changed from Basic to Standard in the future.
{
  "fqdns": "",
  "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity3_DOU/providers/Microsoft.Compute/virtualMachines/activity3-vm-2",
  "location": "centralus",
  "macAddress": "00-0D-3A-9F-5D-E4",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.5",
  "publicIpAddress": "",
  "resourceGroup": "Activity3_DOU",
  "zones": ""
}
```

**These are all my resources created on Azure portal after the script execution**

![Screen Shot 2021-10-05 at 10.35.07.png](First%20Azure%20Infrastructure%204565bb7683fa4b3ba8d66e54e8df5342/Screen_Shot_2021-10-05_at_10.35.07.png)

**This is Jenkins tools working after the installation**

![Screen Shot 2021-10-05 at 10.37.47.png](First%20Azure%20Infrastructure%204565bb7683fa4b3ba8d66e54e8df5342/Screen_Shot_2021-10-05_at_10.37.47.png)

```bash
# Installation
genaroparedes@activity3-vm-1:~$ wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
OK
genaroparedes@activity3-vm-1:~$ sudo sh -c 'echo deb https://pkg.jenkins.io/debian-stable binary/ > \
>     /etc/apt/sources.list.d/jenkins.list'
genaroparedes@activity3-vm-1:~$ sudo apt-get update
Hit:1 http://azure.archive.ubuntu.com/ubuntu bionic InRelease
Hit:2 http://azure.archive.ubuntu.com/ubuntu bionic-updates InRelease
Hit:3 http://azure.archive.ubuntu.com/ubuntu bionic-backports InRelease
Hit:4 http://security.ubuntu.com/ubuntu bionic-security InRelease
Ign:5 https://pkg.jenkins.io/debian-stable binary/ InRelease
Get:6 https://pkg.jenkins.io/debian-stable binary/ Release [2044 B]
Get:7 https://pkg.jenkins.io/debian-stable binary/ Release.gpg [833 B]
Get:8 https://pkg.jenkins.io/debian-stable binary/ Packages [20.6 kB]
Fetched 23.4 kB in 1s (37.0 kB/s)  
Reading package lists... Done
genaroparedes@activity3-vm-1:~$ sudo apt-get install jenkins
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following package was automatically installed and is no longer required:
  linux-headers-4.15.0-159
Use 'sudo apt autoremove' to remove it.
The following additional packages will be installed:
  daemon
The following NEW packages will be installed:
  daemon jenkins
0 upgraded, 2 newly installed, 0 to remove and 3 not upgraded.
Need to get 69.8 MB of archives.
After this operation, 72.6 MB of additional disk space will be used.
Do you want to continue? [Y/n] y
Get:1 http://azure.archive.ubuntu.com/ubuntu bionic/universe amd64 daemon amd64 0.6.4-1build1 [99.5 kB]
Get:2 https://pkg.jenkins.io/debian-stable binary/ jenkins 2.303.1 [69.7 MB]     
Fetched 69.8 MB in 8s (8403 kB/s)                                                  
Selecting previously unselected package daemon.
(Reading database ... 79834 files and directories currently installed.)
Preparing to unpack .../daemon_0.6.4-1build1_amd64.deb ...
Unpacking daemon (0.6.4-1build1) ...
Selecting previously unselected package jenkins.
Preparing to unpack .../jenkins_2.303.1_all.deb ...
Unpacking jenkins (2.303.1) ...
Setting up daemon (0.6.4-1build1) ...
Setting up jenkins (2.303.1) ...
Processing triggers for systemd (237-3ubuntu10.52) ...
Processing triggers for man-db (2.8.3-2ubuntu0.1) ...
Processing triggers for ureadahead (0.100.0-21) ...
genaroparedes@activity3-vm-1:~$ sudo systemctl daemon-reload
genaroparedes@activity3-vm-1:~$ sudo systemctl start jenkins
genaroparedes@activity3-vm-1:~$ sudo systemctl status jenkins
● jenkins.service - LSB: Start Jenkins at boot time
   Loaded: loaded (/etc/init.d/jenkins; generated)
   Active: active (exited) since Tue 2021-10-05 15:12:04 UTC; 1min 14s ago
     Docs: man:systemd-sysv-generator(8)
    Tasks: 0 (limit: 4074)
   CGroup: /system.slice/jenkins.service

Oct 05 15:12:03 activity3-vm-1 systemd[1]: Starting LSB: Start Jenkins at boot time.
Oct 05 15:12:03 activity3-vm-1 jenkins[9402]: Correct java version found
Oct 05 15:12:03 activity3-vm-1 jenkins[9402]:  * Starting Jenkins Automation Server 
Oct 05 15:12:03 activity3-vm-1 su[9457]: Successful su for jenkins by root
Oct 05 15:12:03 activity3-vm-1 su[9457]: + ??? root:jenkins
Oct 05 15:12:03 activity3-vm-1 su[9457]: pam_unix(su:session): session opened for us
Oct 05 15:12:03 activity3-vm-1 su[9457]: pam_unix(su:session): session closed for us
Oct 05 15:12:04 activity3-vm-1 jenkins[9402]:    ...done.
Oct 05 15:12:04 activity3-vm-1 systemd[1]: Started LSB: Start Jenkins at boot time.
```

**Load Balancer proof, IP public address from screenshot and load balancer are the same**

![Screen Shot 2021-10-05 at 10.44.42.png](First%20Azure%20Infrastructure%204565bb7683fa4b3ba8d66e54e8df5342/Screen_Shot_2021-10-05_at_10.44.42.png)

**Both of the prompt after logging using SSH**

![Screen Shot 2021-10-05 at 9.04.59.png](First%20Azure%20Infrastructure%204565bb7683fa4b3ba8d66e54e8df5342/Screen_Shot_2021-10-05_at_9.04.59.png)

![Screen Shot 2021-10-05 at 9.42.24.png](First%20Azure%20Infrastructure%204565bb7683fa4b3ba8d66e54e8df5342/Screen_Shot_2021-10-05_at_9.42.24.png)

***DELETING ALL MY RESOURCES***

![Screen Shot 2021-10-05 at 10.48.27.png](First%20Azure%20Infrastructure%204565bb7683fa4b3ba8d66e54e8df5342/Screen_Shot_2021-10-05_at_10.48.27.png)