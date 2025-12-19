ipmi_exporter
=========

This Ansible role installs ipmi_exporter on target host. This is a Prometheus exporter for Intelligent Platform Management Interface [metrics](https://github.com/prometheus-community/ipmi_exporter/blob/master/docs/metrics.md)

Requirements
------------

Target node:

- `tar`
- `gzip`
- `freeipmi`

Role Variables
--------------
Configuration files must have names `web_conf.yaml` and `ipmi_local.conf`. If `ipmi_exporter_local_conf` is specified, the role searches for `web_conf.yaml` and `ipmi_local.conf` in that directory and copy to target host in `ipmi_exporter_config_dir`. If the source directory is not specified, the role skips this step. In ipmi_local.conf user can describe what modules to use for metric collection.

ipmi_up{collector="<NAME>"} is 1 if the data for this collector could successfully be retrieved from the remote host, 0 otherwise.

The following collectors are available and can be enabled or disabled in the config:
- ipmi: collects IPMI sensor data. If it fails, sensor metrics (see below) will not be available
- dcmi: collects DCMI data, currently only power consumption. If it fails, power consumption metrics (see below) will not be available
- bmc: collects BMC details. If it fails, BMC info metrics (see below) will not be available
- bmc-watchdog: collects status of the watchdog. If it fails, BMC watchdog metrics (see below) will not be available
- chassis: collects the current chassis power state (on/off). If it fails, the chassis power state metric (see below) will not be available
- sel: collects system event log (SEL) details. If it fails, SEL metrics (see below) will not be available
- sel-events: collects metrics for user-defined events in system event log (SEL). If it fails, SEL entries metrics (see below) will not be available
- sm-lan-mode: collects the "LAN mode" setting in the current BMC config. If it fails, the LAN mode metric (see below) will not be available

- `ipmi_exporter_version`: release version of the exporter
- `ipmi_exporter_config_dir`: where to put configuration files
- `ipmi_exporter_args`:
    - `--[no-]native-ipmi`: Use native IPMI implementation instead of FreeIPMI (EXPERIMENTAL)
    - `--[no-]web.systemd-socket`: Use systemd socket activation listeners instead of port listeners (Linux only).
- `ipmi_exporter_log_level`: "info" # Only log messages with the given severity or above. One of: [debug, info, warn, error]
- `ipmi_exporter_log_format`: "logfmt" # Output format of log messages. One of: [logfmt, json]
- `ipmi_exporter_web_listen_address`: Addresses on which to expose metrics and web interface. Repeatable for multiple addresses.    
    - `:9100` or `[::1]:9100` for HTTP
    - `vsock://:9100` for vsock
- `ipmi_exporter_local_conf`: (optional) Path to local configuration file. See: https://github.com/prometheus-community/ipmi_exporter/blob/master/docs/configuration.md
- `ipmi_exporter_web_conf`: (optional) Path to web configuration file that can enable TLS or authentication. See: https://github.com/prometheus/exporter-toolkit/blob/master/docs/web-configuration.md
```

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
