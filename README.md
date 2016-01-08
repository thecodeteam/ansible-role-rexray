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
