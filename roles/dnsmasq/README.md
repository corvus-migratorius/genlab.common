dnsmasq
=========

Deploy dnsmasq on the target node. For now, supports only DNS functionality (DHCP and TFTP are not configuratble).

Requirements
------------

Take care to open the port you choose for dnsmasq to serve queries on. This role does not handle firewall configuration. 

Role Variables
--------------

None

Dependencies
------------

None

Example Playbook
----------------

```yaml
roles:
    - role: genlab.dnsmasq
```

License
-------

BSD

Author Information
------------------

corvus-migratorius@proton.me
