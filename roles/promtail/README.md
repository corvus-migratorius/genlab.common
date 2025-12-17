promtail
=========

Installs promtail as systemd service.

Requirements
------------

Role Variables
--------------

(all optional)
`promtail_version`: version to install
`loki_server`: set loki server
`loki_port`: set loki port
`custom_server_config`: path to custom config witch replace all config with your own
`custom_scrape_configs`: path to custom scrape configs

Dependencies
------------

No

Example Playbook
----------------

    - hosts: servers
      roles:
         - role: promtail
           promtail_version: 2.7.3

License
-------

MIT

Author Information
------------------

Alexander Gorelyshev and Danilkin Danila (MIPT)

Genlab LLC

corvus-migratorius@proton.me
