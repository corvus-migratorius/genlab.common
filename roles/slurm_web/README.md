# Slurm-web

An Ansible role for deploying and configuring [Slurm-web](https://slurm-web.com/).

The role installs Slurm-web, configures the agent and gateway services and ensures all required services are enabled and running.

## Features

* Install Slurm-web using native package repositories or packages stored in an object storage bucket.
* Create a dedicated `slurm-web` user.
* Configure the Slurm-web agent.
* Configure the Slurm-web gateway.
* Optional Prometheus metrics endpoint.
* Deploy and manage policy configuration.
* Enable and start Slurm-web services automatically.

## Requirements

Before using this role, ensure that:

* Slurm and `slurmrestd` are already installed and configured.
* The JWT key used by `slurmrestd` is available to Slurm-web.

## Installation Methods

The role supports two installation methods.

### Native packages

Install Slurm-web from operating system repositories:

```yaml
slurm_web_install_method: native
```

### Bucket packages

Download and install packages from a storage bucket:

```yaml
slurm_web_install_method: bucket
```

## Example Playbook

```yaml
- hosts: slurm_controller
  become: true

  roles:
    - role: genlab.common.slurm_web
      vars:
        slurm_web_gateway_interface: 0.0.0.0
        slurm_web_gateway_port: 5011
        slurm_web_gateway_ui_host: "https://slurm.example.org"
```

## Services

The role manages the following services:

* `slurm-web-agent`
* `slurm-web-gateway`

Both services are enabled and started automatically.

## Default Configuration

### Agent

```yaml
slurm_web_agent_cluster: "{{ inventory_hostname }}"
slurm_web_agent_interface: localhost
slurm_web_agent_port: 5012
```

### Gateway

```yaml
slurm_web_gateway_interface: localhost
slurm_web_gateway_port: 5011
slurm_web_gateway_agents_url: "http://localhost:5012"
slurm_web_gateway_ui_host: "http://localhost:5011"
```

### Authentication

```yaml
slurm_web_gateway_auth_enabled: false
slurm_web_slurmrestd_auth: jwt
```

### Cache (Redis)

```yaml
slurm_web_cache_enabled: false
slurm_web_cache_host: localhost
slurm_web_cache_port: 6379
```

### Metrics

```yaml
slurm_web_metrics_enabled: false
```

### RacksDB

```yaml
slurm_web_racksdb_enabled: false
```

## JWT Authentication

By default, Slurm-web communicates with `slurmrestd` using JWT authentication.

```yaml
slurm_web_slurmrestd_auth: jwt
slurm_web_slurmrestd_jwt_key: /var/lib/slurm-web/slurmrestd.key
```

The JWT key must match the key configured for `slurmrestd`.

## Policy Configuration

The default policy grants anonymous users read-only access to cluster information:

```yaml
slurm_web_policy_roles:
  - name: anonymous
    actions:
      - view-stats
      - view-jobs
      - view-nodes
      - view-partitions
      - view-qos
      - view-accounts
      - associations-view
      - view-reservations
```
