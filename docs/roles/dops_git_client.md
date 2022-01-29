---
title: "Ansible Role: serdigital64.devops.dops_git_client"
description: "Manage provisioning of client side GIT"
authors:
  - SerDigital64
tags:
  - ansible
  - devops
  - linux
  - automation
---

# Ansible Role: serdigital64.devops.dops_git_client

## Purpose

Manage provisioning of client side GIT.

Supported features in the current version:

- Deploy application. Packages are defined in the variable `dops_git_client_profiles`.
- Create GIT local repositories:
  - sets initial git config
    - user.name
    - user.email
    - init.defaultBranch
  - Create .gitignore file
  - initializes project directory: git init

The **dops_git_client** Ansible-Role is part of the [A:Platform64](https://github.com/serdigital64/aplatform64) project and is available in the [devops](../collections/devops.md) Ansible-Collection.

## Usage

The following example is an **Ansible Playbook** that includes all the supported features:

```yaml
{% include "../../collections/serdigital64/devops/playbooks/dops_git_client.yml" %}
```

The playbook can be run by executing:

```shell
# Set ANSIBLE_COLLECTIONS_PATHS to the default install location. Change as needed.
ANSIBLE_COLLECTIONS_PATHS="${HOME}/.ansible/collections"
ansible-playbook "${ANSIBLE_COLLECTIONS_PATHS}/ansible_collections/serdigital64/devops/playbooks/dops_git_client.yml"
```

## Role Parameters

### Actions

- Use **action-parameters** to control what tasks are enabled for the role to execute.
- Parameters should be declared as task level vars as they are intented to be dynamic.

```yaml
dops_git_client:
  resolve_prereq:
  deploy:
```

| Parameter                      | Required? | Type    | Default | Purpose / Value                            |
| ------------------------------ | --------- | ------- | ------- | ------------------------------------------ |
| dops_git_client.resolve_prereq | no        | boolean | `false` | Enable automatic resolution of prequisites |
| dops_git_client.deploy         | no        | boolean | `false` | Enable installation of application package |

### End State

- Use **end-state** parameters to define the target state after role execution.
- Parameters should be declared in **host_vars** or **group_vars** as they are intended to be permanent.

```yaml
dops_git_client_application:
  client:
    name:
    type:
    version:
    installed:
  extras:
    name:
    type:
    version:
    installed:
dops_git_client_repositories:
  - name:
    path:
    owner:
    email:
    branch:
    ignore:
      -
```

| Parameter                                    | Required?      | Type       | Default    | Purpose / Value                           |
| -------------------------------------------- | -------------- | ---------- | ---------- | ----------------------------------------- |
| dops_git_client_application                  | no             | dictionary |            | Set application package end state         |
| dops_git_client_application.client           | no             | dictionary |            | Set application package end state         |
| dops_git_client_application.client.name      | no             | string     | `"git"`    | Select application package name           |
| dops_git_client_application.client.type      | no             | string     | `"distro"` | Select application package type           |
| dops_git_client_application.client.version   | no             | string     | `"latest"` | Select application package version        |
| dops_git_client_application.client.installed | no             | boolean    | `true`     | Set application package end state         |
| dops_git_client_application.extras           | no             | dictionary |            | Set application package end state         |
| dops_git_client_application.extras.name      | no             | string     | `"extras"` | Select application package name           |
| dops_git_client_application.extras.type      | no             | string     | `"distro"` | Select application package type           |
| dops_git_client_application.extras.version   | no             | string     | `"latest"` | Select application package version        |
| dops_git_client_application.extras.installed | no             | boolean    | `false`    | Set application package end state         |
| dops_git_client_repositories                 | yes(provision) | dictionary |            | Define GIT repositories to be provisioned |
| dops_git_client_repositories.0.name          | yes            | string     |            | Project short name                        |
| dops_git_client_repositories.0.path          | yes            | string     |            | Project full path                         |
| dops_git_client_repositories.0.owner         | yes            | string     |            | Project owner. User must already exist    |
| dops_git_client_repositories.0.email         | yes            | string     |            | Project owner's email                     |
| dops_git_client_repositories.0.branch        | no             | string     | `"main"`   | GIT default branch name                   |
| dops_git_client_repositories.0.ignore        | no             | list       | `[]`       | List of paths for gitignore               |
| dops_git_client_repositories.0.ignore.0      | no             | string     |            | Path pattern                              |

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

- Ansible Collections:
  - serdigital64.backup
  - serdigital64.system

### Prerequisites

The Ansible engine must be already installed and configured for privileged access and remote execution.

In addition the following prerequisites can be automatically solved when running the playbook by setting the role action: `resolve_prereq: true`

- Package manager for the target application is installed and enabled.

### Installation Procedure

Manually install Ansible Collections from the Ansible Galaxy repository:

```shell
ansible-galaxy collection install --upgrade serdigital64.devops
```

Automatic installation is also available by deploying [A:Platform64](https://aplatform64.readthedocs.io/en/latest/#deployment)

## Contributing

Help on implementing new features and maintaining the code base is welcomed.

Please see the [guidelines](../contributing/guidelines.md) for further details.

## Author

- [SerDigital64](https://serdigital64.github.io/)

## License

[GPL-3.0-or-later](https://www.gnu.org/licenses/gpl-3.0.txt)