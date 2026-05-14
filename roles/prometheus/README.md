prometheus
==========

Install [Prometheus](https://github.com/prometheus/prometheus) binary from GitHub.

Prometheus collects metrics from configured targets at given intervals, evaluates rule expressions, displays the results, and can trigger alerts when specified conditions are observed.

Prometheus configuration files and rules should be placed in separate directories in the source. They must have a `*.yml` suffix. You'll need to manually specify the paths to your rule files in the main Prometheus configuration file (prometheus.yml) on the target machine

Requirements
------------

Target node:

- `tar`
- `gzip`

Role Variables
--------------

- `prometheus_version`: the desired Prometheus version
- `prometheus_config_source_dir`: where to find config files on the controller
- `prometheus_config_dir`: path for Prometheus configuration file on the target machine 
- `prometheus_db_dir`: location for the TSDB files
- `prometheus_alertrules_source_dir`: where to find alert rules on the controller
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
sayganova@genlab.llc
