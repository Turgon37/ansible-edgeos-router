Ansible Role EdgeOS Router
========

[![License](https://img.shields.io/badge/license-MIT%20License-brightgreen.svg)](https://opensource.org/licenses/MIT)
[![Ansible Role](https://img.shields.io/badge/ansible%20role-Turgon37.edgeos_router-blue.svg)](https://galaxy.ansible.com/Turgon37/edgeos_router/)

## Description

:grey_exclamation: Before using this role, please know that all my Ansible roles are fully written and accustomed to my IT infrastructure. So, even if they are as generic as possible they will not necessarily fill your needs, I advice you to carrefully analyse what they do and evaluate their capability to be installed securely on your servers.

This roles configure Ubiquity Router with EdgeOS.

## Requirements

Require Ansible >= 2.10 and community.network collection

### Dependencies

## OS Family

This role is available for Ubiquity routers

## Features

At this day the role can be used to :

  * configure edgeos using cli
     * service options
     * system options

## Configuration

### Role

All variables which can be overridden are stored in [defaults/main.yml](defaults/main.yml) file as well as in table below. To see default values please refer to this file.

| Name                                                | Type                | Description                    |
| --------------------------------------------------- | ------------------- | ------------------------------ |
| `edgeos_router__services_enabled_global/group/host` | Map of boolean      | Configure enabled services     |
| `edgeos_router__services_options_global/group/host` | Map of Map of mixed | Configure options for services |
| `edgeos_router__system_options_global/group/host`   | Map of mixed        | Configure system options       |
| `edgeos_router__service_ubnt_discover`              | Boolean                    |                                |
| `edgeos_router__service_unms`                       | Boolean                    |                                |

## Example

### Playbook

* Install and configure a built-in exporter type as follows:

```yaml
- hosts: all
  gather_facts: false
  connection: network_cli
  tasks:
    - import_role: name=turgon37.edgeos_router
  vars:
    ansible_network_os: edgeos

    edgeos_router__services_options_global:
      gui:
        older-ciphers: disable
    edgeos_router__system_options_global:
      analytics-handler:
        send-analytics-report: false
      crash-handler:
        send-crash-report: false
      domain-search:
        domain: 'example.com'
      options:
        reboot-on-panic: true
    edgeos_router__service_ubnt_discover: false
```
