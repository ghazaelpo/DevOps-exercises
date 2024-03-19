# Creating a Virtual Machine

In this example we will create a virtual machine using Azure CLI

```bash
# For this case we will create the virtual machine using a RedHat image
# We can consult images availables using the below command
# az vm image list 
# --publisher flag, use to filter by images creator
genaroparedes@GenaroParedes-MacBook-Pro ~ % az vm image list --publisher RedHat --all --output table

# To create a virtual machine is neccesary use the below command...
# and add some flags to complete successfully 

# The general form is:
# az vm create --resource-group YOUR_RESOURCEGROUPNAME --name YOUR_VIRTUALMACHINENAME --image YOUR_CHOICE_NAMEIMAGE --admin-username YOUR_CHOICE_USERNAME --generate-ssh-keys
# It is recommended to use parameter "--public-ip-sku Standard" to create new VM with Standard public IP. Please note that the default public IP used for VM creation will be changed from Basic to Standard in the future.

genaroparedes@GenaroParedes-MacBook-Pro ~ % az vm create --resource-group Activity2_DOU --name exampleVM --image RedHat:RHEL:7-LVM:latest --admin-username genaro --generate-ssh-keys
{
  "fqdns": "",
  "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity2_DOU/providers/Microsoft.Compute/virtualMachines/exampleVM",
  "location": "centralus",
  "macAddress": "00-22-48-46-37-CD",
  "powerState": "VM running",
  "privateIpAddress": "10.1.0.5",
  "publicIpAddress": "104.43.135.83",
  "resourceGroup": "Activity2_DOU",
  "zones": ""
}
genaroparedes@GenaroParedes-MacBook-Pro
```

![Screen Shot 2021-10-02 at 15.36.09.png](Creating%20a%20Virtual%20Machine%2034695dcc34ab4036b911a8a13b83c7dc/Screen_Shot_2021-10-02_at_15.36.09.png)

After the image has been built we can see the Virtual Machine created on Azure Portal

![Screen Shot 2021-10-02 at 15.54.27.png](Creating%20a%20Virtual%20Machine%2034695dcc34ab4036b911a8a13b83c7dc/Screen_Shot_2021-10-02_at_15.54.27.png)

**Open port 80 for web traffic**

