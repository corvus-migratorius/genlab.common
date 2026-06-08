sshd
====

Deploy a hardened `sshd` server

Requirements
------------

None

Role Variables
--------------

- `sshd_disable_pam`: whether to disable PAM support. Default: `false`
- `sshd_password_auth`: whether to allow password authentication. Default: `false`
- `sshd_challenge_response_auth`: whether to allow challenge-response authentication. Default: `false`
- `sshd_gss_api_auth`: whether to allow GSSAPI authentication. Default: `false`
- `sshd_allow_agent_forwarding`: whether to allow SSH agent forwarding. Default: `false`
- `sshd_allow_tcp_forwarding`: whether to allow TCP forwarding. Default: `false`
- `sshd_gateway_ports`: whether to allow gateway ports. Default: `false`
- `sshd_permit_tunnel`: whether to allow SSH tunneling. Default: `false`

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
