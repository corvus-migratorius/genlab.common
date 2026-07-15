ovpn_client
===========

This role installs the OpenVPN client packages and deploys a systemd-managed OpenVPN client profile for a specific user. It renders a client configuration from a provided template, writes credentials to an auth file, and restarts/enables the corresponding OpenVPN service unit.

Requirements
------------

- Ansible 2.1 or newer
- A supported target system, such as Ubuntu Jammy/Noble
- A client configuration template supplied through the `ovpn_client_config_src` variable

Role Variables
--------------

The role uses the following variables:

- `ovpn_client_config_dir`: directory where the client config and auth files are stored (default: `/etc/openvpn/client`)
- `ovpn_client_config_path`: full path to the rendered client configuration file (default: `/etc/openvpn/client/{{ ovpn_client_username }}.conf`)
- `ovpn_client_auth_path`: full path to the credentials file (default: `/etc/openvpn/client/{{ ovpn_client_username }}.auth`)
- `ovpn_client_service`: systemd service name to manage (default: `openvpn-client@{{ ovpn_client_username }}.service`)
- `ovpn_client_no_log`: disables logging for the credentials task when set to `true` (default: `true`)
- `ovpn_client_config_src`: source template for the client config file (required)
- `ovpn_client_username`: username written to the auth file (required)
- `ovpn_client_password`: password written to the auth file (required)

Dependencies
------------

None.

Example Playbook
----------------

See: [converge.yml](molecule/default/converge.yml)

License
-------

MIT

Author Information
------------------

Alexander Gorelyshev, Genlab, LLC
