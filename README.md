[![Build Status](https://travis-ci.org/nl2go/ansible-role-zookeeper.svg?branch=master)](https://travis-ci.org/nl2go/ansible-role-zookeeper)
[![Ansible Galaxy](https://img.shields.io/badge/role-nl2go.zookeeper-blue.svg)](https://galaxy.ansible.com/nl2go/zookeeper/)
[![GitHub tag (latest by date)](https://img.shields.io/github/v/tag/nl2go/ansible-role-zookeeper)](https://galaxy.ansible.com/nl2go/zookeeper)
[![Ansible Galaxy Downloads](https://img.shields.io/ansible/role/d/48974.svg?color=blue)](https://galaxy.ansible.com/nl2go/zookeeper/)

# Ansible Role: ZooKeeper

An Ansible Role that manages installation and configuration of [Apache ZooKeeper](https://zookeeper.apache.org/).

## Role Variables

Available variables listed below, along with default values (see `defaults/main.yml`):

    zookeeper_version: 3.6.1

ZooKeeper application version.

    zookeeper_dir: /opt/zookeeper

Application files directory.

    zookeeper_data_dir: /var/zookeeper

Server data directory.

    zookeeper_conf_dir: /etc/zookeeper
    
Server configuration directory.

    zookeeper_log_dir: /var/log/zookeeper

Server log directory.

    zookeeper_log_file: zookeeper.log

Log file name.
    
    zookeeper_log_level: INFO
    
Logging level.    
    
    zookeeper_log_max_file_size: 265MB
    
Max log file size before rotation.
    
    zookeeper_log_max_backup_index: 20

Max log file number to keep.

    zookeeper_client_port: 2181
    
The port clients can connect to.

    zookeeper_init_limit: 5
    zookeeper_sync_limit: 2
    zookeeper_tick_time: 2000

Consult official [ZooKeeper documentation](https://zookeeper.apache.org/doc/r3.6.1/zookeeperAdmin.html#sc_configuration) for details.    
    
    zookeeper_members: "{{ groups['all'] | map('extract', hostvars, 'ansible_default_ipv4') | map(attribute='address') | list }}"
    
ZooKeeper cluster members. Accepts hostname, FQDN or IP list.
    
    zookeeper_member_id: "{{ ansible_default_ipv4.address }}"
    
ID of the current cluster member (index of the member's hostname, FQDN or IP in the `zookeeper_members` list).
    
    zookeeper_server_username: foo
    zookeeper_server_password: foz
    
SASL based authentication for the cluster member communication. 
    
    zookeeper_clients:
      - username: bar
        password: baz
    
SASL based authentication for the clients.

    zookeeper_jmx_host: 127.0.0.1

Hostname/IP JMX will be exposed on.

    zookeeper_jmx_port: 9181

JMX remote agent port.

    zookeeper_jmx_rmi_port: 9182

RMI connector port.

    zookeeper_jmx_username: foz

JMX username.

    zookeeper_jmx_password: baz

JMX user password.

    zookeeper_jmx_role: readonly

JMX user role.    

    zookeeper_4lw_commands_whitelist: srvr,stat,mntr

Whitelisting of ZooKeeper [4lw commands](https://zookeeper.apache.org/doc/current/zookeeperAdmin.html#sc_zkCommands).

    zookeeper_global_outstanding_limit: 1000

s. [ZooKeeper Administrator's Guide].
    
    zookeeper_prealloc_size: 64M

s. [ZooKeeper Administrator's Guide].
    
    zookeeper_snap_count: 100000
    
s. [ZooKeeper Administrator's Guide].

    zookeeper_max_client_cnxns: 10

s. [ZooKeeper Administrator's Guide].

    zookeeper_min_session_timeout: "{{ 2 * zookeeper_tick_time }}"

s. [ZooKeeper Administrator's Guide].

    zookeeper_max_session_timeout: "{{ 20 * zookeeper_tick_time }}"

s. [ZooKeeper Administrator's Guide].
    
    zookeeper_autopurge_snapretain_count: 10
    
s. [Clickhouse Usage Recommendations for Zookeper].
    
    zookeeper_purge_interval: 1
    
s. [Clickhouse Usage Recommendations for Zookeper].

    zookeeper_fsync_warning_threshold_ms: 1000
    
s. [ZooKeeper Administrator's Guide].

    zookeeper_heap_size: 1024

JVM heap size in MB.

## Dependencies

- [nl2go.openjdk](https://galaxy.ansible.com/nl2go/openjdk)

## Example Playbook

    - hosts: all
      roles:
        - nl2go.zookeeper

## Development

Use [docker-molecule](https://github.com/nl2go/docker-molecule) following the instructions to run [Molecule](https://molecule.readthedocs.io/en/stable/)
or install [Molecule](https://molecule.readthedocs.io/en/stable/) locally (not recommended, version conflicts might appear).

Provide Hetzner Cloud token:

    export HCLOUD_TOKEN=123abc456efg

Use following to run tests:

    molecule test --all

## Maintainers

- [build-failure](https://github.com/build-failure)

## License

See the [LICENSE.md](LICENSE.md) file for details.

## Author Information

This role was created in 2020 by [Sendinblue GmbH](https://www.newsletter2go.com/).

[ZooKeeper Administrator's Guide]: https://zookeeper.apache.org/doc/r3.6.1/zookeeperAdmin.html
[Clickhouse Usage Recommendations for Zookeper]: https://clickhouse.tech/docs/en/operations/tips/#zookeeper
