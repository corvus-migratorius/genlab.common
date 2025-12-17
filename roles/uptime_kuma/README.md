ansible-uptime-kuma
=========

[![linters](https://github.com/corvus-migratorius/ansible-uptime-kuma/actions/workflows/linters.yaml/badge.svg)](https://github.com/corvus-migratorius/ansible-uptime-kuma/actions/workflows/linters.yaml)
[![kics](https://github.com/corvus-migratorius/ansible-uptime-kuma/actions/workflows/kics.yml/badge.svg)](https://github.com/corvus-migratorius/ansible-uptime-kuma/actions/workflows/kics.yml)
[![molecule](https://github.com/corvus-migratorius/ansible-uptime-kuma/actions/workflows/molecule.yaml/badge.svg)](https://github.com/corvus-migratorius/ansible-uptime-kuma/actions/workflows/molecule.yaml)

Deploy and confugure a containerized instance of [uptime-kuma](https://github.com/louislam/uptime-kuma).

Requirements
------------

None

Role Variables
--------------

- `kuma_img_version`: Kuma container version
- `kuma_project_dir`: where to put Docker Compose file and keep Kuma's data
- `kuma_port`: listening port for Kuma API and web interface
- `kuma_api_version`: version of the Python API
- `kuma_limit_cpus`: CPU cores limit for Kuma
- `kuma_limit_ram`: RAM limit for Kuma
- `kuma_tg_notif_name`: Name for Telegram notification method
- `kuma_tg_notif_is_default`: make this notification method default (default: `true`)
- `kuma_tg_notif_apply_existing`: connect all existing monitors to this notification method (default: `true`)
- `kuma_tg_bot_token`: Telegram bot token for the bot that will be delivering messages
- `kuma_tg_chat_id`: Telegram chat/group where the bot should deliver messages (bot must be a member there)
- `kuma_tg_notif_state`: `present` (default) or `absent`

Dependencies
------------

- `genlab.docker_ubuntu`

Example Playbook
----------------

See `molecule/default/converge`.

License
-------

BSD

Author Information
------------------

corvus-migratorius@proton.me
