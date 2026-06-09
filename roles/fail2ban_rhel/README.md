fail2ban_rhel
=============

A small role to deploy `fail2ban` on RHEL/Rocky 9+ hosts. Currently supports only a templated `sshd` jail.

Requirements
------------

- Target hosts must be RHEL-family or Rocky Linux 9+

Supported Platforms
-------------------

- RHEL 9+
- Rocky Linux 9+

Role Variables
--------------

sshd jail configuration

- `fail2ban_rhel_jail_sshd`:
    `enabled`: enable the sshd jail. Default: `true`
    `port`: fail2ban port for sshd. Default: `ssh`
    `logpath`: path to the SSH log file. Default: `/var/log/secure`
    `findtime`: time window for fail2ban. Default: `600`
    `maxretry`: maximum retry count. Default: `5`
    `bantime`: ban duration in seconds. Default: `600`
    `ignoreips`: list of IPs and CIDRs that fail2ban should ignore. Default: `127.0.0.1/8`, `::1`

Behavior
--------

By default this role:

- installs `epel-release` on RedHat-family systems when enabled
- installs `fail2ban`
- creates `/etc/fail2ban/jail.d/sshd.conf` from a template
- enables and starts the `fail2ban` systemd service

Example Playbook
----------------

See: `molecule/default/converge.yml`

License
-------

MIT
