karma
=========

Install and configure Karma - an alert dashboard for Prometheus Alertmanager (https://github.com/prymitive/karma)


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

See: [converge.yml](molecule/default/converge.yml)

License
-------

BSD

Author Information
------------------

corvus-migratorius@proton.me
