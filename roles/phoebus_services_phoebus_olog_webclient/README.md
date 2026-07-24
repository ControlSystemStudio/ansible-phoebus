Role Name
=========

Install and configure the Phoebus Olog webclient service.

Paths
-----

- Service root: `/opt/epics-tools/services/olog_webclient`
- Project path: `/opt/epics-tools/services/olog_webclient/phoebus-olog-web-client`
- Env file: `/opt/epics-tools/services/olog_webclient/phoebus-olog-web-client/.env`
- Systemd unit: `/etc/systemd/system/phoebus_services_phoebus_olog_webclient.service`

Defaults
--------

- Version: `v2.2.1`
- Olog backend URL: `http://localhost:4181/Olog`
- procServ port: `4147`

Dependencies
------------

- `phoebus_dependencies`
- `phoebus_services_phoebus_olog`
