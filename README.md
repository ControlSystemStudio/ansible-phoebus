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
