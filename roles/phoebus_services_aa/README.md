# phoebus_services_aa

Builds and deploys the Archiver Appliance as four local services:

- `mgmt`
- `engine`
- `etl`
- `retrieval`

This role defaults to a single-node setup and can be switched to multi-node by overriding cluster variables.

## Install location

- Install artifacts: `/opt/epics-tools/services/{{ beamline_name }}/aa/install`
- Runtime deploy: `/opt/epics-tools/services/{{ beamline_name }}/aa/deploy`

## Systemd service created

- `{{ beamline_name }}_aa.service`

This service uses the aggregate startup script at:

- `{{ aa_deploy_location }}/{{ beamline_name }}_startup.sh`

## Aggregate startup helper

This role writes an aggregate startup script that starts all four components in order:

- `{{ aa_deploy_location }}/{{ beamline_name }}_startup.sh start`
- `{{ aa_deploy_location }}/{{ beamline_name }}_startup.sh stop`
- `{{ aa_deploy_location }}/{{ beamline_name }}_startup.sh restart`

Start order is `mgmt -> engine -> etl -> retrieval`.
Stop order is reverse: `retrieval -> etl -> engine -> mgmt`.

## Single-node install (default)

No cluster override is required. The defaults already define one appliance (`appliance0`) using `aa_node_hostname`.

Example playbook:

```yaml
- hosts: aa
  become: true
  roles:
    - role: phoebus_services_aa
```

Optional single-node overrides:

```yaml
beamline_name: tst
beamline_id: "31"
aa_node_hostname: "aa1.example.org"
aa_identity: appliance0
```

## Multi-node install

For a multi-node deployment, set:

- `aa_cluster_appliances` to the full list of nodes (same list on every host)
- `aa_identity` uniquely per host (`appliance0`, `appliance1`, ...)

Example shared vars (all hosts):

```yaml
aa_cluster_appliances:
  - identity: appliance0
    hostname: aa1.example.org
    cluster_inetport: "{{ cluster_inetport }}"
  - identity: appliance1
    hostname: aa2.example.org
    cluster_inetport: "{{ cluster_inetport }}"
  - identity: appliance2
    hostname: aa3.example.org
    cluster_inetport: "{{ cluster_inetport }}"
```

Example host-specific vars:

```yaml
# host aa1
aa_identity: appliance0

# host aa2
aa_identity: appliance1

# host aa3
aa_identity: appliance2
```

Important:

- `aa_cluster_appliances` must be identical on all nodes.
- `aa_identity` must match one `identity` entry in `aa_cluster_appliances` on that host.

## Important variables

- `beamline_name`: beamline/site name used in paths and service names
- `beamline_id`: two-digit ID used to derive ports
- `aa_identity`: node identity for this host
- `aa_node_hostname`: hostname used by default single-node `aa_cluster_appliances`
- `aa_cluster_appliances`: appliance topology definition
- `aa_mysql_server`, `aa_mysql_database`, `aa_mysql_user`, `aa_mysql_password`: database settings
- `aa_ssl_cert_file`, `aa_ssl_key_file`, `aa_ssl_chain_file`: TLS files
