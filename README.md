[![Build Status](https://travis-ci.com/nl2go/ansible-role-clickhouse.svg?branch=master)](https://travis-ci.com/nl2go/ansible-role-clickhouse)
[![GitHub tag (latest by date)](https://img.shields.io/github/v/tag/nl2go/ansible-role-clickhouse)](https://galaxy.ansible.com/nl2go/clickhouse)
[![Ansible Galaxy](https://img.shields.io/badge/role-nl2go.clickhouse-blue.svg)](https://galaxy.ansible.com/nl2go/clickhouse/)
[![Ansible Galaxy Quality Score](https://img.shields.io/ansible/quality/49634)](https://galaxy.ansible.com/nl2go/clickhouse/)
[![Ansible Galaxy Downloads](https://img.shields.io/ansible/role/d/49634.svg?color=blue)](https://galaxy.ansible.com/nl2go/clickhouse/)

# Ansible Role: ClickHouse

An Ansible Role that manages installation and configuration of [ClickHouse](https://clickhouse.tech/).

## Role Variables

Available variables listed below, along with default values (see `defaults/main.yml`):

    clickhouse_conf_dir: /etc/clickhouse-server

Server configuration directory.

    clickhouse_loglevel: information

Server log level.

    clickhouse_profiles: 
      default:
        max_memory_usage: 10000000000
        use_uncompressed_cache: 0
        load_balancing: "random"

A settings profile is a collection of [settings](https://clickhouse.tech/docs/en/operations/settings/settings-profiles/) grouped under the same name.

    clickhouse_profiles: 
      default:
        password: "qwerty" # or `password_sha256_hex` to assign a password using its SHA256 hash
        profile: "default"
        quota: "default"

The `users` section of the `user.xml` configuration file contains user  [settings](https://clickhouse.tech/docs/en/operations/settings/settings-users/).

    clickhouse_profiles: 
      default:
        intervals:
          - duration: 3600
            queries: 0
            errors: 0
            result_rows: 0
            read_rows: 0
            execution_time: 0

Quota [settings](https://clickhouse.tech/docs/en/operations/settings/settings-profiles/) is for limiting resource usage over a period of time or track the use of resources.

## Dependencies

None.

## Example Playbook

    - hosts: all
      roles:
        - nl2go.clickhouse

## Development

Use [docker-molecule](https://github.com/nl2go/docker-molecule) following the instructions to run [Molecule](https://molecule.readthedocs.io/en/stable/)
or install [Molecule](https://molecule.readthedocs.io/en/stable/) locally (not recommended, version conflicts might appear).

Provide Hetzner Cloud token:

    export HCLOUD_TOKEN=123abc456efg

Use following to run tests:

    molecule test --all

## Maintainers

- [pablo2go](https://github.com/pablo2go)
- [dirkaholic](https://github.com/dirkaholic)

## License

See the [LICENSE.md](LICENSE.md) file for details.

## Author Information

This role was created in 2020 by [Sendinblue GmbH](https://www.newsletter2go.com/).