```bash
# Opening port to be able to use and access to nginx
# The command is az vm open-port --port xx --resource-group ResourceName --name VirtualMachine
genaroparedes@GenaroParedes-MacBook-Pro ~ % az vm open-port --port 80 --resource-group Activity2_DOU --name exampleVM
{
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
      "etag": "W/\"4ee8fffc-3d9e-48f0-9136-1578eb55adc0\"",
      "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity2_DOU/providers/Microsoft.Network/networkSecurityGroups/exampleVMNSG/defaultSecurityRules/AllowVnetInBound",
      "name": "AllowVnetInBound",
      "priority": 65000,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "Activity2_DOU",
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
      "etag": "W/\"4ee8fffc-3d9e-48f0-9136-1578eb55adc0\"",
      "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity2_DOU/providers/Microsoft.Network/networkSecurityGroups/exampleVMNSG/defaultSecurityRules/AllowAzureLoadBalancerInBound",
      "name": "AllowAzureLoadBalancerInBound",
      "priority": 65001,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "Activity2_DOU",
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
      "etag": "W/\"4ee8fffc-3d9e-48f0-9136-1578eb55adc0\"",
      "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity2_DOU/providers/Microsoft.Network/networkSecurityGroups/exampleVMNSG/defaultSecurityRules/DenyAllInBound",
      "name": "DenyAllInBound",
      "priority": 65500,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "Activity2_DOU",
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
      "etag": "W/\"4ee8fffc-3d9e-48f0-9136-1578eb55adc0\"",
      "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity2_DOU/providers/Microsoft.Network/networkSecurityGroups/exampleVMNSG/defaultSecurityRules/AllowVnetOutBound",
      "name": "AllowVnetOutBound",
      "priority": 65000,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "Activity2_DOU",
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
      "etag": "W/\"4ee8fffc-3d9e-48f0-9136-1578eb55adc0\"",
      "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity2_DOU/providers/Microsoft.Network/networkSecurityGroups/exampleVMNSG/defaultSecurityRules/AllowInternetOutBound",
      "name": "AllowInternetOutBound",
      "priority": 65001,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "Activity2_DOU",
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
      "etag": "W/\"4ee8fffc-3d9e-48f0-9136-1578eb55adc0\"",
      "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity2_DOU/providers/Microsoft.Network/networkSecurityGroups/exampleVMNSG/defaultSecurityRules/DenyAllOutBound",
      "name": "DenyAllOutBound",
      "priority": 65500,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "Activity2_DOU",
      "sourceAddressPrefix": "*",
      "sourceAddressPrefixes": [],
      "sourceApplicationSecurityGroups": null,
      "sourcePortRange": "*",
      "sourcePortRanges": [],
      "type": "Microsoft.Network/networkSecurityGroups/defaultSecurityRules"
    }
  ],
  "etag": "W/\"4ee8fffc-3d9e-48f0-9136-1578eb55adc0\"",
  "flowLogs": null,
  "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity2_DOU/providers/Microsoft.Network/networkSecurityGroups/exampleVMNSG",
  "location": "centralus",
  "name": "exampleVMNSG",
  "networkInterfaces": [
    {
      "dnsSettings": null,
      "dscpConfiguration": null,
      "enableAcceleratedNetworking": null,
      "enableIpForwarding": null,
      "etag": null,
      "extendedLocation": null,
      "hostedWorkloads": null,
      "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity2_DOU/providers/Microsoft.Network/networkInterfaces/exampleVMVMNic",
      "ipConfigurations": null,
      "location": null,
      "macAddress": null,
      "migrationPhase": null,
      "name": null,
      "networkSecurityGroup": null,
      "nicType": null,
      "primary": null,
      "privateEndpoint": null,
      "privateLinkService": null,
      "provisioningState": null,
      "resourceGroup": "Activity2_DOU",
      "resourceGuid": null,
      "tags": null,
      "tapConfigurations": null,
      "type": null,
      "virtualMachine": null,
      "workloadType": null
    }
  ],
  "provisioningState": "Succeeded",
  "resourceGroup": "Activity2_DOU",
  "resourceGuid": "dcaa11b7-4bd1-486d-9daa-021f026554dc",
  "securityRules": [
    {
      "access": "Allow",
      "description": null,
      "destinationAddressPrefix": "*",
      "destinationAddressPrefixes": [],
      "destinationApplicationSecurityGroups": null,
      "destinationPortRange": "22",
      "destinationPortRanges": [],
      "direction": "Inbound",
      "etag": "W/\"4ee8fffc-3d9e-48f0-9136-1578eb55adc0\"",
      "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity2_DOU/providers/Microsoft.Network/networkSecurityGroups/exampleVMNSG/securityRules/default-allow-ssh",
      "name": "default-allow-ssh",
      "priority": 1000,
      "protocol": "Tcp",
      "provisioningState": "Succeeded",
      "resourceGroup": "Activity2_DOU",
      "sourceAddressPrefix": "*",
      "sourceAddressPrefixes": [],
      "sourceApplicationSecurityGroups": null,
      "sourcePortRange": "*",
      "sourcePortRanges": [],
      "type": "Microsoft.Network/networkSecurityGroups/securityRules"
    },
    {
      "access": "Allow",
      "description": null,
      "destinationAddressPrefix": "*",
      "destinationAddressPrefixes": [],
      "destinationApplicationSecurityGroups": null,
      "destinationPortRange": "80",
      "destinationPortRanges": [],
      "direction": "Inbound",
      "etag": "W/\"4ee8fffc-3d9e-48f0-9136-1578eb55adc0\"",
      "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity2_DOU/providers/Microsoft.Network/networkSecurityGroups/exampleVMNSG/securityRules/open-port-80",
      "name": "open-port-80",
      "priority": 900,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "Activity2_DOU",
      "sourceAddressPrefix": "*",
      "sourceAddressPrefixes": [],
      "sourceApplicationSecurityGroups": null,
      "sourcePortRange": "*",
      "sourcePortRanges": [],
      "type": "Microsoft.Network/networkSecurityGroups/securityRules"
    }
  ],
  "subnets": null,
  "tags": {},
  "type": "Microsoft.Network/networkSecurityGroups"
}
```

## Installing NGINX

Once we have built the Virtual Machine is necessary install NGINX server to complete all the requirements for this activity. 

To install this service first we have to connect to our Virtual Machine and in this case we will connect through SSH key. So we start creating it and then connect to the VM to proceed to install nginx.

