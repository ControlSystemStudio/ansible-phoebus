Role Name
=========

Install and configure a MongoDB service for Phoebus.

Paths
-----

- Service root: `/opt/epics-tools/services/mongodb`
- Config file: `/etc/phoebus_services_mongodb.conf`
- Data: `/opt/epics-tools/services/mongodb/data`
- Logs: `/opt/epics-tools/services/mongodb/logs/mongod.log`
- Run: `/opt/epics-tools/services/mongodb/run`

Defaults
--------

- Package: `mongodb-org`
- Repository stream: `8.3`
- Service name: `phoebus_services_mongodb`
- Port: `27017`
- Bind address: `127.0.0.1`
- Replica set: disabled by default

Dependencies
------------

- `phoebus_dependencies` role should be applied first.
