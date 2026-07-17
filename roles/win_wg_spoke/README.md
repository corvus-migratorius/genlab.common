win_wg_spoke
=========

Configure windows hosts as a Spoke in the Wireguard Spoke-and-Hub topology.

Requirements
------------

None

Role Variables
--------------

None

Dependencies
------------

ansible.windows

Example Playbook
----------------

```yaml
roles:
  - role: genlab.common.win_wg_spoke
    win_wg_spoke_iface_name: wg0
    win_wg_spoke_subnet: "10.0.0.0"
    win_wg_spoke_netmask: "24"
    win_wg_spoke_ipv4_vpn: "10.0.0.1"
    win_wg_spoke_port: "51820"
    win_wg_spoke_pkey: eGqGx4A5ufFKatLflPFKNuzFgGuospIe08iPbTlEhm0=
    win_wg_spoke_hub_pubkey: EvcoZ21/p0AHz5y95jwjVIR9puljc2kXqh/f3U1A4nk=
    win_wg_spoke_psk: 5qmMuLuGQT7w8VnHPsZDO4vRF5wEKcpEtaCQW1BLmbg=  # optional
    win_wg_spoke_hub_ipv4_wan: "1.2.3.4"
    win_wg_spoke_hub_port: "51820"
    win_wg_spoke_dns_server: "10.0.0.254"   # optional
    win_wg_spoke_domain: "corp.local"       # optional
```

License
-------

BSD

Author Information
------------------

malyuk.ss@genlab.llc
