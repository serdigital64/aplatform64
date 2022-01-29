---
title: "Ansible Playbook: manage_dev_nodes"
description: "Provision software development environments"
authors:
  - SerDigital64
tags:
  - ansible
  - devops
  - linux
  - automation
---

# Ansible Playbook: manage_dev_nodes

## Purpose

Provision software development environments.

Supported features in the current version:

- Install development languages:
  - GCC
  - Java
  - NodeJS
  - Python
  - Ruby
- Install common development tools:
  - make
- Install IDEs:
  - VSCode
- Install test/dev environment provisioners:
  - Vagrant

## Use Cases

### Deploy software development environments

- Verify that target nodes are registered in the inventory file: [dev_nodes.ini](#inventory)
- Verify that target endstate is set: [manage_dev_nodes.yml](#end-state)
- Run the playbook. Use the `-s <SITE>` parameter to select the target site.

```shell
/opt/aplatform64/bin/ap64.sh -n -p manage_dev_nodes -s <SITE>
```

## Playbook Parameters

### Inventory

Register the hosts that will consume the service in the Ansible Inventory file:

- File: `inventories/<SITE>/dev_nodes.ini`
- Host Group: `dev_nodes`

### End State

A dedicated group_vars directory is used to store end-state configuration settings for both the playbook and related Ansible Roles.

Set playbook specific settings in the file: `inventories/<SITE>/group_vars/dev_nodes/manage_dev_nodes.yml`

```yaml
dev_nodes_apps:
  gcc:
  java:
  nodejs:
  python:
  ruby:
  tools:
  vagrant:
  vscode:
```

| Parameter              | Required? | Type       | Default | Purpose / Value                           |
| ---------------------- | --------- | ---------- | ------- | ----------------------------------------- |
| dev_nodes_apps         | yes       | dictionary |         | Define what applications will be deployed |
| dev_nodes_apps.gcc     | no        | boolean    | `false` | Deploy the application?                   |
| dev_nodes_apps.java    | no        | boolean    | `false` | Deploy the application?                   |
| dev_nodes_apps.nodejs  | no        | boolean    | `false` | Deploy the application?                   |
| dev_nodes_apps.python  | no        | boolean    | `false` | Deploy the application?                   |
| dev_nodes_apps.ruby    | no        | boolean    | `false` | Deploy the application?                   |
| dev_nodes_apps.tools   | no        | boolean    | `true`  | Deploy the application?                   |
| dev_nodes_apps.vagrant | no        | boolean    | `false` | Deploy the application?                   |
| dev_nodes_apps.vscode  | no        | boolean    | `false` | Deploy the application?                   |

Additional role specific settings are available to further customize the playbook:

| A:Platform64 role                                                                | group_vars file                                               |
| -------------------------------------------------------------------------------- | ------------------------------------------------------------- |
| [serdigital64.system.sys_repository](../roles/sys_repository.md#role-parameters) | `inventories/<SITE>/group_vars/dev_nodes/sys_repository.yml` |
| [serdigital64.application.app_vscode](../roles/app_vscode.md#role-parameters)    | `inventories/<SITE>/group_vars/dev_nodes/app_vscode.yml`      |
| [serdigital64.development.dev_java](../roles/dev_java.md#role-parameters)        | `inventories/<SITE>/group_vars/dev_nodes/dev_java.yml`        |

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
  - serdigital64.development
  - serdigital64.application

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