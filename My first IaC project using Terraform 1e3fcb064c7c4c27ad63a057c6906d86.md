# My first IaC project using Terraform

### Create repository for the project

Repository created to proceed, here I will upload all the files from the activity

![Screen Shot 2021-10-13 at 11.05.46.png](My%20first%20IaC%20project%20using%20Terraform%201e3fcb064c7c4c27ad63a057c6906d86/Screen_Shot_2021-10-13_at_11.05.46.png)

[https://gitlab.com/genarop/my-first-iac-project-using-terraform.git](https://gitlab.com/genarop/my-first-iac-project-using-terraform.git)

### Declare the provider and design a simple infrastructure

I'm going to choose Azure as provider

```bash
terraform {
  required_providers {
    azurerm = {
      source = "hashicorp/azurerm"
      version = "2.80.0"
    }
  }
}

provider "azurerm" {
  # Configuration options
}
```

### Create your file structure

```bash
terraform {
  required_providers {
    azurerm = {
      source = "hashicorp/azurerm"
      version = "2.80.0"
    }
  }
}

provider "azurerm" {
  features {}
}

resource "azurerm_resource_group" "example" {
  name     = "example-resources-activity1"
  location = "Central US"
}

resource "azurerm_virtual_network" "example" {
  name                = "example-network"
  address_space       = ["10.0.0.0/16"]
  location            = azurerm_resource_group.example.location
  resource_group_name = azurerm_resource_group.example.name
}

resource "azurerm_subnet" "example" {
  name                 = "internal"
  resource_group_name  = azurerm_resource_group.example.name
  virtual_network_name = azurerm_virtual_network.example.name
  address_prefixes     = ["10.0.2.0/24"]
}

resource "azurerm_network_interface" "example" {
  name                = "example-nic"
  location            = azurerm_resource_group.example.location
  resource_group_name = azurerm_resource_group.example.name

  ip_configuration {
    name                          = "internal"
    subnet_id                     = azurerm_subnet.example.id
    private_ip_address_allocation = "Dynamic"
  }
}

resource "azurerm_linux_virtual_machine" "example" {
  name                = "example-machine"
  resource_group_name = azurerm_resource_group.example.name
  location            = azurerm_resource_group.example.location
  size                = "Standard_F2"
  admin_username      = "adminuser"
  network_interface_ids = [
    azurerm_network_interface.example.id,
  ]

admin_ssh_key {
    username   = "adminuser"
    public_key = file("~/.ssh/id_rsa.pub")
  }

  os_disk {
    caching              = "ReadWrite"
    storage_account_type = "Standard_LRS"
  }

  source_image_reference {
    publisher = "Canonical"
    offer     = "UbuntuServer"
    sku       = "16.04-LTS"
    version   = "latest"
  }
}
```

### Add the resources, providers and all objects that will compose the project

I have decided a linux virtual machine, above I showed the used code, my resources are:

- Azure as provider
- Resource group
- Virtual Network
- OS Disk
- Network Interface
- Virtual Machine

### Validate, Plan, Apply, Destroy

**Validate** 

```bash
GenaroParedes-MacBook-Pro:my-first-iac-project-using-terraform genaroparedes$ terraform validate
Success! The configuration is valid.
```

**Plan**

```bash
GenaroParedes-MacBook-Pro:my-first-iac-project-using-terraform genaroparedes$ terraform plan 

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # azurerm_linux_virtual_machine.example will be created
  + resource "azurerm_linux_virtual_machine" "example" {
      + admin_username                  = "adminuser"
      + allow_extension_operations      = true
      + computer_name                   = (known after apply)
      + disable_password_authentication = true
      + extensions_time_budget          = "PT1H30M"
      + id                              = (known after apply)
      + location                        = "centralus"
      + max_bid_price                   = -1
      + name                            = "example-machine"
      + network_interface_ids           = (known after apply)
      + platform_fault_domain           = -1
      + priority                        = "Regular"
      + private_ip_address              = (known after apply)
      + private_ip_addresses            = (known after apply)
      + provision_vm_agent              = true
      + public_ip_address               = (known after apply)
      + public_ip_addresses             = (known after apply)
      + resource_group_name             = "Act1Terraform-example-resources"
      + size                            = "Standard_F2"
      + virtual_machine_id              = (known after apply)
      + zone                            = (known after apply)

      + admin_ssh_key {
          + public_key = "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDebkNmFZ07hGjKH3ZcrQ0AMEnthsgQE+VXmQ/yOjBrede3wf7+vniwMaDsC9kIlxRCs/sbBig86Q3/g5JhDOpDjEoReraMjLj/fhb1pxEWwUPNZkYbYq5Q4BwgLR9LfnrOTPZoOm3CWAckoxb0OVsHgr8dvdwTfwjjam4bjeELfKtNs49xUmAjfpPVkK3WqJ6YXxxN5XTeG4sV26gDWUAdboY44ohBwBcGN/Vpf0UcyvR0UWgnGVrPJ1PZ3eF3CncwHaCpTLaH7JKOGQafRzIhF9kdXbqwrPAGGiuh276paWJZpSfWZEY3uetx8ZqPu+oyu+B2Qs0oNSow40ln45j3"
          + username   = "adminuser"
        }

      + os_disk {
          + caching                   = "ReadWrite"
          + disk_size_gb              = (known after apply)
          + name                      = (known after apply)
          + storage_account_type      = "Standard_LRS"
          + write_accelerator_enabled = false
        }

      + source_image_reference {
          + offer     = "UbuntuServer"
          + publisher = "Canonical"
          + sku       = "16.04-LTS"
          + version   = "latest"
        }
    }

  # azurerm_network_interface.example will be created
  + resource "azurerm_network_interface" "example" {
      + applied_dns_servers           = (known after apply)
      + dns_servers                   = (known after apply)
      + enable_accelerated_networking = false
      + enable_ip_forwarding          = false
      + id                            = (known after apply)
      + internal_dns_name_label       = (known after apply)
      + internal_domain_name_suffix   = (known after apply)
      + location                      = "centralus"
      + mac_address                   = (known after apply)
      + name                          = "example-nic"
      + private_ip_address            = (known after apply)
      + private_ip_addresses          = (known after apply)
      + resource_group_name           = "Act1Terraform-example-resources"
      + virtual_machine_id            = (known after apply)

      + ip_configuration {
          + name                          = "internal"
          + primary                       = (known after apply)
          + private_ip_address            = (known after apply)
          + private_ip_address_allocation = "dynamic"
          + private_ip_address_version    = "IPv4"
          + subnet_id                     = (known after apply)
        }
    }

  # azurerm_resource_group.example will be created
  + resource "azurerm_resource_group" "example" {
      + id       = (known after apply)
      + location = "centralus"
      + name     = "Act1Terraform-example-resources"
    }

  # azurerm_subnet.example will be created
  + resource "azurerm_subnet" "example" {
      + address_prefix                                 = (known after apply)
      + address_prefixes                               = [
          + "10.0.2.0/24",
        ]
      + enforce_private_link_endpoint_network_policies = false
      + enforce_private_link_service_network_policies  = false
      + id                                             = (known after apply)
      + name                                           = "internal"
      + resource_group_name                            = "Act1Terraform-example-resources"
      + virtual_network_name                           = "example-network"
    }

  # azurerm_virtual_network.example will be created
  + resource "azurerm_virtual_network" "example" {
      + address_space         = [
          + "10.0.0.0/16",
        ]
      + dns_servers           = (known after apply)
      + guid                  = (known after apply)
      + id                    = (known after apply)
      + location              = "centralus"
      + name                  = "example-network"
      + resource_group_name   = "Act1Terraform-example-resources"
      + subnet                = (known after apply)
      + vm_protection_enabled = false
    }

Plan: 5 to add, 0 to change, 0 to destroy.
```

**Apply**

```bash
GenaroParedes-MacBook-Pro:my-first-iac-project-using-terraform genaroparedes$ terraform apply

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # azurerm_linux_virtual_machine.example will be created
  + resource "azurerm_linux_virtual_machine" "example" {
      + admin_username                  = "adminuser"
      + allow_extension_operations      = true
      + computer_name                   = (known after apply)
      + disable_password_authentication = true
      + extensions_time_budget          = "PT1H30M"
      + id                              = (known after apply)
      + location                        = "centralus"
      + max_bid_price                   = -1
      + name                            = "example-machine"
      + network_interface_ids           = (known after apply)
      + platform_fault_domain           = -1
      + priority                        = "Regular"
      + private_ip_address              = (known after apply)
      + private_ip_addresses            = (known after apply)
      + provision_vm_agent              = true
      + public_ip_address               = (known after apply)
      + public_ip_addresses             = (known after apply)
      + resource_group_name             = "Act1Terraform-example-resources"
      + size                            = "Standard_F2"
      + virtual_machine_id              = (known after apply)
      + zone                            = (known after apply)

      + admin_ssh_key {
          + public_key = "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDebkNmFZ07hGjKH3ZcrQ0AMEnthsgQE+VXmQ/yOjBrede3wf7+vniwMaDsC9kIlxRCs/sbBig86Q3/g5JhDOpDjEoReraMjLj/fhb1pxEWwUPNZkYbYq5Q4BwgLR9LfnrOTPZoOm3CWAckoxb0OVsHgr8dvdwTfwjjam4bjeELfKtNs49xUmAjfpPVkK3WqJ6YXxxN5XTeG4sV26gDWUAdboY44ohBwBcGN/Vpf0UcyvR0UWgnGVrPJ1PZ3eF3CncwHaCpTLaH7JKOGQafRzIhF9kdXbqwrPAGGiuh276paWJZpSfWZEY3uetx8ZqPu+oyu+B2Qs0oNSow40ln45j3"
          + username   = "adminuser"
        }

      + os_disk {
          + caching                   = "ReadWrite"
          + disk_size_gb              = (known after apply)
          + name                      = (known after apply)
          + storage_account_type      = "Standard_LRS"
          + write_accelerator_enabled = false
        }

      + source_image_reference {
          + offer     = "UbuntuServer"
          + publisher = "Canonical"
          + sku       = "16.04-LTS"
          + version   = "latest"
        }
    }

  # azurerm_network_interface.example will be created
  + resource "azurerm_network_interface" "example" {
      + applied_dns_servers           = (known after apply)
      + dns_servers                   = (known after apply)
      + enable_accelerated_networking = false
      + enable_ip_forwarding          = false
      + id                            = (known after apply)
      + internal_dns_name_label       = (known after apply)
      + internal_domain_name_suffix   = (known after apply)
      + location                      = "centralus"
      + mac_address                   = (known after apply)
      + name                          = "example-nic"
      + private_ip_address            = (known after apply)
      + private_ip_addresses          = (known after apply)
      + resource_group_name           = "Act1Terraform-example-resources"
      + virtual_machine_id            = (known after apply)

      + ip_configuration {
          + name                          = "internal"
          + primary                       = (known after apply)
          + private_ip_address            = (known after apply)
          + private_ip_address_allocation = "dynamic"
          + private_ip_address_version    = "IPv4"
          + subnet_id                     = (known after apply)
        }
    }

  # azurerm_resource_group.example will be created
  + resource "azurerm_resource_group" "example" {
      + id       = (known after apply)
      + location = "centralus"
      + name     = "Act1Terraform-example-resources"
    }

  # azurerm_subnet.example will be created
  + resource "azurerm_subnet" "example" {
      + address_prefix                                 = (known after apply)
      + address_prefixes                               = [
          + "10.0.2.0/24",
        ]
      + enforce_private_link_endpoint_network_policies = false
      + enforce_private_link_service_network_policies  = false
      + id                                             = (known after apply)
      + name                                           = "internal"
      + resource_group_name                            = "Act1Terraform-example-resources"
      + virtual_network_name                           = "example-network"
    }

  # azurerm_virtual_network.example will be created
  + resource "azurerm_virtual_network" "example" {
      + address_space         = [
          + "10.0.0.0/16",
        ]
      + dns_servers           = (known after apply)
      + guid                  = (known after apply)
      + id                    = (known after apply)
      + location              = "centralus"
      + name                  = "example-network"
      + resource_group_name   = "Act1Terraform-example-resources"
      + subnet                = (known after apply)
      + vm_protection_enabled = false
    }

Plan: 5 to add, 0 to change, 0 to destroy.

Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value: yes

azurerm_resource_group.example: Creating...
azurerm_resource_group.example: Creation complete after 2s [id=/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Act1Terraform-example-resources]
azurerm_virtual_network.example: Creating...
azurerm_virtual_network.example: Creation complete after 7s [id=/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Act1Terraform-example-resources/providers/Microsoft.Network/virtualNetworks/example-network]
azurerm_subnet.example: Creating...
azurerm_subnet.example: Creation complete after 5s [id=/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Act1Terraform-example-resources/providers/Microsoft.Network/virtualNetworks/example-network/subnets/internal]
azurerm_network_interface.example: Creating...
azurerm_network_interface.example: Creation complete after 3s [id=/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Act1Terraform-example-resources/providers/Microsoft.Network/networkInterfaces/example-nic]
azurerm_linux_virtual_machine.example: Creating...
azurerm_linux_virtual_machine.example: Still creating... [10s elapsed]
azurerm_linux_virtual_machine.example: Still creating... [20s elapsed]
azurerm_linux_virtual_machine.example: Still creating... [30s elapsed]
azurerm_linux_virtual_machine.example: Still creating... [40s elapsed]
azurerm_linux_virtual_machine.example: Still creating... [50s elapsed]
azurerm_linux_virtual_machine.example: Creation complete after 51s [id=/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Act1Terraform-example-resources/providers/Microsoft.Compute/virtualMachines/example-machine]

Apply complete! Resources: 5 added, 0 changed, 0 destroyed.
```

Resources created on Azure Portal, the name of my resource group is *${var.resourcename}-example-resources,* inside of this group there are all my created resources using Terraform.

![Screen Shot 2021-10-13 at 18.32.05.png](My%20first%20IaC%20project%20using%20Terraform%201e3fcb064c7c4c27ad63a057c6906d86/Screen_Shot_2021-10-13_at_18.32.05.png)

**Destroy**

```bash
Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  - destroy

Terraform will perform the following actions:

  # azurerm_linux_virtual_machine.example will be destroyed
  - resource "azurerm_linux_virtual_machine" "example" {
      - admin_username                  = "adminuser" -> null
      - allow_extension_operations      = true -> null
      - computer_name                   = "example-machine" -> null
      - disable_password_authentication = true -> null
      - encryption_at_host_enabled      = false -> null
      - extensions_time_budget          = "PT1H30M" -> null
      - id                              = "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Act1Terraform-example-resources/providers/Microsoft.Compute/virtualMachines/example-machine" -> null
      - location                        = "centralus" -> null
      - max_bid_price                   = -1 -> null
      - name                            = "example-machine" -> null
      - network_interface_ids           = [
          - "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Act1Terraform-example-resources/providers/Microsoft.Network/networkInterfaces/example-nic",
        ] -> null
      - platform_fault_domain           = -1 -> null
      - priority                        = "Regular" -> null
      - private_ip_address              = "10.0.2.4" -> null
      - private_ip_addresses            = [
          - "10.0.2.4",
        ] -> null
      - provision_vm_agent              = true -> null
      - public_ip_addresses             = [] -> null
      - resource_group_name             = "Act1Terraform-example-resources" -> null
      - size                            = "Standard_F2" -> null
      - tags                            = {} -> null
      - virtual_machine_id              = "5d7a7da5-a2ba-4958-bace-86553065cd00" -> null

      - admin_ssh_key {
          - public_key = "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDebkNmFZ07hGjKH3ZcrQ0AMEnthsgQE+VXmQ/yOjBrede3wf7+vniwMaDsC9kIlxRCs/sbBig86Q3/g5JhDOpDjEoReraMjLj/fhb1pxEWwUPNZkYbYq5Q4BwgLR9LfnrOTPZoOm3CWAckoxb0OVsHgr8dvdwTfwjjam4bjeELfKtNs49xUmAjfpPVkK3WqJ6YXxxN5XTeG4sV26gDWUAdboY44ohBwBcGN/Vpf0UcyvR0UWgnGVrPJ1PZ3eF3CncwHaCpTLaH7JKOGQafRzIhF9kdXbqwrPAGGiuh276paWJZpSfWZEY3uetx8ZqPu+oyu+B2Qs0oNSow40ln45j3" -> null
          - username   = "adminuser" -> null
        }

      - os_disk {
          - caching                   = "ReadWrite" -> null
          - disk_size_gb              = 30 -> null
          - name                      = "example-machine_OsDisk_1_3b60f6b441064dc38df1e8018088487c" -> null
          - storage_account_type      = "Standard_LRS" -> null
          - write_accelerator_enabled = false -> null
        }

      - source_image_reference {
          - offer     = "UbuntuServer" -> null
          - publisher = "Canonical" -> null
          - sku       = "16.04-LTS" -> null
          - version   = "latest" -> null
        }
    }

  # azurerm_network_interface.example will be destroyed
  - resource "azurerm_network_interface" "example" {
      - applied_dns_servers           = [] -> null
      - dns_servers                   = [] -> null
      - enable_accelerated_networking = false -> null
      - enable_ip_forwarding          = false -> null
      - id                            = "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Act1Terraform-example-resources/providers/Microsoft.Network/networkInterfaces/example-nic" -> null
      - internal_domain_name_suffix   = "ftrebybqf5zurfqflfuowxom2a.gx.internal.cloudapp.net" -> null
      - location                      = "centralus" -> null
      - mac_address                   = "00-0D-3A-A4-01-03" -> null
      - name                          = "example-nic" -> null
      - private_ip_address            = "10.0.2.4" -> null
      - private_ip_addresses          = [
          - "10.0.2.4",
        ] -> null
      - resource_group_name           = "Act1Terraform-example-resources" -> null
      - tags                          = {} -> null
      - virtual_machine_id            = "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Act1Terraform-example-resources/providers/Microsoft.Compute/virtualMachines/example-machine" -> null

      - ip_configuration {
          - name                          = "internal" -> null
          - primary                       = true -> null
          - private_ip_address            = "10.0.2.4" -> null
          - private_ip_address_allocation = "Dynamic" -> null
          - private_ip_address_version    = "IPv4" -> null
          - subnet_id                     = "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Act1Terraform-example-resources/providers/Microsoft.Network/virtualNetworks/example-network/subnets/internal" -> null
        }
    }

  # azurerm_resource_group.example will be destroyed
  - resource "azurerm_resource_group" "example" {
      - id       = "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Act1Terraform-example-resources" -> null
      - location = "centralus" -> null
      - name     = "Act1Terraform-example-resources" -> null
      - tags     = {} -> null
    }

  # azurerm_subnet.example will be destroyed
  - resource "azurerm_subnet" "example" {
      - address_prefix                                 = "10.0.2.0/24" -> null
      - address_prefixes                               = [
          - "10.0.2.0/24",
        ] -> null
      - enforce_private_link_endpoint_network_policies = false -> null
      - enforce_private_link_service_network_policies  = false -> null
      - id                                             = "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Act1Terraform-example-resources/providers/Microsoft.Network/virtualNetworks/example-network/subnets/internal" -> null
      - name                                           = "internal" -> null
      - resource_group_name                            = "Act1Terraform-example-resources" -> null
      - service_endpoint_policy_ids                    = [] -> null
      - service_endpoints                              = [] -> null
      - virtual_network_name                           = "example-network" -> null
    }

  # azurerm_virtual_network.example will be destroyed
  - resource "azurerm_virtual_network" "example" {
      - address_space         = [
          - "10.0.0.0/16",
        ] -> null
      - dns_servers           = [] -> null
      - guid                  = "e040e22c-2f30-48f3-9605-5968eb5dcce0" -> null
      - id                    = "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Act1Terraform-example-resources/providers/Microsoft.Network/virtualNetworks/example-network" -> null
      - location              = "centralus" -> null
      - name                  = "example-network" -> null
      - resource_group_name   = "Act1Terraform-example-resources" -> null
      - subnet                = [
          - {
              - address_prefix = "10.0.2.0/24"
              - id             = "/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Act1Terraform-example-resources/providers/Microsoft.Network/virtualNetworks/example-network/subnets/internal"
              - name           = "internal"
              - security_group = ""
            },
        ] -> null
      - tags                  = {} -> null
      - vm_protection_enabled = false -> null
    }

Plan: 0 to add, 0 to change, 5 to destroy.

Do you really want to destroy all resources?
  Terraform will destroy all your managed infrastructure, as shown above.
  There is no undo. Only 'yes' will be accepted to confirm.

  Enter a value: yes

azurerm_linux_virtual_machine.example: Destroying... [id=/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Act1Terraform-example-resources/providers/Microsoft.Compute/virtualMachines/example-machine]
azurerm_linux_virtual_machine.example: Still destroying... [id=/subscriptions/faf4b0cb-287e-4be0-818e-...ompute/virtualMachines/example-machine, 10s elapsed]
azurerm_linux_virtual_machine.example: Still destroying... [id=/subscriptions/faf4b0cb-287e-4be0-818e-...ompute/virtualMachines/example-machine, 20s elapsed]
azurerm_linux_virtual_machine.example: Still destroying... [id=/subscriptions/faf4b0cb-287e-4be0-818e-...ompute/virtualMachines/example-machine, 30s elapsed]
azurerm_linux_virtual_machine.example: Still destroying... [id=/subscriptions/faf4b0cb-287e-4be0-818e-...ompute/virtualMachines/example-machine, 40s elapsed]
azurerm_linux_virtual_machine.example: Still destroying... [id=/subscriptions/faf4b0cb-287e-4be0-818e-...ompute/virtualMachines/example-machine, 50s elapsed]
azurerm_linux_virtual_machine.example: Still destroying... [id=/subscriptions/faf4b0cb-287e-4be0-818e-...ompute/virtualMachines/example-machine, 1m0s elapsed]
azurerm_linux_virtual_machine.example: Still destroying... [id=/subscriptions/faf4b0cb-287e-4be0-818e-...ompute/virtualMachines/example-machine, 1m10s elapsed]
azurerm_linux_virtual_machine.example: Still destroying... [id=/subscriptions/faf4b0cb-287e-4be0-818e-...ompute/virtualMachines/example-machine, 1m20s elapsed]
azurerm_linux_virtual_machine.example: Destruction complete after 1m25s
azurerm_network_interface.example: Destroying... [id=/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Act1Terraform-example-resources/providers/Microsoft.Network/networkInterfaces/example-nic]
azurerm_network_interface.example: Still destroying... [id=/subscriptions/faf4b0cb-287e-4be0-818e-....Network/networkInterfaces/example-nic, 10s elapsed]
azurerm_network_interface.example: Destruction complete after 11s
azurerm_subnet.example: Destroying... [id=/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Act1Terraform-example-resources/providers/Microsoft.Network/virtualNetworks/example-network/subnets/internal]
azurerm_subnet.example: Still destroying... [id=/subscriptions/faf4b0cb-287e-4be0-818e-...works/example-network/subnets/internal, 10s elapsed]
azurerm_subnet.example: Destruction complete after 11s
azurerm_virtual_network.example: Destroying... [id=/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Act1Terraform-example-resources/providers/Microsoft.Network/virtualNetworks/example-network]
azurerm_virtual_network.example: Still destroying... [id=/subscriptions/faf4b0cb-287e-4be0-818e-...etwork/virtualNetworks/example-network, 10s elapsed]
azurerm_virtual_network.example: Destruction complete after 11s
azurerm_resource_group.example: Destroying... [id=/subscriptions/faf4b0cb-287e-4be0-818e-c4348b26c45e/resourceGroups/Act1Terraform-example-resources]
azurerm_resource_group.example: Still destroying... [id=/subscriptions/faf4b0cb-287e-4be0-818e-...Groups/Act1Terraform-example-resources, 10s elapsed]
azurerm_resource_group.example: Destruction complete after 17s

Destroy complete! Resources: 5 destroyed.
```

As you can see my resources disappear

![Screen Shot 2021-10-13 at 14.51.50.png](My%20first%20IaC%20project%20using%20Terraform%201e3fcb064c7c4c27ad63a057c6906d86/Screen_Shot_2021-10-13_at_14.51.50.png)

These are all my files, objects and resources for this project. In GitLab these are not present due to my .gitignore file

![Screen Shot 2021-10-13 at 18.31.28.png](My%20first%20IaC%20project%20using%20Terraform%201e3fcb064c7c4c27ad63a057c6906d86/Screen_Shot_2021-10-13_at_18.31.28.png)

[Azure Backend](My%20first%20IaC%20project%20using%20Terraform%201e3fcb064c7c4c27ad63a057c6906d86/Azure%20Backend%20f9571c51070a4ec4bd097cd88bb9b3f2.md)

[Integrating Terraform to CICD tools](My%20first%20IaC%20project%20using%20Terraform%201e3fcb064c7c4c27ad63a057c6906d86/Integrating%20Terraform%20to%20CICD%20tools%200a75a8269b98426a9d36235c6856a0e2.md)

[Basic Azure Infrastructure ](My%20first%20IaC%20project%20using%20Terraform%201e3fcb064c7c4c27ad63a057c6906d86/Basic%20Azure%20Infrastructure%206e3fde97099e42168db9852795d41c84.md)

[Modules](My%20first%20IaC%20project%20using%20Terraform%201e3fcb064c7c4c27ad63a057c6906d86/Modules%202732966a92794ba192cdd7649b846656.md)