```bash
# Generate the SSH key
genaroparedes@GenaroParedes-MacBook-Pro ~ % ssh-keygen -t rsa -b 2048
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/genaroparedes/.ssh/id_rsa): /Users/genaroparedes/.ssh/VMkey
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /Users/genaroparedes/.ssh/VMkey.
Your public key has been saved in /Users/genaroparedes/.ssh/VMkey.pub.
The key fingerprint is:
SHA256:lIVSWZ3bbSeVzmVnrT0Dmrb6aP9VjmiH36GlZhomJGE genaroparedes@GenaroParedes-MacBook-Pro.local
The key\'s randomart image is:
+---[RSA 2048]----+
|       ..+o. .  o|
|      . oo  o. .B|
|       Eo   oo+Bo|
|      ...  +. +==|
|       .S.. .  o=|
|        o  . o o.|
|         ..o+ o+.|
|         o+..==..|
|        ..o+=+. .|
+----[SHA256]-----+

#Install the SSH key 
genaroparedes@GenaroParedes-MacBook-Pro .ssh % ssh-copy-id -i VMkey.pub genaro@104.43.135.83
/usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "VMkey.pub"
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
/etc/profile.d/lang.sh: line 19: warning: setlocale: LC_CTYPE: cannot change locale (UTF-8): No such file or directory

Number of key(s) added:        1

Now try logging into the machine, with:   "ssh 'genaro@104.43.135.83'"
and check to make sure that only the key(s) you wanted were added.

# Trying to connect using generated key 
genaroparedes@GenaroParedes-MacBook-Pro .ssh % ssh -i VMkey genaro@104.43.135.83
Last login: Sat Oct  2 22:34:27 2021 from 187.172.92.38
-bash: warning: setlocale: LC_CTYPE: cannot change locale (UTF-8): No such file or directory
[genaro@exampleVM ~]$
```

Now we can proceed to install nginx and modify the html path

```bash
# First we have to created a file with the repo where we will download nginx
[genaro@exampleVM ~]$ sudo vim /etc/yum.repos.d/nginx.repo
[genaro@exampleVM ~]$ sudo cat /etc/yum.repos.d/nginx.repo
[nginx]
name=nginx repo
baseurl=http://nginx.org/packages/mainline/centos/7/$basearch/
gpgcheck=0
enabled=1

# Update all the packcages using 
[genaro@exampleVM ~]$ sudo yum update -y

# Then just install nginx and wait
[genaro@exampleVM ~]$ sudo yum -y install nginx
Failed to set locale, defaulting to C
Loaded plugins: langpacks, product-id, search-disabled-repos
nginx                                                    | 2.9 kB     00:00     
nginx/x86_64/primary_db                                    | 223 kB   00:00     
Resolving Dependencies
--> Running transaction check
---> Package nginx.x86_64 1:1.21.3-1.el7.ngx will be installed
--> Finished Dependency Resolution

Dependencies Resolved

================================================================================
 Package       Arch           Version                       Repository     Size
================================================================================
Installing:
 nginx         x86_64         1:1.21.3-1.el7.ngx            nginx         792 k

Transaction Summary
================================================================================
Install  1 Package

Total download size: 792 k
Installed size: 2.8 M
Downloading packages:
nginx-1.21.3-1.el7.ngx.x86_64.rpm                          | 792 kB   00:00     
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Installing : 1:nginx-1.21.3-1.el7.ngx.x86_64                              1/1 
----------------------------------------------------------------------

Thanks for using nginx!

Please find the official documentation for nginx here:
* https://nginx.org/en/docs/

Please subscribe to nginx-announce mailing list to get
the most important news about nginx:
* https://nginx.org/en/support.html

Commercial subscriptions for nginx are available on:
* https://nginx.com/products/

----------------------------------------------------------------------
  Verifying  : 1:nginx-1.21.3-1.el7.ngx.x86_64                              1/1 

Installed:
  nginx.x86_64 1:1.21.3-1.el7.ngx                                               

Complete!

# Once nginx has been installed we need start the service
service nginx start
Redirecting to /bin/systemctl start nginx.service
==== AUTHENTICATING FOR org.freedesktop.systemd1.manage-units ===
Authentication is required to manage system services or units.
Authenticating as: root
Password: 
==== AUTHENTICATION COMPLETE ===

# To use nginx in our VM we must allow the ports in the firewall
[genaro@exampleVM ~]$ sudo firewall-cmd --permanent --add-port={80/tcp,443/tcp}
success
[genaro@exampleVM ~]$ sudo firewall-cmd --reload
success
```

**Now all the configuration is ready and we can access to NGINX using using our VM IP address 104.43.135.83, let's try it:**

