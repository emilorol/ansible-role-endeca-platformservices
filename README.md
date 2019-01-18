endeca_platformservices
=========
[![License](https://img.shields.io/badge/license-Apache-green.svg?style=flat)](https://raw.githubusercontent.com/lean-delivery/ansible-role-endeca-platformservices/master/LICENSE)
[![Build Status](https://travis-ci.org/lean-delivery/ansible-role-endeca-platformservices.svg?branch=master)](https://travis-ci.org/lean-delivery/ansible-role-endeca-platformservices)
[![Build Status](https://gitlab.com/lean-delivery/ansible-role-endeca-platformservices/badges/master/build.svg)](https://gitlab.com/lean-delivery/ansible-role-endeca-platformservices)
[![Galaxy](https://img.shields.io/badge/galaxy-lean__delivery.endeca__platformservices-blue.svg)](https://galaxy.ansible.com/lean_delivery/endeca_platformservices)
![Ansible](https://img.shields.io/ansible/role/d/29401.svg)
![Ansible](https://img.shields.io/badge/dynamic/json.svg?label=min_ansible_version&url=https%3A%2F%2Fgalaxy.ansible.com%2Fapi%2Fv1%2Froles%2F29401%2F&query=$.min_ansible_version)

## Summary
--------------

This role installs Oracle Endeca PlatformServices on Linux platforms which consists of a number of components that are used to build Endeca applications in support of the Endeca MDEX Engine.


Requirements
------------

 - Minimal Version of the ansible for installation: 2.5
 - **Supported PlatformServices versions**:
   - 6.x.x
   - 11.x
   - _higher versions should be retested_
 - **Supported OS**:
   - CentOS
     - 6
     - 7

For more information regarding support matrix please visit <https://support.oracle.com>

MDEX Engine should be installed preliminarily:
  - lean_delivery.endeca_mdex

```
For test scenarios endeca_platformservices/requirements.yml is used
If another roles/versions are required, put requirements.yml to molecule/<scenario_name> and remove in molecule.yml lines
  options:
    role-file: requirements.yml
```

Role Variables
--------------

  - `transport` - artifact source transport
     Available:
      - `web` - fetch artifact from custom web uri
      - `local` - local artifact

  - `transport_web` - URI for http/https artifact  e.g. "http://my-storage.example.com/V861206-01.zip"
  - `transport_local` - path for local artifact e.g. "/tmp/V861206-01.zip"

  - `download_path` - local folder for downloading artifacts
    default: `/tmp/`

  - `ps_version` - Endeca PlatformServices version

```
Set  PlatformServices version as it's defined in official Oracle Documentation
```

  - `base_root` - where PlatformServices should be installed
    default: `/opt`

  - `ps_service` - name of the service
    default: `endeca-platformservices`

  - `install_set` - set chosen set for silent installation
    Available:
      - `Complete`
      - `Typical`
      - `PS-ACA` - PS & App Controller Agent
      - `Ref-Impl` - Reference Implementation

  - `etools_http_port` - EAC (Endeca Application Controller) Service Port
    default: `8888`

  - `etools_server_port` - EAC Service Shutdown Port
    default: `8090`

```
Parameters for PlatformServices versions lower 11.2
```

  - `etools_jcd_port` - Endeca Control System JCD
    default: `8088`

  - `install_eac_controller` - should be installed Endeca Application Controller (EAC) with EAC Agent
    default: `False`


Example Playbook
----------------

### Installing Endeca PlatformServices 11.3.0 from local:
```yaml
- name: "Install PlatformServices 11.3.0 from local"
  hosts: all

  roles:
    - role: lean_delivery.endeca_mdex
      transport: "local"
      transport_local: "/tmp/V861206-01.zip"
    - role: lean_delivery.endeca_platformservices
      ps_version: "11.3.0"
      transport: "local"
      transport_local: "/tmp/V861203-01.zip"
  vars:
    mdex_version: "11.3.0"
```

### Installing Endeca PlatformServices 11.3.0 from web:
```yaml
- name: "Install PlatformServices 11.3.0 from web"
  hosts: all

  roles:
    - role: lean_delivery.endeca_mdex
      transport: "web"
      transport_web: "http://my-storage.example.com/V861206-01.zip"
    - role: lean_delivery.endeca_platformservices
      ps_version: "11.3.0"
      transport: "web"
      transport_web: "http://my-storage.example.com/V861203-01.zip"
  vars:
    mdex_version: "11.3.0"
```

License
-------
Apache

Author Information
------------------

authors:
  - Lean Delivery Team <team@lean-delivery.com>
