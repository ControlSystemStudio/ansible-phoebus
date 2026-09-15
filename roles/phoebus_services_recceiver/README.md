# phoebus_services_recceiver

Install and run the ChannelFinder Recceiver service from https://github.com/ChannelFinder/recceiver.

## Files

- Service root: `/opt/epics-tools/services/recceiver`
- Jar: `/opt/epics-tools/services/recceiver/recceiver.jar`
- Config: `/opt/epics-tools/services/recceiver/application.properties`
- Systemd unit: `/etc/systemd/system/phoebus_services_recceiver.service`

## Defaults

- Java: `/opt/epics-tools/lib/jvm/jdk-21`
- Maven: `/opt/epics-tools/lib/apache-maven-3.9.9`
- TCP bind: `0.0.0.0`
- TCP port: `5064`
- UDP broadcast port: `5049`
- ChannelFinder service URL: `http://localhost:9090/ChannelFinder`

## Dependencies

- `phoebus_dependencies`
