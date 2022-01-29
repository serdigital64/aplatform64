---
title: "Ansible Playbook: bootstrap_ansible_managed_nodes"
description: "Bootstrap Ansible Managed nodes"
authors:
  - SerDigital64
tags:
  - ansible
  - devops
  - linux
  - automation
---

# Ansible Playbook: bootstrap_ansible_managed_nodes

## Purpose

Bootstrap Ansible Managed nodes.

Supported features in the current version:

- Register the node in the Ansible controller
- Prepare the managed node for remote control

## Use Cases

### Prepare Ansible Managed node

- Verify that target nodes are registered in the inventory file: [ansible_service.ini](#inventory), group: `bootstrap_ansible_managed_nodes_distro`
- Verify that the bootstrap credentials are set in the endstate file: [auto_ansible_node.yml](#end-state)
- Run the playbook. Use the `-s <SITE>` parameter to select the target site.

```shell
/opt/aplatform64/bin/ap64.sh -n -p bootstrap_ansible_managed_nodes -s <SITE>
```

- Update the inventory file by removing the host from the group `bootstrap_ansible_managed_nodes_distro` and adding it to the group `ansible_managed_nodes`

## Playbook Parameters

### Inventory

Register the hosts that will consume the service in the Ansible Inventory file:

- File: `inventories/<SITE>/ansible_service.ini`
- Host Group: `bootstrap_ansible_managed_nodes_distro`

### End State

A dedicated group_vars directory is used to store end-state configuration settings for both the playbook and related Ansible Roles.

Role specific settings are available to further customize the playbook:

| A:Platform64 role                                                                          | group_vars file                                                                              |
| ------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------- |
| [serdigital64.automation.auto_ansible_node](../roles/auto_ansible_node.md#role-parameters) | `inventories/<SITE>/group_vars/bootstrap_ansible_managed_nodes_distro/auto_ansible_node.yml` |

## Deployment

### OS Compatibility

- CentOS8
- OracleLinux8
- Ubuntu20
- Ubuntu21
- Fedora33
- Fedora35
- Debian10
- Debian11

### Dependencies

Dependencies in this section are automatically solved during the installation of A:Platform64.

- Ansible Collections:
  - serdigital64.backup
  - serdigital64.system
  - serdigital64.automation

### Prerequisites

- Ansible:
  - Control Node: A:Platform64 installed and configured.
  - Managed Nodes: target hosts prepared for A:Platform64 control.

### Installation Procedure

The playbook is automatically deployed during the [A:Platform64 installation](/#installation) process.

## Contributing

Help on implementing new features and maintaining the code base is welcomed.

Please see the [guidelines](../contributing/guidelines.md) for further details.

## Author

- [SerDigital64](https://serdigital64.github.io/)

## License

[GPL-3.0-or-later](https://www.gnu.org/licenses/gpl-3.0.txt)