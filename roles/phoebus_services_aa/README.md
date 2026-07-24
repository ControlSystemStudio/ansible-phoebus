# phoebus_services_aa

Builds and deploys the Archiver Appliance as four local services:

- `mgmt`
- `engine`
- `etl`
- `retrieval`

This role defaults to a single-node setup and can be switched to multi-node by overriding cluster variables.

SSL/TLS is disabled by default (`aa_enable_ssl: false`).

## Filesystem layout

- Root: `{{ aa_root }}`
- Release: `{{ aa_release_dir }}`
- Config: `{{ aa_conf_dir }}`
- Data: `{{ aa_data_dir }}`
- Logs: `{{ aa_logs_dir }}`
- Run: `{{ aa_run_dir }}`

Internal role paths:

- Install artifacts: `{{ aa_install_location }}`
- Runtime deploy: `{{ aa_deploy_location }}`

## Systemd service created

- `{{ aa_service_name }}.service`

This service uses the aggregate startup script at:

- `{{ aa_deploy_location }}/{{ aa_script_prefix }}_startup.sh`

## Aggregate startup helper

This role writes an aggregate startup script that starts all four components in order:

- `{{ aa_deploy_location }}/{{ aa_script_prefix }}_startup.sh start`
- `{{ aa_deploy_location }}/{{ aa_script_prefix }}_startup.sh stop`
- `{{ aa_deploy_location }}/{{ aa_script_prefix }}_startup.sh restart`

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
aa_node_hostname: "aa1.example.org"
aa_identity: appliance0
aa_enable_ssl: false
```

Default ports:

```yaml
cluster_inetport: 17670
mgmt_port: 17665
engine_port: 17666
etl_port: 17667
data_retrieval_port: 17668
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

- `aa_root`: archiver service root path
- `aa_release_dir`, `aa_conf_dir`, `aa_data_dir`, `aa_logs_dir`, `aa_run_dir`: service layout directories
- `aa_service_name`: systemd unit base name (without `.service`)
- `aa_script_prefix`: startup script name prefix
- `aa_identity`: node identity for this host
- `aa_node_hostname`: hostname used by default single-node `aa_cluster_appliances`
- `cluster_inetport`, `mgmt_port`, `engine_port`, `etl_port`, `data_retrieval_port`: archiver network ports
- `aa_enable_ssl`: enables TLS URL generation and SSL certificate setup when `true`
- `aa_cluster_appliances`: appliance topology definition
- `aa_mysql_server`, `aa_mysql_database`, `aa_mysql_user`, `aa_mysql_password`: database settings
- `aa_ssl_cert_file`, `aa_ssl_key_file`, `aa_ssl_chain_file`: TLS files
