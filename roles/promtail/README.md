promtail
========

Installs `promtail` as a systemd service.

Requirements
------------

Role Variables
--------------

(all optional)
`promtail_version`: version to install
`promtail_loki_server`: set loki server
`promtail_loki_port`: set loki port
`custom_server_config`: path to custom config witch replace all config with your own
`custom_scrape_configs`: path to custom scrape configs

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

Alexander Gorelyshev and Danilkin Danila (MIPT)

corvus-migratorius@proton.me
