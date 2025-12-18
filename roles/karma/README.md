karma
=========
This is the ansible role to install and configure Karma - alert dashboard for Prometheus Alertmanager (https://github.com/prymitive/karma)

------------
⚠️ Do not forget to update:

- `meta/main.yml`
- Conda/Mamba manifests
- this README =) including *the name at the top* and *maintainers*.

Requirements
------------

None

Role Variables
--------------
```yaml
karma_version: "0.121" - karma version
karma_user: karma - name of karma system user
karma_group: karma - name of karma system group
karma_dir: /etc/karma - path where to unpack karma
karma_config_dir: /etc/karma/conf - where to copy configuration file
config_source_dir: source - path to source dir with karma config on localhost
```

Dependencies
------------

None

Example Playbook
----------------

```yaml
roles:
    - role: genlab.karma
      karma_version: "0.121"
      config_source_dir: "karma/"
      karma_dir: "/etc/karma"
      karma_config_dir: "/etc/karma/config"
```

License
-------

BSD

Author Information
------------------

corvus-migratorius@proton.me
