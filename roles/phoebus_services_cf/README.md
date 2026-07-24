Role Name
=========

Install and configure the ChannelFinder service.

Paths
-----

- Service root: `/opt/epics-tools/services/cf`
- Properties: `/opt/epics-tools/services/cf/cf.properties`
- Runtime script: `/opt/epics-tools/services/cf/run-cf.sh`
- Systemd unit: `/etc/systemd/system/phoebus_services_cf.service`

Defaults
--------

- Version: `ChannelFinder-4.7.3`
- HTTPS port: `1181`
- HTTP port: `1180`
- Elasticsearch host: `localhost`
- Elasticsearch port: `9200`

Dependencies
------------

- `phoebus_dependencies`
- `phoebus_tools`
- `phoebus_services_elasticsearch`
