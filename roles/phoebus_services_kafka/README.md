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

Cluster vars
------------

- `phoebus_services_kafka_cluster_id`: pre-generated KRaft cluster id shared by all nodes.
- `phoebus_services_kafka_controller_quorum_voters`: controller voters list, for example `1@10.0.1.11:9093,2@10.0.1.12:9093,3@10.0.1.13:9093`.
- `phoebus_services_kafka_node_id`: unique per node.

Note: the voters list must include an entry for `phoebus_services_kafka_node_id`.

Dependencies
------------

- phoebus_dependencies role should be applied first.
