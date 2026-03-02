The role uses asynchronous Prometheus exporter for wireguard (https://github.com/kbknapp/wireguard_exporter).


**Metrics Provided**

- *wireguard_bytes_total*: Total number of bytes per direction per interface
- *wireguard_duration_since_latest_handshake*: Duration in milliseconds since latest handshake for a peer
- *wireguard_interfaces_total*: Total number of interfaces
- *wireguard_peer_bytes_total*: Total number of bytes per direction for a peer
- *wireguard_peer_endpoint*: Peers info. static value
- *wireguard_peers_total*: Total number of peers per interfaces
- *wireguard_scrape_duration_milliseconds*: Duration in milliseconds of the scrape
- *wireguard_scrape_success*: If the scrape was a success


**Variables**

- *wg_exporter_version*: version of exporter
- *wg_exporter_alias*: Add an alias for a given public key in the form of 'pubkey:alias' (separate multiple with commas)
- *wg_exporter_collect_interval_sec*: How often metrics are gathered
- *wg_exporter_listen_port*: The listen port for scraping metrics
- *wg_exporter_listen_address*:  The listen address scraping metrics
- *wg_exporter_quiet*: Supress output at a level or lower. -q: INFO, -qq: WARN, -qqq: ERROR (i.e everything)
- *wg_exporter_verbose*: Show verbose output at a level or higher. -v:  DEBUG, -vv: TRACE

**Example playbook**

```yaml
---
- name: test_playbook
  hosts: all

  roles:
    - role: genlab.common.wg_exporter
```