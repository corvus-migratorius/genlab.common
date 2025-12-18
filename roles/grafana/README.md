grafana
=========

This ansible role installs [Grafana](https://github.com/grafana/grafana) - the open-source platform for monitoring and observability. It can produce charts, graphs, and alerts for the web when connected to supported data sources.

This role installs and configures Grafana from a binary distribution. It also:

- Uploads custom dashboards

- Installs plugins

- Imports public dashboards and data sources

- Allows admin password changes

Supports user creation
 Grafana service requires an environment file at startup, where you can set custom paths for logs (`grafana_log_dir`), data (`grafana_data_dir`), and plugins (`grafana_plugins_dir`). This allows flexible control over Grafana's data storage.

 Requirements
------------

You need `community.grafana` module. 

Role Variables
--------------

```
grafana_user: "grafana"    # user name
grafana_group: "grafana"   # group name
grafana_version: 11.5.0    # version
grafana_port: 3000         # port

# Directory paths  
grafana_dashboard_dir: "/tmp/grafana/dashboards"          # where to copy dashboards from source  
grafana_plugins_dir: "/var/lib/grafana/plugins"           # where to store plugins on target  
grafana_datasource_dir: "/etc/grafana/provisioning/datasources"  # where to store data sources on target  
grafana_log_dir: "/var/log/grafana"                       # where to write logs  
grafana_data_dir: "/var/lib/grafana"                      # where to store Grafana DB  

# Optional configurations  
grafana_users: []                  # array of user names, passwords, and statuses  
grafana_plugins: []                # array of plugins to install  
grafana_public_dashboards: []      # array of public dashboards to import  

# Admin credentials  
admin_api_username: "secret"       # Grafana admin username  
admin_api_password: "secret"       # Grafana admin password  

# Source paths  
dashboard_source_path: "mydir/dashboards"         # path to dashboards on source server  
datasource_source_path: "mydir/datasources"       # path to data sources on source server  
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
