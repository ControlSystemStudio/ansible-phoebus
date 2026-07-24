Role Name
=========

Install and configure the Phoebus Olog service.

Paths
-----

- Service root: `/opt/epics-tools/services/olog`
- Properties: `/opt/epics-tools/services/olog/olog.properties`
- Runtime script: `/opt/epics-tools/services/olog/run-phoebus-olog.sh`
- Systemd unit: `/etc/systemd/system/phoebus_services_phoebus_olog.service`

Defaults
--------

- Version: `v5.0.4`
- HTTPS port: `4181`
- HTTP port: `4180`
- Elasticsearch host: `localhost`
- Elasticsearch port: `9200`
- MongoDB host: `localhost`
- MongoDB port: `27017`

Dependencies
------------

- `phoebus_dependencies`
- `phoebus_tools`
- `phoebus_services_elasticsearch`
- `phoebus_services_mongodb`
