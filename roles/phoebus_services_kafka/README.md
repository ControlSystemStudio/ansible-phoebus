Role Name
=========

Install and configure Kafka (KRaft mode, no Zookeeper) for Phoebus.

Paths
-----

- Service root: /opt/epics-tools/services/kafka
- Release: /opt/epics-tools/services/kafka/release
- Config: /opt/epics-tools/services/kafka/conf
- Data: /opt/epics-tools/services/kafka/data
- Logs: /opt/epics-tools/services/kafka/logs

Defaults
--------

- Kafka version: 4.3.1 (Scala 2.13)
- Kafka port: 9092
- Controller port: 9093
- Kafka service: phoebus_services_kafka
- Java home: /opt/epics-tools/lib/jvm/jdk-21

Behavior
--------

- Uses KRaft mode (no Zookeeper dependency).
- Automatically formats Kafka storage with `kafka-storage.sh` when first installed.
- Requires `phoebus_services_kafka_cluster_id` from inventory.
- `phoebus_services_kafka_controller_quorum_voters` defaults to `1@localhost:9093` for single-node use.

Generate a cluster ID (run once, share the result across all nodes):

```bash
kafka-storage.sh random-uuid
```

Single-node example
-------------------

inventory `host_vars/kafka1.yml`:

```yaml
phoebus_services_kafka_cluster_id: "your-generated-uuid"
phoebus_services_kafka_node_id: 1
phoebus_services_kafka_controller_quorum_voters:
  - "1@kafka1.example.org:9093"
```

3-node cluster example
----------------------

All three nodes share the same `cluster_id` and the same `controller_quorum_voters` list.
Each node gets a unique `node_id`.

inventory `group_vars/kafka.yml` (shared by all nodes):

```yaml
phoebus_services_kafka_cluster_id: "your-generated-uuid"
phoebus_services_kafka_controller_quorum_voters:
  - "1@kafka1.example.org:9093"
  - "2@kafka2.example.org:9093"
  - "3@kafka3.example.org:9093"
```

inventory `host_vars/kafka1.yml`:

```yaml
phoebus_services_kafka_node_id: 1
```

inventory `host_vars/kafka2.yml`:

```yaml
phoebus_services_kafka_node_id: 2
```

inventory `host_vars/kafka3.yml`:

```yaml
phoebus_services_kafka_node_id: 3
```

See `playbooks/kafka_cluster.yml` for the matching playbook.

Dependencies
------------

- phoebus_dependencies role should be applied first.
