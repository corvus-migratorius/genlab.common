sshd
====

A hardened OpenSSH server role for Debian/Ubuntu and RHEL/Rocky systems.

This role installs and configures the `sshd` server with secure defaults and a small set of tunable options for authentication and forwarding.

Requirements
------------

- Target hosts must be Debian-family or RedHat-family Linux systems

Supported Platforms
-------------------

- Debian
- Ubuntu
- RHEL 9+
- Rocky Linux 9+

Role Variables
--------------

Access control

- `sshd_v2_allow_users`: optional space-separated list of users permitted to log in via SSH
- `sshd_v2_allow_groups`: optional space-separated list of groups permitted to log in via SSH

Behavior
--------

By default this role:

- installs `openssh-server`
- enforces `Protocol 2`
- disables `PermitRootLogin`
- disables `X11Forwarding`, `HostbasedAuthentication`, `KbdInteractiveAuthentication`, and `PermitUserEnvironment`
- disables weak(-er) host keys (`ecdsa`, `dsa`)
- disables empty passwords
- configure `LogLevel` (default: `INFO`)

Compatibility Notes
-------------------

- The role uses `sshd` validation via `/usr/sbin/sshd -t -f %s`.
- Debian/Ubuntu systems use the `ssh` service name; RHEL/Rocky systems use `sshd`.
- The role is intentionally conservative with forwarding and tunneling defaults.

Example Playbook
----------------

See: [converge.yml](molecule/default/converge.yml)

Dependencies
------------

None

License
-------

BSD

Author Information
------------------

corvus-migratorius@proton.me
