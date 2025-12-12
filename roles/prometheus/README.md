genlab.prometheus
=========

This ansible role installs [Prometheus](https://github.com/prometheus/prometheus) from binary distribution. Prometheus is a systems and service monitoring system. It collects metrics from configured targets at given intervals, evaluates rule expressions, displays the results, and can trigger alerts when specified conditions are observed.

Prometheus configuration files and rules should be placed in separate directories in the source. They must have a `*.yml` suffix. You'll need to manually specify the paths to your rule files in the main Prometheus configuration file (prometheus.yml) on the target machine

Requirements
------------

None

Role Variables
--------------
```
prometheus_version: 3.2.1                 # prometheus version
prometheus_dir: "/etc/prometheus"         # where to install prometheus
prometheus_user: prometheus               # user name
prometheus_group: prometheus              # groups name
prometheus_config_dir: "/etc/prometheus/conf"        # where to place prometheus config
prometheus_db_dir: "/var/lib/prometheus"             # where to store prometheus db
prometheus_config_source_dir: prometheus             # path to config files on source
prometheus_alertrules_source_dir: prometheus/rules   # path to rule files  on source
```

Dependencies
------------

None

Example Playbook
----------------

```yaml
roles:
    - role: genlab.prometheus
      prometheus_config_source_dir: mydir/configs
      prometheus_alertrules_source_dir: mydir/configs/rules
      prometheus_version: 3.2.1
```

License
-------

BSD

Author Information
------------------

corvus-migratorius@proton.me
