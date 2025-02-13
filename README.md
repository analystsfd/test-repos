# Nutanix Ansible
Official nutanix ansible collection.

# About
Nutanix ansible collection <font color=rolyalblue>nutanix.ncp</font> is the official Nutanix ansible collection to automate Nutanix Cloud Platform (ncp).

It is designed keeping simplicity as the core value. Hence it is
1. Easy to use
2. Easy to develop

Checkout this [blog](https://www.nutanix.dev/2022/08/05/getting-started-with-the-nutanix-ansible-module/) for getting started with nutanix ansible module.

# Version compatibility

## Ansible
This collection and examples has been tested against following versions :
  1. ansible==5.0.1
  2. ansible-core==2.12.3

## Python
This collection requires Python 2.7 or greater

## Prism Central
> For the 1.1.0 release of the ansible plugin it will have N-2 compatibility with the Prism Central APIs. This release was tested against Prism Central versions pc2022.1.0.2, pc.2021.9.0.5 and pc.2021.8.0.1.

> For the 1.2.0 release of the ansible plugin it will have N-2 compatibility with the Prism Central APIs. This release was tested against Prism Central versions pc.2022.4, pc2022.1.0.2 and pc.2021.9.0.5.

> For the 1.3.0 release of the ansible plugin it will have N-2 compatibility with the Prism Central APIs. This release was tested against Prism Central versions pc.2022.4, pc2022.1.0.2 and pc.2021.9.0.4. 

> For the 1.4.0 release of the ansible plugin it will have N-2 compatibility with the Prism Central APIs. This release was tested against Prism Central versions pc.2022.4, pc2022.1.0.2 and pc.2021.9.0.4. 

> For the 1.5.0 release of the ansible plugin it will have N-2 compatibility with the Prism Central APIs. This release was tested against Prism Central versions pc.2022.6, pc.2022.4.0.2 and pc2022.1.0.2.

> For the 1.7.0 release of the ansible plugin it will have N-2 compatibility with the Prism Central APIs. This release was tested against Prism Central versions pc.2022.6, pc.2022.4 and pc2022.1.0.2.

> For the 1.8.0-beta.1 release of the ansible plugin it will have N compatibility with the Prism Central APIs. This release was tested against Prism Central version pc.2022.6 .
### Notes:
1. Static routes module (ntnx_static_routes) is supported for PC versions >= pc.2022.1

2. Adding cluster references in projects module (ntnx_projects) is supported for PC versions >= pc.2022.1

3. For Users and User Groups modules (ntnx_users and ntnx_user_groups), adding Identity Provider (IdP) & Organizational Unit (OU) based users/groups are supported for PC versions >= pc.2022.1

Prism Central based examples: https://github.com/nutanix/nutanix.ansible/tree/main/examples/

## Foundation
> For the 1.1.0 release of the ansible plugin, it will have N-1 compatibility with the Foundation. This release was tested against Foundation versions v5.2 and v5.1.1

Foundation based examples : https://github.com/nutanix/nutanix.ansible/tree/main/examples/foundation

## Foundation Central
> For the 1.1.0 release of the ansible plugin, it will have N-1 compatibility with the Foundation Central . This release was tested against Foundation Central versions v1.3 and v1.2

Foundation Central based examples : https://github.com/nutanix/nutanix.ansible/tree/main/examples/fc

## Karbon
> For the 1.6.0 release of the ansible plugin, it will have N-2 compatibility with the Karbon. This release was tested against Karbon versions v2.3.0, v2.4.0 and v2.5.0 

Karbon based examples : https://github.com/nutanix/nutanix.ansible/tree/main/examples/karbon

## Nutanix Database Service (ERA)
> For the 1.8.0-beta.1 release of the ansible plugin, it will have N-1 compatibility with the Nutanix Database Service (ERA). This release was tested against era versions v2.4.1 and v2.4.0

NDB based examples : https://github.com/nutanix/nutanix.ansible/tree/main/examples/ndb

Nutanix Ansible support for Nutanix Database Service is currently at beta stage.

### Notes:
1. Currently for ntnx_ndb_databases, creation of only postgres type database instance is tested and offically supported. 
 
# Installing the collection
**Prerequisite**

Ansible should be pre-installed. If not, please follow official ansible [install guide](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html) .

For <font color=royalblue>Developers</font>, please follow [this install guide](https://docs.ansible.com/ansible/latest/dev_guide/developing_modules_general.html) for setting up dev environment.

**1. Clone the GitHub repository to a local directory**

```git clone https://github.com/nutanix/nutanix.ansible.git```

**2. Git checkout release version**

```git checkout <release_version> -b <release_version>```

**3. Build the collection**

```ansible-galaxy collection build```

**4. Install the collection**

```ansible-galaxy collection install nutanix-ncp-<version>.tar.gz```

**Note** Add <font color=red>`--force`</font> option for rebuilding or reinstalling to overwrite existing data

# Using this collection
You can either call modules by their Fully Qualified Collection Namespace (FQCN), such as<font color=royalblue> nutanix.ncp.ntnx_vms</font>, or you can call modules by their short name if you list the <font color=royalblue>nutanix.ncp </font>collection in the playbook's ```collections:``` keyword

For example, the playbook for iaas.yml is as follows:
```yaml
---
- name: IaaS Provisioning
  hosts: localhost
  gather_facts: false
  collections:
    - nutanix.ncp
  module_defaults:
    group/nutanix.ncp.ntnx:
      nutanix_host: <pc_ip>
      nutanix_username: <user>
      nutanix_password: <pass>
      validate_certs: true
  tasks:
    - include_role:
        name: external_subnet
    - include_role:
        name: vpc
    - include_role:
        name: overlay_subnet
    - include_role:
        name: vm
    - include_role:
        name: fip
```
To run this playbook, use <font color=royalblue>ansible-playbook</font> command as follows:
```
ansible-playbook <playbook_name>
ansible-playbook examples/iaas/iaas.yml
```

# Included Content

## Modules

| Name | Description |
| --- | --- |
| ntnx_acps | Create, Update, Delete acp. |
| ntnx_acps_info | Get acp info. |
| ntnx_address_groups | Create, Update, Delete Nutanix address groups. |
| ntnx_address_groups_info | Get address groups info. |
| ntnx_categories | Create, Update, Delete categories |
| ntnx_categories_info | Get categories info. |
| ntnx_clusters_info | Get cluster info. |
| ntnx_floating_ips | Create or delete a Floating Ip. |
| ntnx_floating_ips_info | List existing Floating_Ips. |
| ntnx_hosts_info | Get host info. |
| ntnx_images | Create, update or delete a image. |
| ntnx_images_info | List existing images. |
| ntnx_image_placement_policy | Create, update or delete a image placement policy. |
| ntnx_image_placement_policies_info | List existing image placement policies. |
| ntnx_karbon_clusters | Create, Delete k8s clusters |
| ntnx_karbon_clusters_info | Get clusters info. |
| ntnx_karbon_registries | Create, Delete a karbon private registry entry |
| ntnx_karbon_registries_info | Get karbon private registry registry info. |
| ntnx_ndb_databases | Create, Update and Delete single instance database. |
| ntnx_ndb_databases_info | Get database info. |
| ntnx_ndb_db_servers_info | Get db servers vm info. |
| ntnx_ndb_clusters_info | Get clusters info. |
| ntnx_ndb_slas_info | Get slas info |
| ntnx_ndb_profiles_info | Get profiles info. |
| ntnx_ndb_time_machines_info | Get time machines info. |
| ntnx_ndb_clones_info | Get database clones info. |
| ntnx_pbrs | Create or delete a PBR. |
| ntnx_pbrs_info | List existing PBRs. |
| ntnx_permissions_info | List permissions info |
| ntnx_projects | create, update and delete pc projects |
| ntnx_projects_info | Get projects info. |
| ntnx_protection_rules | create, update and delete pc protection rules |
| ntnx_protection_rules_info | Get pc protection rules info. |
| ntnx_recovery_plans | create, update and delete pc recovery plans |
| ntnx_recovery_plans_info | Get pc recovery plans info. |
| ntnx_recovery_plan_jobs | create and perform action on pc recovery plans |
| ntnx_recovery_plan_jobs_info | Get pc recovery plan jobs info. |
| ntnx_roles | Create, Update, Delete Nutanix roles |
| ntnx_roles_info | Get roles info. |
| ntnx_security_rules | Create, update or delete a Security Rule. |
| ntnx_security_rules_info | List existing Security Rules. |
| ntnx_service_groups | Create, Update, Delete service_group |
| ntnx_service_groups_info | Get service groups info. |
| ntnx_static_routes | Update static routes of a vpc. |
| ntnx_static_routes_info | List existing static routes of a vpc. |
| ntnx_subnets | Create or delete a Subnet. |
| ntnx_subnets_info | List existing Subnets. |
| ntnx_user_groups | Create, Delete user_groups |
| ntnx_user_groups_info | Get user groups info. |
| ntnx_users | Create, Delete users |
| ntnx_users_info | Get users info. |
| ntnx_vms | Create or delete a VM. |
| ntnx_vms_clone | Clone VM. |
| ntnx_vms_ova | Create OVA image from VM. |
| ntnx_vms_info | List existing VMs. |
| ntnx_vpcs | Create or delete a VPC. |
| ntnx_vpcs_info | List existing VPCs. |
| ntnx_foundation | Image nodes and create new cluster. |
| ntnx_foundation_aos_packages_info | List the AOS packages uploaded to Foundation. |
| ntnx_foundation_bmc_ipmi_config | Configure IPMI IP address on BMC of nodes. |
| ntnx_foundation_discover_nodes_info | List the nodes discovered by Foundation. |
| ntnx_foundation_hypervisor_images_info | List the hypervisor images uploaded to Foundation. |
| ntnx_foundation_image_upload | Upload hypervisor or AOS image to Foundation VM. |
| ntnx_foundation_node_network_info | Get node network information discovered by Foundation. |
| ntnx_foundation_central | Create a cluster out of nodes registered with Foundation Central. |
| ntnx_foundation_central_api_keys | Create a new api key which will be used by remote nodes to authenticate with Foundation Central. |
| ntnx_foundation_central_api_keys_info | List all the api keys created in Foundation Central. |
| ntnx_foundation_central_imaged_clusters_info | List all the clusters created using Foundation Central. |
| ntnx_foundation_central_imaged_nodes_info | List all the nodes registered with Foundation Central. |

## Inventory Plugins

| Name | Description |
| --- | --- |
| ntnx_prism_vm_inventory | Nutanix VMs inventory source |

# Module documentation and examples
```
ansible-doc nutanix.ncp.<module_name>
```

# How to contribute

We glady welcome contributions from the community. From updating the documentation to adding more functions for Ansible, all ideas are welcome. Thank you in advance for all of your issues, pull requests, and comments!

* [Contributing Guide](CONTRIBUTING.md)
* [Code of Conduct](CODE_OF_CONDUCT.md)

# Examples
## Playbook for IaaS provisioning on Nutanix

**Refer to [`examples/iaas`](https://github.com/nutanix/nutanix.ansible/tree/main/examples/iaas) for full implementation**

```yaml
---
- name: IaaS Provisioning
  hosts: localhost
  gather_facts: false
  collections:
    - nutanix.ncp
  vars:
      nutanix_host: <pc_ip>
      nutanix_username: <user>
      nutanix_password: <pass>
      validate_certs: true
  tasks:
    - name: Inputs for external subnets task
      include_tasks: external_subnet.yml
      with_items:
        - { name: Ext-Nat, vlan_id: 102, ip: 10.44.3.192, prefix: 27, gip: 10.44.3.193, sip: 10.44.3.198, eip: 10.44.3.207, eNat: True }

    - name: Inputs for vpcs task
      include_tasks: vpc.yml
      with_items:
      - { name: Prod, subnet_name: Ext-Nat}
      - { name: Dev, subnet_name: Ext-Nat}

    - name: Inputs for overlay subnets
      include_tasks: overlay_subnet.yml
      with_items:
        - { name: Prod-SubnetA, vpc_name: Prod , nip: 10.1.1.0, prefix: 24, gip: 10.1.1.1, sip: 10.1.1.2, eip: 10.1.1.5,
            domain_name: "calm.nutanix.com", dns_servers : ["8.8.8.8","8.8.8.4"], domain_search: ["calm.nutanix.com","eng.nutanix.com"] }
        - { name: Prod-SubnetB, vpc_name: Prod , nip: 10.1.2.0, prefix: 24, gip: 10.1.2.1, sip: 10.1.2.2, eip: 10.1.2.5,
            domain_name: "calm.nutanix.com", dns_servers : ["8.8.8.8","8.8.8.4"], domain_search: ["calm.nutanix.com","eng.nutanix.com"] }
        - { name: Dev-SubnetA, vpc_name:  Dev , nip: 10.1.1.0, prefix: 24, gip: 10.1.1.1, sip: 10.1.1.2, eip: 10.1.1.5,
            domain_name: "calm.nutanix.com", dns_servers : ["8.8.8.8","8.8.8.4"], domain_search: ["calm.nutanix.com","eng.nutanix.com"] }
        - { name: Dev-SubnetB, vpc_name:  Dev , nip: 10.1.2.0, prefix: 24, gip: 10.1.2.1, sip: 10.1.2.2, eip: 10.1.2.5,
            domain_name: "calm.nutanix.com", dns_servers : ["8.8.8.8","8.8.8.4"], domain_search: ["calm.nutanix.com","eng.nutanix.com"] }

    - name: Inputs for vm task
      include_tasks: vm.yml
      with_items:
       - {name: "Prod-Wordpress-App", desc: "Prod-Wordpress-App", is_connected: True , subnet_name: Prod-SubnetA, image_name: "wordpress-appserver", private_ip: ""}
       - {name: "Prod-Wordpress-DB", desc: "Prod-Wordpress-DB", is_connected: True , subnet_name: Prod-SubnetB, image_name: "wordpress-db", private_ip: 10.1.2.5}
       - {name: "Dev-Wordpress-App", desc: "Dev-Wordpress-App", is_connected: True , subnet_name: Dev-SubnetA, image_name: "wordpress-appserver", private_ip: ""}
       - {name: "Dev-Wordpress-DB", desc: "Dev-Wordpress-DB", is_connected: True , subnet_name: Dev-SubnetB, image_name: "wordpress-db",private_ip: 10.1.2.5}

    - name: Inputs for Floating IP task
      include_tasks: fip.yml
      with_items:
        - {vm_name: "Prod-Wordpress-App"}
        - {vm_name: "Dev-Wordpress-App"}

```
