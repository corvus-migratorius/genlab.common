loki
====

Installs Loki as a `systemd` service.

Requirements
------------

Role Variables
--------------

- `loki_version`: Loki version to be deployed
- `loki_storage_path`: where to put Loki's files, including log data and positions (default: /data/loki)
- `loki_port`: Loki will listen on this port (default: 3000)
- `loki_log_level`: log level for the service file itself
- `loki_install_logcli`: a toggle for installation of the `logcli` troubleshooting tool

Dependencies
------------

No

Example Playbook
----------------

See: [converge.yml](molecule/default/converge.yml)
      
License
-------

MIT

Author Information
------------------

Alexander Gorelyshev (corvus-migratorius@proton.me) and Danila Danilkin

Genlab LLC
