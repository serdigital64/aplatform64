---
title: "Ansible Role: serdigital64.system.sys_kernel"
description: "Manage OS Kernel configuration"
authors:
  - SerDigital64
tags:
  - ansible
  - devops
  - linux
  - automation
---

# Ansible Role: serdigital64.system.sys_kernel

## Purpose

Manage OS Kernel configuration.

Supported features in the current version:

- Provision sysctl tool
- Control Kernel subsystem tunables:
  - network
  - filesystem

The **sys_kernel** Ansible-Role is part of the [A:Platform64](https://github.com/serdigital64/aplatform64) project and is available in the [system](../collections/system.md) Ansible-Collection.

## Usage

The following example is an **Ansible Playbook** that includes all the supported features:

```yaml
{% include "../../collections/serdigital64/system/playbooks/sys_kernel.yml" %}
```

The playbook can be run by executing:

```shell
# Set ANSIBLE_COLLECTIONS_PATHS to the default install location. Change as needed.
ANSIBLE_COLLECTIONS_PATHS="${HOME}/.ansible/collections"
ansible-playbook "${ANSIBLE_COLLECTIONS_PATHS}/ansible_collections/serdigital64/system/playbooks/sys_kernel.yml"
```

## Role Parameters

### Actions

- Use **action-parameters** to control what tasks are enabled for the role to execute.
- Parameters should be declared as task level vars as they are intented to be dynamic.

```yaml
sys_kernel:
  resolve_prereq:
  deploy:
  setup:
```

| Parameter                 | Required? | Type    | Default | Purpose / Value                             |
| ------------------------- | --------- | ------- | ------- | ------------------------------------------- |
| sys_kernel.resolve_prereq | no        | boolean | `false` | Enable automatic resolution of prequisites  |
| sys_kernel.deploy         | no        | boolean | `false` | Enable installation of application packages |
| sys_kernel.setup          | no        | boolean | `false` | Enable application configuration            |

### End State

- Use **end-state** parameters to define the target state after role execution.
- Parameters should be declared in **host_vars** or **group_vars** as they are intended to be permanent.

```yaml
sys_kernel_tunables:
  net:
    ipv4:
      ip_forward:
  fs:
    file_max:
    inotify:
      max_queued_events:
      max_user_instances:
      max_user_watches:
```

| Parameter                                         | Required? | Type       | Default | Purpose / Value           |
| ------------------------------------------------- | --------- | ---------- | ------- | ------------------------- |
| sys_kernel_tunables                               | no        | dictionary |         | Set kernel tunables       |
| sys_kernel_tunables.net                           | no        | dictionary |         | Tune network subsystem    |
| sys_kernel_tunables.net.ipv4                      | no        | dictionary |         | Set IPv4 tunables         |
| sys_kernel_tunables.net.ipv4.ip_forwad            | no        | boolean    |         | Set tunable               |
| sys_kernel_tunables.fs                            | no        | dictionary |         | Tune filesystem subsystem |
| sys_kernel_tunables.fs.file_max                   | no        | string     |         | Set tunable               |
| sys_kernel_tunables.fs.inotify                    | no        | dictionary |         | Set inotify tunables      |
| sys_kernel_tunables.fs.inotify.max_queued_events  | no        | string     |         | Set tunable               |
| sys_kernel_tunables.fs.inotify.max_user_instances | no        | string     |         | Set tunable               |
| sys_kernel_tunables.fs.inotify.max_user_watches   | no        | string     |         | Set tunable               |

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
    - bkp_archive
  - serdigital64.system
    - sys_package
    - sys_repository
  - ansible.posix
    - sysctl

### Prerequisites

The Ansible engine must be already installed and configured for privileged access and remote execution.

In addition the following prerequisites can be automatically solved when running the playbook by setting the role action: `resolve_prereq: true`

- Package manager for the target application is installed and enabled.

### Installation Procedure

Manually install Ansible Collections from the Ansible Galaxy repository:

```shell
ansible-galaxy collection install --upgrade serdigital64.system
```

Automatic installation is also available by deploying [A:Platform64](https://aplatform64.readthedocs.io/en/latest/#deployment)

## Contributing

Help on implementing new features and maintaining the code base is welcomed.

Please see the [guidelines](../contributing/guidelines.md) for further details.

## Author

- [SerDigital64](https://serdigital64.github.io/)

## License

[GPL-3.0-or-later](https://www.gnu.org/licenses/gpl-3.0.txt)