![Screen Shot 2021-10-02 at 17.58.32.png](Creating%20a%20Virtual%20Machine%2034695dcc34ab4036b911a8a13b83c7dc/Screen_Shot_2021-10-02_at_17.58.32.png)

![giphy.gif](Creating%20a%20Virtual%20Machine%2034695dcc34ab4036b911a8a13b83c7dc/giphy.gif)

## Even I changed the index.html file using a template:

![Screen Shot 2021-10-03 at 0.23.55.png](Creating%20a%20Virtual%20Machine%2034695dcc34ab4036b911a8a13b83c7dc/Screen_Shot_2021-10-03_at_0.23.55.png)

## Install nginx using the custom-data attribute instead of manual commands after launch:

In this case we will install nginx server using the below file and inside this is specified the nginx installation

```bash
genaroparedes@GenaroParedes-MacBook-Pro Documents % vim cloud-init-github.txt
genaroparedes@GenaroParedes-MacBook-Pro Documents % cat cloud-init-github.txt 
#cloud-config
package_upgrade: true
packages:
  - nginx
write_files:
  - owner: www-data:www-data
    path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 80;
        location / {
          proxy_pass http://localhost:3000;
          proxy_http_version 1.1;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection keep-alive;
          proxy_set_header X-Forwarded-For $remote_addr;
          proxy_set_header Host $host;
          proxy_cache_bypass $http_upgrade;
        }
      }
runcmd:
  # install Node.js
  - 'curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -'
  - 'sudo apt-get install -y nodejs'
  # clone GitHub Repo into myapp directory
  - 'cd /home/azureuser'
  - git clone "https://github.com/Azure-Samples/js-e2e-vm" myapp
  # Start app
  - 'cd myapp && npm install && npm start'
  # restart NGINX
  - service nginx restart

########## Creating the virtual machine using custom-data attribute ######### 

genaroparedes@GenaroParedes-MacBook-Pro Documents % az vm create \
  --resource-group Activity2_DOU \    
  --name demo-vm \
  --location eastus \
  --image UbuntuLTS \
  --admin-username genaza \   
  --generate-ssh-keys \
  --custom-data cloud-init-github.txt
It is recommended to use parameter "--public-ip-sku Standard" to create new VM with Standard public IP. Please note that the default public IP used for VM creation will be changed from Basic to Standard in the future.
{
  "fqdns": "",
  "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity2_DOU/providers/Microsoft.Compute/virtualMachines/demo-vm",
  "location": "eastus",
  "macAddress": "00-0D-3A-11-CF-89",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "40.71.98.9",
  "resourceGroup": "Activity2_DOU",
  "zones": ""
}
genaroparedes@GenaroParedes-MacBook-Pro Documents % az vm open-port \
  --port 80 \
  --resource-group Activity2_DOU \    
  --name demo-vm
{
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
      "etag": "W/\"95539b24-47d5-4c51-9208-254de2d31e84\"",
      "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity2_DOU/providers/Microsoft.Network/networkSecurityGroups/demo-vmNSG/defaultSecurityRules/AllowVnetInBound",
      "name": "AllowVnetInBound",
      "priority": 65000,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "Activity2_DOU",
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
      "etag": "W/\"95539b24-47d5-4c51-9208-254de2d31e84\"",
      "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity2_DOU/providers/Microsoft.Network/networkSecurityGroups/demo-vmNSG/defaultSecurityRules/AllowAzureLoadBalancerInBound",
      "name": "AllowAzureLoadBalancerInBound",
      "priority": 65001,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "Activity2_DOU",
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
      "etag": "W/\"95539b24-47d5-4c51-9208-254de2d31e84\"",
      "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity2_DOU/providers/Microsoft.Network/networkSecurityGroups/demo-vmNSG/defaultSecurityRules/DenyAllInBound",
      "name": "DenyAllInBound",
      "priority": 65500,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "Activity2_DOU",
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
      "etag": "W/\"95539b24-47d5-4c51-9208-254de2d31e84\"",
      "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity2_DOU/providers/Microsoft.Network/networkSecurityGroups/demo-vmNSG/defaultSecurityRules/AllowVnetOutBound",
      "name": "AllowVnetOutBound",
      "priority": 65000,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "Activity2_DOU",
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
      "etag": "W/\"95539b24-47d5-4c51-9208-254de2d31e84\"",
      "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity2_DOU/providers/Microsoft.Network/networkSecurityGroups/demo-vmNSG/defaultSecurityRules/AllowInternetOutBound",
      "name": "AllowInternetOutBound",
      "priority": 65001,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "Activity2_DOU",
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
      "etag": "W/\"95539b24-47d5-4c51-9208-254de2d31e84\"",
      "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity2_DOU/providers/Microsoft.Network/networkSecurityGroups/demo-vmNSG/defaultSecurityRules/DenyAllOutBound",
      "name": "DenyAllOutBound",
      "priority": 65500,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "Activity2_DOU",
      "sourceAddressPrefix": "*",
      "sourceAddressPrefixes": [],
      "sourceApplicationSecurityGroups": null,
      "sourcePortRange": "*",
      "sourcePortRanges": [],
      "type": "Microsoft.Network/networkSecurityGroups/defaultSecurityRules"
    }
  ],
  "etag": "W/\"95539b24-47d5-4c51-9208-254de2d31e84\"",
  "flowLogs": null,
  "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity2_DOU/providers/Microsoft.Network/networkSecurityGroups/demo-vmNSG",
  "location": "eastus",
  "name": "demo-vmNSG",
  "networkInterfaces": [
    {
      "dnsSettings": null,
      "dscpConfiguration": null,
      "enableAcceleratedNetworking": null,
      "enableIpForwarding": null,
      "etag": null,
      "extendedLocation": null,
      "hostedWorkloads": null,
      "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity2_DOU/providers/Microsoft.Network/networkInterfaces/demo-vmVMNic",
      "ipConfigurations": null,
      "location": null,
      "macAddress": null,
      "migrationPhase": null,
      "name": null,
      "networkSecurityGroup": null,
      "nicType": null,
      "primary": null,
      "privateEndpoint": null,
      "privateLinkService": null,
      "provisioningState": null,
      "resourceGroup": "Activity2_DOU",
      "resourceGuid": null,
      "tags": null,
      "tapConfigurations": null,
      "type": null,
      "virtualMachine": null,
      "workloadType": null
    }
  ],
  "provisioningState": "Succeeded",
  "resourceGroup": "Activity2_DOU",
  "resourceGuid": "23cd8c70-1948-4dd9-9b38-b60858619645",
  "securityRules": [
    {
      "access": "Allow",
      "description": null,
      "destinationAddressPrefix": "*",
      "destinationAddressPrefixes": [],
      "destinationApplicationSecurityGroups": null,
      "destinationPortRange": "22",
      "destinationPortRanges": [],
      "direction": "Inbound",
      "etag": "W/\"95539b24-47d5-4c51-9208-254de2d31e84\"",
      "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity2_DOU/providers/Microsoft.Network/networkSecurityGroups/demo-vmNSG/securityRules/default-allow-ssh",
      "name": "default-allow-ssh",
      "priority": 1000,
      "protocol": "Tcp",
      "provisioningState": "Succeeded",
      "resourceGroup": "Activity2_DOU",
      "sourceAddressPrefix": "*",
      "sourceAddressPrefixes": [],
      "sourceApplicationSecurityGroups": null,
      "sourcePortRange": "*",
      "sourcePortRanges": [],
      "type": "Microsoft.Network/networkSecurityGroups/securityRules"
    },
    {
      "access": "Allow",
      "description": null,
      "destinationAddressPrefix": "*",
      "destinationAddressPrefixes": [],
      "destinationApplicationSecurityGroups": null,
      "destinationPortRange": "80",
      "destinationPortRanges": [],
      "direction": "Inbound",
      "etag": "W/\"95539b24-47d5-4c51-9208-254de2d31e84\"",
      "id": "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Activity2_DOU/providers/Microsoft.Network/networkSecurityGroups/demo-vmNSG/securityRules/open-port-80",
      "name": "open-port-80",
      "priority": 900,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "Activity2_DOU",
      "sourceAddressPrefix": "*",
      "sourceAddressPrefixes": [],
      "sourceApplicationSecurityGroups": null,
      "sourcePortRange": "*",
      "sourcePortRanges": [],
      "type": "Microsoft.Network/networkSecurityGroups/securityRules"
    }
  ],
  "subnets": null,
  "tags": {},
  "type": "Microsoft.Network/networkSecurityGroups"
}
```

![Screen Shot 2021-10-03 at 17.10.29.png](Creating%20a%20Virtual%20Machine%2034695dcc34ab4036b911a8a13b83c7dc/Screen_Shot_2021-10-03_at_17.10.29.png)