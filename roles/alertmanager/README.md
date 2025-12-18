alertmanager
=========

The [Alertmanager](https://github.com/prometheus/alertmanager) handles alerts sent by client applications such as the Prometheus server. It takes care of deduplicating, grouping, and routing them to the correct receiver integration such as email, PagerDuty, or OpsGenie. It also takes care of silencing and inhibition of alerts.

You'll need to manually specify the paths to your template files in the main Alertmanager configuration file (`alertmanager.yml`) on the target machine. The configuration file must have a `.yml` suffix, and template files must use a `.tmpl` suffix.

Requirements
------------

None

Role Variables
--------------

```
alertmanager_version: 0.28.1          # version of Alertmanager (AM)
alertmanager_config_dir: "/etc/alertmanager/conf"  # where to place AM configs
alertmanager_storage_dir: "/var/lib/alertmanager"  # path to AM storage
alertmanager_dir: "/etc/alertmanager" # where to install AM on target
alertmanager_user: "alertmanager"     # system user name
alertmanager_group: "alertmanager"    # system group name
config_source_dir: "./alertmanager"   # path to config files on source

# Optional
template_source_dir: "./templates"    # path to template files on source
```

Dependencies
------------

None

Example Playbook
----------------

```yaml
roles:
    - role: genlab.template
      config_source_dir: alertmanager
      alertmanager_version: 0.28.1

```

License
-------

BSD

Author Information
------------------

corvus-migratorius@proton.me
