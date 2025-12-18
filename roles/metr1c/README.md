metr1c
=========

Install metr1c as `systemd` service

Requirements
------------

None

Role Variables
--------------

      metr1c_deploy: set true or false depending on whether we start the service or not, set false when running molecule test
      metr1c_version: metr1c version  to be deployed
      metr1c_cluster_uuid: cluster id
      metr1c_cluster_admin: name of cluster admin
      metr1c_cluster_pw: password to authenticate as cluster admin
      metr1c_platform_version: version of 1c platform
      metr1c_port: metr1c will listen on this port

Dependencies
------------

None

Example Playbook
----------------

```yaml
roles:
  - role: genlab.metr1c
    metr1c_deploy: false
    metr1c_version: "0.0.1"
    metr1c_cluster_uuid: "111-111-111-111"
    metr1c_cluster_admin: "test"
    metr1c_cluster_pw: "testpw"
    metr1c_platform_version: "8.3.24.1467"
    metr1c_port: "1599"
```

License
-------

BSD

Author Information
------------------

Alexander Gorelyshev (corvus-migratorius@proton.me)

Genlab LLC