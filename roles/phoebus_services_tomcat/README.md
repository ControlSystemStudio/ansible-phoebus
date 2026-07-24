Role Name
=========

Install and configure a Tomcat service.

Paths
-----

- Service root: `/opt/epics-tools/services/tomcat`
- Systemd unit: `/etc/systemd/system/tomcat.service`

Defaults
--------

- Tomcat version: `9.0.104`
- HTTP port: `7070`
- HTTPS redirect port: `8443`
- AJP port: `8009`
- Bind address: `localhost`

Dependencies
------------

- `phoebus_dependencies`
