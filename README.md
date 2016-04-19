Ansible Role: Consul
=========

Install Consul on CentOS servers.

Requirements
------------

Written in Ansible 2.0.*

Role Variables
--------------

Available variables are listed below, along with default values (see `defaults/main.yml`):

## server

Install consul on server or not.

Default is `false`.

## supervisor_enabled

Install consul in supervisor or not.

Default is `true`.

## user, group

User and group for consul.

Default is `consul:consul`.

## version

Default consul version is `0.5.0`.

## url, ui_url

URL to download consul and consul ui packages.

## dir, conf_dir, data_dir, log_dir, ui_dir

Directories for consul.

```
/home/consul/consul_0.5.0
├── bin
├── consul.d
├── data
├── dist
└── logs
```

## consul config values

Please refer to http://www.consul.io/docs/agent/options.html for more information.

## rpc_services

Configure rpc services in consul.

For example, install `time_service` and bind to `8081` port (also add `tags` and `check`)

```
rpc_services:
  - {
    name: time_service,
    port: 8081,
    tags: "['rpc']",
    check: zerorpc --connect tcp://127.0.0.1:8081 --timeout 1 _zerorpc_ping,
    interval: 60s
  }
```

Dependencies
------------

+ juwai.supervisor, when supervisor_enabled

Example Playbook
----------------

    - hosts: servers
      roles:
        - { role: consul, when: server}

License
-------

MIT / BSD

Author Information
------------------

This role was created in 2015 by [Juwai Limited](http://www.juwai.com).
