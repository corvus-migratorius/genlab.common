# ovpn_server

Ansible role to deploy an OpenVPN Community server (EL9-targeted packaging),
authenticating users via the PAM plugin and an SSSD-backed directory when
appropriate. The role focuses on a secure, minimal server footprint and
expects PKI material to be supplied by the controller (Ansible Vault or a
secrets backend) rather than generated in-role.

## Scope

- Installs the packaged OpenVPN and supporting packages (EPEL repository used
  on EL9).
- Places supplied PKI/secret files into the server instance directory — the
  role does not generate CA/server certificates itself.
- Configures the `openvpn` systemd instance `openvpn-server@<instance>.service`.
- Configures a PAM service to use SSSD by default and enables deferred PAM authentication
  to avoid blocking on slow directory lookups.
- Optionally manages IPv4 forwarding and opens the listener in `firewalld`.
- Does not perform FreeIPA enrollment or create network-wide forwarding/NAT
  policies — those are site responsibilities.

Set `ovpn_server_verify_client_cert: none` only when intentionally running a
password-only service (no client certificates).

## Collections

Install test and helper collections used by CI and Molecule:

```shell
ansible-galaxy collection install -r requirements.yml
```

## Role variables

The role documents common variables with their defaults. See
[defaults/main.yml](defaults/main.yml) for the canonical source.

- `ovpn_server_instance` (default: `server`): OpenVPN instance name used by the
  systemd template unit.
- `ovpn_server_port` (default: `1194`): UDP/TCP listener port.
- `ovpn_server_proto` (default: `udp`): Listener protocol.
- `ovpn_server_dev` (default: `tun0`): Tunnel device name.
- `ovpn_server_config_path` (default: `/etc/openvpn/server/{{ ovpn_server_instance }}.conf`):
  Path to the active configuration file.
- PKI/secret contents (supply either `_content` variables or place files under
  the expected paths):
  - `ovpn_server_ca_content` (default: `""`)
  - `ovpn_server_cert_content` (default: `""`)
  - `ovpn_server_key_content` (default: `""`)
  - `ovpn_server_tls_crypt_key_content` (default: `""`)
  - `ovpn_server_crl_content` (default: empty — optional)
- `ovpn_server_verify_client_cert` (default: `require`): `require` for
  certificate + PAM auth, or `none` for password-only.
- `ovpn_server_deferred_auth_pam` (default: `true`): enable deferred PAM
  processing to avoid blocking the worker thread on directory lookups.
- `ovpn_server_push_options` (default: `[]`): list of client-push options
  (routes, DHCP options, etc.).
- `ovpn_server_manage_firewalld` (default: `true`) / `ovpn_server_firewalld_zone`
  (default: `public`): optional firewalld management and zone selection.
  Use `ovpn_server_firewalld_default_zone` (default: `public`) to select the
  host default zone where the `openvpn` service will be enabled. The role will
  create a tunnel zone named by `ovpn_server_firewalld_tunnel_zone` (default:
  `ovpn`) and enable any services listed in
  `ovpn_server_firewalld_tunnel_zone_services`.

  If you want the role to provision a firewalld policy file, supply
  `ovpn_server_firewalld_policy_name` and `ovpn_server_firewalld_policy_content`.
  If `ovpn_server_firewalld_policy_name` is empty the role will not write a
  policy file.
- `ovpn_server_manage_ip_forwarding` (default: `true`): enables
  `net.ipv4.ip_forward` when true.
- Encryption-related defaults:
  - `ovpn_server_tls_version_min` (default: `"1.2"`)
  - `ovpn_server_data_ciphers` (default: `['AES-256-GCM','AES-128-GCM']`)
  - `ovpn_server_tls_crypt_enabled` (default: `true`)

For the full list of variables and their defaults, consult
[defaults/main.yml](defaults/main.yml).

## Example playbook

Store private keys and `tls-crypt` keys in Ansible Vault or a secrets
backend. Example minimal role usage:

```yaml
- name: Deploy OpenVPN server
  hosts: vpn_servers
  become: true
  roles:
    - role: ovpn_server
      vars:
        ovpn_server_ca_content: "{{ vault_openvpn_ca_certificate }}"
        ovpn_server_cert_content: "{{ vault_ovpn_server_certificate }}"
        ovpn_server_key_content: "{{ vault_ovpn_server_private_key }}"
        ovpn_server_tls_crypt_key_content: "{{ vault_openvpn_tls_crypt_key }}"
        ovpn_server_crl_content: "{{ vault_openvpn_crl }}"
        ovpn_server_push_options:
          - "route 192.0.2.0 255.255.255.0"
          - "dhcp-option DNS 192.0.2.53"
```

Generate a `tls-crypt` key locally with:

```shell
openvpn --genkey tls-crypt tls-crypt.key
```

### Password-only mode

To run an authentication service that uses only PAM (no client certificates):

```yaml
ovpn_server_verify_client_cert: none
ovpn_server_crl_enabled: false
```

## FreeIPA / SSSD notes

This role does not enroll hosts into FreeIPA or manage `/etc/sssd/sssd.conf`.
When using SSSD/FreeIPA ensure the PAM service name `openvpn` is permitted by
HBAC rules. The default PAM stack configured by the role uses `pam_sss.so` for
both `auth` and `account` phases. Example PAM fragment:

```pam
auth       required     pam_sss.so
account    required     pam_sss.so
```

If your environment requires a different PAM stack (for example an
`authselect`-managed `password-auth` stack) override
`ovpn_server_pam_stack`.

## Routing and firewall policy

The role can enable IPv4 forwarding and open the OpenVPN listener in
`firewalld`. It deliberately does not create permissive zone assignments or
automatic masquerading; those network policies are site-specific and should be
handled outside the role (or via an explicit playbook that configures the host
networking to match your topology).

## Molecule tests

The provided scenario does not test actual OpenVPN server functionality in
a container environment.
The verifications tests formally check installed packages and availability
of deployed files, and nothing more.

## Documentation & references

- OpenVPN auth-pam plugin README
- OpenVPN Community 2.5 manual
- SSSD troubleshooting: https://sssd.io/troubleshooting/basics.html

## License

MIT

## Author

Alexander Gorelyshev, corvus-migratorius@proton.me
