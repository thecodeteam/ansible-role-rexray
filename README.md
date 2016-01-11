rexray
=========

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
are optional. Details for each driver can be found in the [User Guide)[http://rexray.readthedocs.org/en/stable/].

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

Dependencies
------------

None

Example Playbook
----------------

```yaml
- hosts: docker_hosts
  roles:
  - { role: codenrhoden.rexray, rexray_service: true }
- hosts: persistent_store_containers
  roles:
  - { role: codenrhoden.rexray }
- hosts: experimental_containers
  roles:
  - { role: codenrhoden.rexray, rexray_channel: unstable }
```

License
-------

Apache 2.0

Author Information
------------------

This role created by [Travis Rhoden](https://github.com/codenrhoden), a
developer advocate at [EMC {code}](http://blog.emccode.com).
