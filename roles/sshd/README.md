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

Authentication

- `sshd_disable_pam`: disable PAM support in `sshd_config`. Default: `false`
- `sshd_password_auth`: allow password authentication. Default: `false`
- `sshd_challenge_response_auth`: allow challenge-response authentication. Default: `false`
- `sshd_gss_api_auth`: allow GSSAPI authentication. Default: `false`

Forwarding & tunneling

- `sshd_allow_agent_forwarding`: allow SSH agent forwarding. Default: `false`
- `sshd_allow_tcp_forwarding`: allow TCP forwarding. Default: `false`
- `sshd_gateway_ports`: allow gateway ports. Default: `false`
- `sshd_permit_tunnel`: allow SSH tunneling. Default: `false`

Access control

- `sshd_allow_users`: optional space-separated list of users permitted to log in via SSH
- `sshd_allow_groups`: optional space-separated list of groups permitted to log in via SSH

Behavior
--------

By default this role:

- installs `openssh-server`
- enforces `Protocol 2`
- disables `PermitRootLogin`
- disables `X11Forwarding`, `HostbasedAuthentication`, `KbdInteractiveAuthentication`, and `PermitUserEnvironment`
- disables weak(-er) host keys (`ecdsa`, `dsa`)
- disables empty passwords
- sets `LogLevel VERBOSE`
- restricts `/etc/ssh/sshd_config` to `0600`

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
