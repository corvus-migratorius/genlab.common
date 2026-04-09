win_firewall
=========

Configure windows hosts as a Spoke in the Wireguard Spoke-and-Hub topology.

Requirements
------------

None

Role Variables
--------------

```yaml
win_firewall_name: name     # Required

# Default variables
win_firewall_action: allow
win_firewall_direction: in
win_firewall_enabled: true
win_firewall_localip: any
win_firewall_localport: any
win_firewall_profiles: domain,private,public
win_firewall_program: any
win_firewall_protocol: any
win_firewall_remoteip: any
win_firewall_remoteport: any
win_firewall_service: any
win_firewall_state: present
```

Dependencies
------------

ansible.windows
community.windows

Example Playbook
----------------

```yaml
roles:
  - role: genlab.common.win_firewall
    win_firewall_name: Allow port 1234 to 10.0.0.0/24
    win_firewall_action: allow
    win_firewall_localport: 1234
    win_firewall_remoteip: 10.0.0.0/24
```

License
-------

BSD

Author Information
------------------

malyuk.ss@genlab.llc
