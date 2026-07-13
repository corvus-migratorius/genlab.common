Role Name
=========

Download, configure and deploy Prometheus `cnexporter` as a systemd unit.

Requirements
------------

- Linux
- x86_64/amd64

Role Variables
--------------

- `cgrpuser_exporter_ver`: version (tag) identifying the Github release to be downloaded
- `cgrpuser_exporter_bin_path`: a pathway to install the `cgrpuser-exporter` executable
- `cgrpuser_exporter_port`: the exporter will serve its `/metrics` endpoint at this TCP port
- `cgrpuser_exporter_timeout`: time interval between polling Docker API for container info (seconds)

Dependencies
------------

None

Example Playbook
----------------

```yaml
    - role: cgrpuser_exporter
      cgrpuser_exporter_ver: "0.1.1"
```

License
-------

MIT

Author Information
------------------

corvus-migratorius@proton.me