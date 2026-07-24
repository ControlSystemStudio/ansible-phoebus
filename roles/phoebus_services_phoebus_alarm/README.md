Role Name
=========

Install and configure Phoebus Alarm services.

This role includes:
- alarm server
- alarm message logger
- alarm configuration logger

Paths
-----

- Service root: /opt/epics-tools/services/phoebus_alarm
- Preferences: /opt/epics-tools/services/phoebus_alarm/phoebus_alarm_preferences.ini
- Systemd units:
  - /etc/systemd/system/phoebus_services_phoebus_alarm.service
  - /etc/systemd/system/phoebus_services_phoebus_alarm_logger.service
  - /etc/systemd/system/phoebus_services_phoebus_alarm_config_logger.service

Defaults
--------

- Alarm config name: NSLS2_OPR
- Kafka bootstrap: localhost:9092
- Elasticsearch: localhost:9200

Dependencies
------------

- phoebus_dependencies
- phoebus_tools
- phoebus_services_elasticsearch
- phoebus_services_kafka
