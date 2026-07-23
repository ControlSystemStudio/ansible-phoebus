Role Name
=========

Install and configure a single-node Elasticsearch service for Phoebus.

Paths
-----

- Service root: `/opt/epics-tools/services/elasticsearch`
- Release: `/opt/epics-tools/services/elasticsearch/release`
- Config: `/opt/epics-tools/services/elasticsearch/conf`
- Data: `/opt/epics-tools/services/elasticsearch/data`
- Logs: `/opt/epics-tools/services/elasticsearch/logs`
- Run: `/opt/epics-tools/services/elasticsearch/run`

Defaults
--------

- Elasticsearch version: `8.2.3`
- HTTP port: `9200`
- Service name: `phoebus_services_elasticsearch`
- Java home: `/opt/epics-tools/lib/jvm/jdk-21`

Dependencies
------------

- `phoebus_dependencies` role should be applied first.

Behavior
--------

- The role enables and starts `phoebus_services_elasticsearch`.
- The service is restarted only when release/config/systemd unit content changes.
