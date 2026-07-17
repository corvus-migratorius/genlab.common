caddy
========

Installs `caddy` as a systemd service.

Requirements
------------

Role Variables
--------------

- `caddy_version`: default `2.11.3`
- `caddy_src_conf_path`: (required) location of the `Caddyfile` on the controller
- `caddy_dest_conf_path`: where to put the configuration file for the service default `/etc/caddy/Caddyfile`
- `caddy_limit_nofile`: default `1048576`

Dependencies
------------

None

Example Playbook
----------------

See: [converge.yml](molecule/default/converge.yml)

License
-------

MIT

Author Information
------------------

Alexander Gorelyshev

corvus-migratorius@proton.me
