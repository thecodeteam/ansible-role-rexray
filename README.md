rexray
=========

[![Build Status](https://travis-ci.org/emccode/ansible-role-rexray.svg?branch=master)](https://travis-ci.org/emccode/ansible-role-rexray)

Ansible role that installs and configures [REX-Ray](https://github.com/emccode/rexray).

See http://rexray.readthedocs.org/en/stable/ for details on REX-Ray and specifically how
the REX-Ray config file should be populated.

Requirements
------------

None

Role Variables
--------------

Available variables are listed below, along with their default values (see `vars/main.yml`):

```yaml
rexray_channel: stable
```

The rexray channel refers to where to get the package from and can be one of `stable`,
`unstable`, or `staged`.

```yaml
rexray_service: false
```

This controls whether or not the rexray service/daemon should be started on the node.

```yaml
rexray_storage_drivers: []
```

This is a list of all storage drivers to enable. The default is an empty list, but at least
one storage driver **must** be enabled for REX-Ray to function. Setting this role variable
is therefore **mandatory**.

Each storage driver has driver-specific variables that can be set.  Some are required, some
are optional. Details for each driver can be found in the [User Guide](http://rexray.readthedocs.org/en/stable/).

**AWS**

```yaml
rexray_aws_accesskey: ''
rexray_aws_secretkey: ''
rexray_aws_region: ''
```

**GCE**

```yaml
rexray_gce_keyfile: ''
```

**Isilon**

```yaml
rexray_isilon_endpoint: ''
rexray_isilon_insecure: false
rexray_isilon_username: ''
rexray_isilon_password: ''
rexray_isilon_volumePath: ''
rexray_isilon_nfsHost: ''
```

**OpenStack**

```yaml
rexray_os_authurl: ''
rexray_os_userid: 0
rexray_os_username: ''
rexray_os_password: ''
rexray_os_tenantid: 0
rexray_os_tenantname: ''
rexray_os_domainid: 0
rexray_os_domainname: ''
rexray_os_regionname: ''
rexray_os_availabilityzonename: ''
```

**Rackspace**

```yaml
rexray_rax_authurl: ''
rexray_rax_userid: 0
rexray_rax_username: ''
rexray_rax_password: ''
rexray_rax_tenantid: 0
rexray_rax_tenantname: ''
rexray_rax_domainid: 0
rexray_rax_domainname: ''
```

**ScaleIO**

```yaml
rexray_sio_endpoint: ''
rexray_sio_insecure: false
rexray_sio_usecerts: false
rexray_sio_username: ''
rexray_sio_password: ''
rexray_sio_systemid: 0
rexray_sio_systemname: ''
rexray_sio_protectiondomainid: 0
rexray_sio_protectiondomainname: ''
rexray_sio_storagepoolid: 0
rexray_sio_storagepoolname: ''
```

**VirtualBox**

```yaml
rexray_vbox_endpoint: ''
rexray_vbox_user: ''
rexray_vbox_pass: ''
rexray_vbox_tls: false
rexray_vbox_volume_path: ''
rexray_vbox_controller_name: SATA
rexray_vbox_machine: ''
```

**VMAX**

```yaml
rexray_vmax_smisHost: ''
rexray_vmax_smisPort: ''
rexray_vmax_insecure: false
rexray_vmax_username: ''
rexray_vmax_password: ''
rexray_vmax_sid: ''
rexray_vmax_volumePrefix: ''
rexray_vmax_storageGroup: ''
rexray_vmax_mode: vmh
rexray_vmax_vmh:
  host: ''
  username: ''
  password: ''
  insecure: false
```

**XtremIO**

```yaml
rexray_xtremio_endpoint: ''
rexray_xtremio_userName: ''
rexray_xtremio_password: ''
rexray_xtremio_insecure: false
rexray_xtremio_deviceMapper: false
rexray_xtremio_multipath: false
rexray_xtremio_remoteManagement: false
```

Dependencies
------------

None

Example Playbook
----------------

It is **highly** recommended to use [Ansible Vault](http://docs.ansible.com/ansible/playbooks_vault.html)
for storing sensitive variable values, such as passwords and API keys.

```yaml
- hosts: gce_docker_hosts
  roles:
  - { role: emccode.rexray,
      rexray_service: true,
      rexray_storage_drivers: [gce],
      rexray_gce_keyfile: "/opt/gce_keyfile" }
- hosts: gce_containers
  roles:
  - { role: emccode.rexray,
      rexray_storage_drivers: [gce],
      rexray_gce_keyfile: "/opt/gce_keyfile" }
- hosts: vbox_local_dev_containers
  roles:
  - { role: emccode.rexray,
      rexray_channel: unstable,
      rexray_storage_drivers: [virtualbox],
      rexray_vbox_endpoint: "http://10.0.2.2:18083",
      rexray_vbox_volume_path: "/Users/travis/VirtualBox VMs/Volumes" }
```

License
-------

Apache 2.0

Author Information
------------------

This role created by [Travis Rhoden](https://github.com/codenrhoden), a
developer advocate at [EMC {code}](http://blog.emccode.com).
