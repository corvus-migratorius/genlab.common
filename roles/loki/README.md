loki
====

Installs Loki as a `systemd` service.

Requirements
------------

Role Variables
--------------

```yaml
loki_version: Loki version to be deployed
loki_storage_path: where to put Loki's files, including log data and positions (default: /data/loki)
loki_port: Loki will listen on this port (default: 3000)
```

Dependencies
------------

No

Example Playbook
----------------

```yaml
roles:
  - role: loki
    loki_version: 2.7.3
```
      

License
-------

MIT

Author Information
------------------

Alexander Gorelyshev (corvus-migratorius@proton.me) and Danila Danilkin

Genlab LLC
