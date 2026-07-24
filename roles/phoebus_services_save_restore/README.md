Role Name
=========

Install and configure the Phoebus Save & Restore service.

Paths
-----

- Service root: `/opt/epics-tools/services/save_restore`
- Properties: `/opt/epics-tools/services/save_restore/save_restore.properties`
- Runtime script: `/opt/epics-tools/services/save_restore/run-save-restore.sh`
- Systemd unit: `/etc/systemd/system/phoebus_services_save_restore.service`

Defaults
--------

- Version: `4.7.4`
- HTTPS port: `23181`
- HTTP port: `23180`
- Elasticsearch host: `localhost`
- Elasticsearch port: `9200`

Dependencies
------------

- `phoebus_dependencies` role should be applied first.
- `phoebus_tools` role should be applied first so build artifacts are available.
- `phoebus_services_elasticsearch` should be running before this role starts.
