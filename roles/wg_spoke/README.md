wg_spoke
=========

Configure the host as a Spoke in Wireguard Spoke&Hub topology.

Requirements
------------

Ubuntu 20.04, 22.04 or 24.04.

Role Variables
--------------

```yaml
iface_name: name of the Wireguard interface (network), config file is named after it; WARNING, dashes are not supported
spoke_ipv4_vpn: IPv4 address that this Spoke should expect on the VPN
subnet: something like "10.0.0.0"
netmask: CIDR-style netmask without a slash, e.g. "24"
spoke_pkey: Spoke private key (Wireguard-generated, base64)
hub_pubkey: Hub public key (Wireguard-generated, base64)
hub_ipv4_wan: WAN (Internet) IPv4 address of the Hub
hub_ipv4_vpn: IPv4 address of the Hub on the VPN
hub_port: Hub should be listening on this port
wg_spoke_hide_secrets: whether or not prevent Ansible from logging tasks that handle sensitive info like keys (default is `true`)
wg_spoke_logging: whether or not to send Wireguard dyndbg logs to the kernel buffer accesible via journalctl -ek (default is `true`)
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
