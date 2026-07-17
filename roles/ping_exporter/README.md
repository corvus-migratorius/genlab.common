ping_exporter
=============

Deploy `czerwonk/ping_exporter` as a systemd service and configure the ICMP
targets exported to Prometheus.

The role installs the upstream GitHub release package for the target OS family:

- Debian family hosts install the `.deb` package with `apt`.
- RHEL family hosts install the `.rpm` package with `dnf`.

It renders `/etc/ping_exporter/config.yml` from `templates/config.yml.j2`, then
restarts and enables the `ping_exporter` systemd unit.

Requirements
------------

Target node:

- systemd
- Debian-family or RHEL-family package manager support
- Network access to GitHub releases when installing the package

Role Variables
--------------

Available defaults:

| Variable | Default | Description |
| --- | --- | --- |
| `ping_exporter_version` | `1.2.1` | Upstream version to install. |
| `ping_exporter_interval` | `5s` | How often to ping each target. |
| `ping_exporter_timeout` | `4s` | Timeout for a single ICMP echo request. |
| `ping_exporter_history_size` | `42` | Number of ping results retained per target. |
| `ping_exporter_payload_size` | `56` | ICMP payload size. |
| `ping_exporter_targets` | `["1.1.1.1"]` | List of target hostnames or IP addresses written to `config.yml`. |

The rendered configuration has this shape:

```yaml
targets:
  - host: "1.1.1.1"
    alias: cloudflare-dns

ping:
  interval: 5s
  timeout: 4s
  history-size: 42
  payload-size: 56
```

Dependencies
------------

None.

Example Playbook
----------------

```yaml
---
- name: Deploy ping_exporter
  hosts: all
  roles:
    - role: genlab.common.ping_exporter
      ping_exporter_targets:
        - host: "1.1.1.1"
          alias: cloudflare-dns
      ping_exporter_interval: "10s"
```

Testing
-------

The Molecule default scenario converges the role with `127.0.0.1` as a target
and verifies that `http://127.0.0.1:9427/metrics` returns HTTP 200 with
`ping_up` metrics.

License
-------

GPL-2.0-or-later

Author Information
------------------

Alexander Gorelyshev (corvus-migratorius@proton.me)
