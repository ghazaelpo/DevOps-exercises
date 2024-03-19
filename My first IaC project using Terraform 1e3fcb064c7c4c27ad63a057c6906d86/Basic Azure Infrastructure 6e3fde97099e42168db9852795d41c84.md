# Basic Azure Infrastructure

### Instructions

1. Create file `main.tf` and include the following resources:
    
    Git project:
    
    [https://gitlab.com/genarop/basic-azure-infra](https://gitlab.com/genarop/basic-azure-infra)
    
    - azurerm_virtual_machine
    
    ```bash
    #main.tf
    provider "azurerm" {
      features {}
    }
    
    resource "azurerm_resource_group" "example" {
      name     = "${var.prefix}-resources"
      location = var.location
    }
    
    resource "azurerm_virtual_network" "example" {
      name                = "${var.prefix}-vnet"
      location            = azurerm_resource_group.example.location
      resource_group_name = azurerm_resource_group.example.name
      address_space       = ["10.0.0.0/16"]
    }
    
    resource "azurerm_subnet" "internal" {
      name                 = "internal"
      resource_group_name  = azurerm_resource_group.example.name
      virtual_network_name = azurerm_virtual_network.example.name
      address_prefixes     = ["10.0.2.0/24"]
    }
    
    resource "azurerm_public_ip" "example" {
      name                = "${var.prefix}-pip"
      location            = azurerm_resource_group.example.location
      resource_group_name = azurerm_resource_group.example.name
      allocation_method   = "Static"
      sku                 = "Standard"
    }
    
    resource "azurerm_network_interface" "main" {
      name                = "${var.prefix}-nic1"
      resource_group_name = azurerm_resource_group.example.name
      location            = azurerm_resource_group.example.location
    
      ip_configuration {
        name                          = "primary"
        subnet_id                     = azurerm_subnet.internal.id
        private_ip_address_allocation = "Dynamic"
        public_ip_address_id          = azurerm_public_ip.example.id
      }
    }
    
    resource "azurerm_network_interface" "internal" {
      name                      = "${var.prefix}-nic2"
      resource_group_name       = azurerm_resource_group.example.name
      location                  = azurerm_resource_group.example.location
    
      ip_configuration {
        name                          = "internal"
        subnet_id                     = azurerm_subnet.internal.id
        private_ip_address_allocation = "Dynamic"
      }
    }
    
    resource "azurerm_network_security_group" "webserver" {
      name                = "tls_webserver"
      location            = azurerm_resource_group.example.location
      resource_group_name = azurerm_resource_group.example.name
      security_rule {
        access                     = "Allow"
        direction                  = "Inbound"
        name                       = "tls"
        priority                   = 200
        protocol                   = "Tcp"
        source_port_range          = "*"
        source_address_prefix      = "*"
        destination_port_range     = "22"
        destination_address_prefix = azurerm_network_interface.main.private_ip_address
      }
    }
    
    resource "azurerm_network_interface_security_group_association" "main" {
      network_interface_id      = azurerm_network_interface.internal.id
      network_security_group_id = azurerm_network_security_group.webserver.id
    }
    
    resource "azurerm_network_interface_security_group_association" "main2" {
      network_interface_id      = azurerm_network_interface.main.id
      network_security_group_id = azurerm_network_security_group.webserver.id
    }
    
    resource "azurerm_linux_virtual_machine" "main" {
      name                            = "${var.prefix}-vm"
      resource_group_name             = azurerm_resource_group.example.name
      location                        = azurerm_resource_group.example.location
      size                            = "Standard_F2"
      admin_username                  = "adminuser"
      admin_password                  = "Password1234!"
      disable_password_authentication = false
      network_interface_ids = [
        azurerm_network_interface.main.id,
        azurerm_network_interface.internal.id,
      ]
    
      source_image_reference {
        publisher = "Canonical"
        offer     = "UbuntuServer"
        sku       = "18.04-LTS"
        version   = "latest"
      }
    
      os_disk {
        storage_account_type = "Standard_LRS"
        caching              = "ReadWrite"
      }
    }
    
    resource "azurerm_route_table" "example" {
      name                = "example-routetable"
      location            = azurerm_resource_group.example.location
      resource_group_name = azurerm_resource_group.example.name
    
      route {
        name                   = "example"
        address_prefix         = "10.100.0.0/14"
        next_hop_type          = "VirtualAppliance"
        next_hop_in_ip_address = "10.10.1.1"
      }
    }
    
    resource "azurerm_route" "example" {
      name                = "acceptanceTestRoute1"
      resource_group_name = azurerm_resource_group.example.name
      route_table_name    = azurerm_route_table.example.name
      address_prefix      = "10.1.0.0/16"
      next_hop_type       = "vnetlocal"
    }
    
    resource "azurerm_subnet_route_table_association" "example" {
      subnet_id      = azurerm_subnet.internal.id
      route_table_id = azurerm_route_table.example.id
    }
    
    resource "azurerm_ssh_public_key" "example" {
      name                = "genaro-sshk"
      resource_group_name = azurerm_resource_group.example.name
      location            = azurerm_resource_group.example.location
      public_key          = file("~/.ssh/id_rsa.pub")
    }
    ```
    
    Connected through SSH
    
    ![Screen Shot 2021-10-18 at 19.07.39.png](Basic%20Azure%20Infrastructure%206e3fde97099e42168db9852795d41c84/Screen_Shot_2021-10-18_at_19.07.39.png)
    
    Resources deployed
    
    ![Screen Shot 2021-10-18 at 19.09.17.png](Basic%20Azure%20Infrastructure%206e3fde97099e42168db9852795d41c84/Screen_Shot_2021-10-18_at_19.09.17.png)