wg_spoke
=========

Configure the host as a Spoke in the Wireguard Spoke-and-Hub topology.

Requirements
------------

Ubuntu 22.04 or 24.04.

Role Variables
--------------

```yaml
wg_spoke_iface_name: name of the Wireguard interface (network), config file is named after it; WARNING, dashes are not supported by Wireguard
wg_spoke_spoke_ipv4_vpn: IPv4 address that this Spoke should expect within the VPN
wg_spoke_subnet: something like "10.0.0.0"
wg_spoke_netmask: CIDR-style netmask without a slash, e.g. "24"
wg_spoke_spoke_pkey: Spoke private key (Wireguard-generated, base64)
wg_spoke_hub_pubkey: Hub public key (Wireguard-generated, base64)
wg_spoke_hub_ipv4_wan: WAN (Internet) IPv4 address of the Hub
wg_spoke_hub_ipv4_vpn: IPv4 address of the Hub on the VPN
wg_spoke_hub_port: Hub should be listening on this port
wg_spoke_hide_secrets: whether or not prevent Ansible from logging tasks that handle sensitive info like keys (default is `true`)
wg_spoke_logging: whether or not to send Wireguard dyndbg logs to the kernel buffer accesible via `journalctl -ek` (default is `true`)
```

Dependencies
------------

None

Example Playbook
----------------

See: [converge.yml](molecule/default/converge.yml)

License
-------

BSD

Author Information
------------------

corvus-migratorius@proton.me
