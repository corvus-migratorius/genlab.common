# grafana_alloy

Install Grafana Alloy binary from GitHub.

Install Grafana Alloy from the release binary and configures it to scrape log files and push them to Loki. RHEL / CentOS / Rocky. 

## Variables

```yaml
grafana_alloy_version: "1.17.1"
grafana_alloy_config_dir: "/etc/alloy"
grafana_alloy_data_dir: "/var/lib/alloy"
grafana_alloy_loki_url: "http://localhost:3100/loki/api/v1/push"
grafana_alloy_log_paths:
  - "/var/log/*.log"
```

## Usage

```yaml
- hosts: log_shippers
  become: true
  roles:
    - role: grafana_alloy
      vars:
        grafana_alloy_loki_url: "http://loki.example.com:3100/loki/api/v1/push"
        grafana_alloy_log_paths:
          - "/var/log/*.log"
          - "/var/log/myapp/*.log"
```
