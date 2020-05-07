## Required Privileges (terraform)

In order to use Terraform provider as non priviledged user, some Roles within vCenter must be assigned the following privileges:

- Datastore (Role: ocp-terraform-datastore)
  - Allocate space
  - Low level file operations
- Profile-driven storage (Role: ocp-terraform-vcenter)
  - Profile-driven storage view
- Network (Role: ocp-terraform-network)
  - Assign network
- Resource (Role: ocp-terraform-resource)
  - Assign vApp to resource pool
  - Assign virtual machine to resource pool
- vApp (Role: ocp-terraform-vm)
  - Clone
  - View OVF environment
  - vApp application configuration
  - vApp instance configuration
  - vApp resource configuration
- Virtual machine (Role: ocp-terraform-vm)
  - Change Configuration (all)
  - Edit Inventory (all)
  - Guest operations (all)
  - Interaction (all)
  - Provisioning (all)

And these roles have to be given permission on the following entities:
Role | Entity | Propagate to Children | Description
---- | ------ | --------- | -----------
ocp-terraform-vm | VM Folder | Yes | The folder where VMs will be alocated
ocp-terraform-vm | Virtual Machine | No | The OVA template that will be cloned
ocp-terraform-network | VM Network | No | The VM Network the VMs will attach  to
ocp-terraform-datastore | Datastore | No | The Datastore where the VMs disk0 will reside
ocp-terraform-resource | Resource Pool |  No | The Resource Pool the VMs will we added to
ocp-terraform-vcenter | vCenter | No | Profile-driven storage view
Read-Only (System) | Virtual Switch | No | The Distributed Virtual Switch (\*)

(\*) If the VM Network is going to be on a Distributed Virtual Switch then this permissions needs to be applied as well
