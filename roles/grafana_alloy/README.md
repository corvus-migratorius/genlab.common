# grafana_alloy

Install Grafana Alloy binary from GitHub.

Install Grafana Alloy from the release binary and configures it to scrape log files and push them to Loki. RHEL / CentOS / Rocky. 

## Variables

```yaml
alloy_version: "1.17.1"
alloy_config_dir: "/etc/alloy"
alloy_data_dir: "/var/lib/alloy"
alloy_loki_url: "http://localhost:3100/loki/api/v1/push"
alloy_log_paths:
  - "/var/log/*.log"
```

## Usage

```yaml
- hosts: log_shippers
  become: true
  roles:
    - role: grafana_alloy
      vars:
        alloy_loki_url: "http://loki.example.com:3100/loki/api/v1/push"
        alloy_log_paths:
          - "/var/log/*.log"
          - "/var/log/myapp/*.log"
```
