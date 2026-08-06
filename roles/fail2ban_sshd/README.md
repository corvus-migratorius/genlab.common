# fail2ban_sshd

This role installs and configures Fail2Ban for the sshd jail on Ubuntu and EL-based hosts.

## What this role does

By default, the role will:

- check the currently installed Fail2Ban version
- install or upgrade Fail2Ban to the requested package version
- install EPEL release on RedHat-family systems when needed
- render /etc/fail2ban/jail.d/sshd.local from the shipped Jinja template
- ensure the Fail2Ban service is enabled and running
- restore SELinux contexts for /etc/fail2ban on EL systems

## Supported platforms

The role metadata currently targets:

- Ubuntu noble
- Enterprise Linux 9

## Variables

The role exposes the following variables in defaults/main.yml:

- fail2ban_sshd_version – package version to install (default: 1.0.2-3ubuntu0.1)
- fail2ban_sshd_jail_enabled – enable the sshd jail (default: true)
- fail2ban_sshd_jail_port – port or service name watched by the jail (default: ssh)
- fail2ban_sshd_jail_findtime – time window for counting failures (default: 600)
- fail2ban_sshd_jail_maxretry – number of failures allowed in the findtime window (default: 5)
- fail2ban_sshd_jail_bantime – ban duration in seconds (default: 3600)
- fail2ban_sshd_jail_logpath – SSH log path used by the jail (default: null)
- fail2ban_sshd_jail_backend – backend used by the jail (default: systemd)
- fail2ban_sshd_jail_ignoreips – IPs or CIDRs that should be ignored (default: 127.0.0.1/8 and ::1)

## Example playbook

```yaml
- name: Converge
  hosts: all
  roles:
    - role: genlab.common.fail2ban_sshd
      fail2ban_sshd_version: "1.0.2-3ubuntu0.1"
      fail2ban_sshd_jail_maxretry: 5
      fail2ban_sshd_jail_bantime: 3600
```

## Notes

The current scope is deliberately focused on a single jail: sshd. The role does not define additional Fail2Ban jails or custom actions beyond the supplied template.

## License

MIT
