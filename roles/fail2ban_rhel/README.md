# fail2ban_rhel

A small role to deploy a lean `fail2ban` configuration on RHEL/Rocky 9+ hosts.
Currently supports a templated `sshd` jail.

## Requirements

- Target hosts must be RHEL-family or Rocky Linux 9+

## Supported Platforms

- RHEL 9+
- Rocky Linux 9+

## Defaults

The role exposes flat defaults for the `sshd` jail. These values are assembled
into the internal `fail2ban_rhel_jail_sshd` mapping in `vars/main.yml` and then
rendered into `/etc/fail2ban/jail.d/sshd.local`.

| Variable | Default | Description |
| --- | --- | --- |
| `fail2ban_rhel_jail_sshd_enabled` | `true` | Enable the `sshd` jail. |
| `fail2ban_rhel_jail_sshd_port` | `ssh` | Port or service name watched by the jail. |
| `fail2ban_rhel_jail_sshd_findtime` | `600` | Time window, in seconds, used when counting failures. |
| `fail2ban_rhel_jail_sshd_maxretry` | `5` | Number of failures allowed within `findtime`. |
| `fail2ban_rhel_jail_sshd_bantime` | `3600` | Ban duration, in seconds. |
| `fail2ban_rhel_jail_sshd_logpath` | `%(sshd_log)s` | Fail2Ban's platform default SSH log path token. |
| `fail2ban_rhel_jail_sshd_backend` | `%(sshd_backend)s` | Fail2Ban's platform default SSH backend token. |
| `fail2ban_rhel_jail_sshd_banaction` | `firewallcmd-multiport` | Ban action used by the jail. |
| `fail2ban_rhel_jail_sshd_ignoreips` | `127.0.0.1/8`, `::1` | IPs and CIDRs that should never be banned. |

## Internal Vars

`vars/main.yml` builds the `fail2ban_rhel_jail_sshd` dictionary consumed by the
`sshd.conf.j2` template:

```yaml
fail2ban_rhel_jail_sshd:
  enabled: "{{ fail2ban_rhel_jail_sshd_enabled }}"
  port: "{{ fail2ban_rhel_jail_sshd_port }}"
  findtime: "{{ fail2ban_rhel_jail_sshd_findtime }}"
  maxretry: "{{ fail2ban_rhel_jail_sshd_maxretry }}"
  bantime: "{{ fail2ban_rhel_jail_sshd_bantime }}"
  logpath: "{{ fail2ban_rhel_jail_sshd_logpath }}"
  backend: "{{ fail2ban_rhel_jail_sshd_backend }}"
  banaction: "{{ fail2ban_rhel_jail_sshd_banaction }}"
  ignoreips: "{{ fail2ban_rhel_jail_sshd_ignoreips }}"
```

Override the flat defaults, not the internal mapping, unless you intentionally
want to replace the rendered jail data.

## Behavior

By default this role:

- installs `epel-release`
- installs `fail2ban`
- renders `/etc/fail2ban/jail.d/sshd.local` from `templates/sshd.conf.j2`
- restarts and enables `fail2ban` when the rendered jail changes

## Example Playbook

```yaml
- name: Converge
  hosts: all
  roles:
    - role: genlab.common.fail2ban_rhel
      fail2ban_rhel_jail_sshd_maxretry: 4
      fail2ban_rhel_jail_sshd_bantime: 7200
```

See also: `molecule/default/converge.yml`

## License

MIT
