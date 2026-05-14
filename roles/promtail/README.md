promtail
========

Installs `promtail` as a systemd service.

Requirements
------------

Role Variables
--------------

(all optional)
- `promtail_version`: Promtail version to install
- `promtail_loki_server`: address of the Loki server
- `promtail_loki_port`: Loki listening port
- `promtail_positions_path`: a YAML file containing last scraped positions in the logs (default: `/var/lib/promtail/positions.yaml`)
- `promtail_custom_scrape_configs`: additional `scrape_configs` configuration
- `promtail_add_var_logs`: scrape the entire `/var/logs` directory (default: `true`)

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
