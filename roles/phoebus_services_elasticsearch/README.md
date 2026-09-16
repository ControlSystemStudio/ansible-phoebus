Role Name
=========

Install and configure a single-node Elasticsearch service for Phoebus.

Paths
-----

- Service root: `/opt/epics-tools/services/elasticsearch`
- Release: `/opt/epics-tools/services/elasticsearch/release`
- Config: `/opt/epics-tools/services/elasticsearch/release/config`
- Data: `/opt/epics-tools/services/elasticsearch/data`
- Logs: `/opt/epics-tools/services/elasticsearch/logs`
- Run: `/opt/epics-tools/services/elasticsearch/run`

Defaults
--------

- Elasticsearch version: `8.2.3`
- HTTP port: `9200`
- Transport port: `9300`
- Service name: `phoebus_services_elasticsearch`
- Java home: `/opt/epics-tools/lib/jvm/jdk-21`
- Security default: `xpack.security.enabled: false`
- TLS defaults: `xpack.security.http.ssl.enabled: false` and `xpack.security.transport.ssl.enabled: false`
- Out-of-the-box mode is single-node (`discovery.type: single-node`) and binds to `127.0.0.1`.

Multi-node model (many hosts)
-----------------------------

Use one role on every Elasticsearch host and drive cluster settings from inventory.

- Set per-host values in host vars: `phoebus_services_elasticsearch_node_name`, `phoebus_services_elasticsearch_network_host`.
- Set shared values in group vars: `phoebus_services_elasticsearch_cluster_name`, `phoebus_services_elasticsearch_seed_hosts`, `phoebus_services_elasticsearch_initial_master_nodes`.
- Override `phoebus_services_elasticsearch_network_host` from `127.0.0.1` to a reachable interface/IP for multi-host clustering.
- Set `phoebus_services_elasticsearch_discovery_type` to an empty string (`""`) for clustered mode, then define `seed_hosts` and `initial_master_nodes`.
- Treat `phoebus_services_elasticsearch_initial_master_nodes` as a bootstrap-only setting for first cluster formation. After the cluster forms, remove it or set it to an empty list on all nodes.
- The role writes `elasticsearch.yml` into `release/config`, so first-start auto-generated security settings in that file are intentionally replaced by the managed template on the next run.

Example group vars:

```yaml
phoebus_services_elasticsearch_cluster_name: phoebus-es
phoebus_services_elasticsearch_seed_hosts:
  - 10.0.1.11:9300
  - 10.0.1.12:9300
  - 10.0.1.13:9300
phoebus_services_elasticsearch_initial_master_nodes:
  - es1
  - es2
  - es3
```

Dependencies
------------

- `phoebus_dependencies` role should be applied first.

Behavior
--------

- The role enables and starts `phoebus_services_elasticsearch`.
- The role manages only `release/config/elasticsearch.yml` and uses the archive's stock `jvm.options` and `log4j2.properties`.
- The service is restarted only when release/config/systemd unit content changes.
