# ansible-phoebus

Ansible collection published as `org.phoebus`.

## Scope

- Core dependencies for Phoebus
- Phoebus build and tooling roles
- Phoebus middle layer service roles

## Collection name

- Fully qualified collection name: `org.phoebus`

## Current roles

- `phoebus_dependencies`: installs shared JDK and Maven dependencies under `/opt/epics-tools/lib`
- `phoebus_services_elasticsearch`: installs and configures Elasticsearch under `/opt/epics-tools/services/elasticsearch`
- `phoebus_services_mongodb`: installs and configures MongoDB under `/opt/epics-tools/services/mongodb`
- `phoebus_services_kafka`: installs and configures Kafka (KRaft mode, no Zookeeper) under `/opt/epics-tools/services/kafka`
- `phoebus_services_cf`: installs and configures the ChannelFinder service under `/opt/epics-tools/services/cf`
- `phoebus_services_save_restore`: installs and configures the Phoebus Save & Restore service under `/opt/epics-tools/services/save_restore`
- `phoebus_services_phoebus_olog`: installs and configures the Phoebus Olog service under `/opt/epics-tools/services/olog`
- `phoebus_services_phoebus_olog_webclient`: installs and configures the Phoebus Olog webclient under `/opt/epics-tools/services/olog_webclient`
- `phoebus_tools`: builds and installs core Phoebus libraries

## Filesystem layout

Single-instance-first layout used by this collection:

```text
/opt/epics-tools
├── lib
│   ├── jvm
│   └── maven
├── tools
│   └── phoebus
└── services
	├── olog
	│   ├── release
	│   ├── conf
	│   ├── data
	│   ├── logs
	│   └── run
	├── archiver
	│   ├── release
	│   ├── conf
	│   ├── data
	│   ├── logs
	│   └── run
	└── alarms
		├── release
		├── conf
		├── data
		├── logs
		└── run
```

Notes:

- Use `release` for immutable binaries.
- Use `conf`, `data`, `logs`, and `run` for mutable runtime state.
- Add a `current` symlink under each service later if versioned upgrades are needed.

## Local build

```bash
ansible-galaxy collection build
```
