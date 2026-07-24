Role Name
=========

Install and configure Phoebus Web Runtime services.

Paths
-----

- Tomcat root: `/opt/epics-tools/services/tomcat`
- Tools root: `/opt/epics-tools/tools`
- pvws source: `/opt/epics-tools/tools/nsls2-pvws`
- dbwr source: `/opt/epics-tools/tools/nsls2-dbwr`

Defaults
--------

- pvws version: `nsls2_deploy`
- dbwr version: `nsls2_deploy`
- EPICS CA addr list: `localhost`
- EPICS CA max array bytes: `1000000`

Dependencies
------------

- `phoebus_dependencies`
- `phoebus_services_tomcat`
