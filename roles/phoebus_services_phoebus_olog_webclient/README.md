Role Name
=========

Install and configure the Phoebus Olog webclient service.

On each startup, the run script installs project dependencies,
rebuilds using `.env.production.local`, installs `serve` under the service
account's `~/.local`, and serves the build on the configured HTTP port. Startup
stops if installation or compilation fails and may require npm registry access.

Paths
-----

- Service root: `/opt/epics-tools/services/olog_webclient`
- Project path: `/opt/epics-tools/services/olog_webclient/phoebus-olog-web-client`
- Env file: `/opt/epics-tools/services/olog_webclient/phoebus-olog-web-client/.env.production.local`
- Systemd unit: `/etc/systemd/system/phoebus_services_phoebus_olog_webclient.service`

Defaults
--------

- Version: `v2.8.0`
- Olog backend URL: `http://localhost:4181/Olog`
- HTTP port: `3000` (override with `phoebus_services_phoebus_olog_webclient_http_port`)
- procServ port: `4147`

Dependencies
------------

- `phoebus_dependencies`
- `phoebus_services_phoebus_olog`
