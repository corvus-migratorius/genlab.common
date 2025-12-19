smartctl_exporter
=================

`smartctl` is a command-line utility used to control and monitor the Self-Monitoring, Analysis and Reporting Technology (SMART) system in hard disk drives (HDDs) and solid-state drives (SSDs). `smartctl-exporter` exports `smartctl` statistics to Prometheus.

Requirements
------------

- `smartctl` 

Role Variables
--------------
The exporter will scan the system for available devices if no `--smartctl.device` flags are used. The format of web.config file id described [here](https://github.com/prometheus/exporter-toolkit/blob/master/docs/web-configuration.md). If `smartctl_exp_source_web_config_dir` is defined, role searches for `web_smartctl.conf` file and copy it to target host to `smartctl_exp_web_config_dir` directory

```yaml
smartctl_exp_port: "localhost:9633"  # Addresses on which to expose metrics and web interface. Repeatable for multiple addresses.
smartctl_exp_version: "0.14.0" # exporter version to install
smartctl_exp_dir: "/etc/exporters" # where to download and unarchive expoter 
smartctl_exp_web_config_dir:  "/etc/exporters/config" # Path to configuration file that can enable TLS or authentication
smartctl_exp_interval: "60s" # The interval between smartctl polls
smartctl_exp_rescan: "10m" # The interval between rescanning for new/disappeared devices. If the interval is smaller than 1s no rescanning takes place. If any devices are configured with smartctl.device also no rescanning takes place.
smartctl_exp_devices: [] # The device to monitor (repeatable)
smartctl_exp_device_exclude: "" #Regexp of devices to exclude from automatic scanning. (mutually exclusive to device-include)
smartctl_exp_device_include: "" #  Regexp of devices to include in automatic scanning. (mutually exclusive to device-exclude)
smartctl_exp_web_telemetry_path: "/metrics" # Path under which to expose metrics
smartctl_exp_log_level: "info" # Only log messages with the given severity or above. One of: [debug, info, warn, error]
smartctl_exp_log_format: "logfmt" # Output format of log messages. One of: [logfmt, json]
smartctl_exp_args: # --version --web.systemd-socket 

smartctl_exp_source_web_config_dir: ""
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
