# Ansible Role: ONLYOFFICE Document Server

[![Test](https://github.com/ONLYOFFICE/ansible-role-documentserver/actions/workflows/ci.yml/badge.svg)](https://github.com/ONLYOFFICE/ansible-role-documentserver/actions/workflows/ci.yml)

Installs and configures ONLYOFFICE Document Server on RHEL/CentOS or Debian/Ubuntu servers.

## Requirements

Installation requires PostgreSQL, RabbitMQ and Redis server in the system or network. Also this role requires root access, so either run it in a playbook with a global `become: yes`, or invoke the role in your playbook like:

    - hosts: documentserver
      roles:
        - role: ONLYOFFICE.documentserver
          become: yes

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    ds_server_port: ""

The port where documentserver is running, if you do not set this variable, documentserver is will be runned on port `80` by default.

    db_server_host: localhost

The IP address or the name of the host where the PostgreSQL server is running.

    db_server_name: onlyoffice

The name of a PostgreSQL database to be created on the image startup.

    db_server_user: onlyoffice

The new user name with superuser permissions for the PostgreSQL account.

    db_server_pass: onlyoffice

The password set for the PostgreSQL account.

    package_name: onlyoffice-documentserver

The package name of the ONLYOFFICE Document Server.

    redis_server_host: localhost

The IP address or the name of the host where the Redis server is running.

    redis_server_port: 6379

The Redis server port number.

    rabbitmq_server_host: localhost

The IP address or the name of the host where the RabbitMQ server is running.

    rabbitmq_server_user: guest

The new user name for the RabbitMQ account.

    rabbitmq_server_pass: guest

The password set for the RabbitMQ account.

    rabbitmq_server_vpath: /

The virtual path for the RabbitMQ server.

    proto: http

The option to add ssl configuration or not.

    jwt_enabled: false

The option to add jwt configuration or not.

    jwt_secret: secret

The secret set for jwt option.

    jwt_header: Authorization

The header set for jwt option.

    key_file: "~/certs/tls.key"

The path to the key file.

    cert_file: "~/certs/tls.crt"

The path to the certificate file.

    cluster_mode: false

The option to enable or disable cluster mode.

    start_example: false

The option for starting example service after install.

    package_url: "" 

The option for being able to install the package by URL.

## Dependencies

    None.

## Example Playbook

    - hosts: all

    vars:
        postgresql_global_config_options:
        - option: listen_addresses
            value: "*"
        - option: unix_socket_directories
            value: '{{ postgresql_unix_socket_directories | join(",") }}'

        postgresql_hba_entries:
        - type: local
            database: all
            user: postgres
            auth_method: peer
        - type: local
            database: all
            user: all
            auth_method: peer 
        - type: host
            database: all
            user: all
            address: 127.0.0.1/32
            auth_method: md5
        - type: host
            database: all
            user: all
            address: ::1/128
            auth_method: md5
        - type: host
            database: all
            user: all
            address: 0.0.0.0/0
            auth_method: md5

        postgresql_databases:
        - name: "{{ db_server_name }}"

        postgresql_users:
        - name: "{{ db_server_user }}"
            password: "{{ db_server_pass }}"

        rabbitmq_users:
        - name: "{{ rabbitmq_server_user }}"
            password: "{{ rabbitmq_server_pass }}"
            vhost: "{{ rabbitmq_server_vpath }}"
            configure_priv: .*
            read_priv: .*
            write_priv: .*
            tags: administrator

        rabbitmq_users_remove: []

        redis_bind_interface: 0.0.0.0

    roles:
        - geerlingguy.postgresql
        - ONLYOFFICE.rabbitmq
        - geerlingguy.redis
        - ONLYOFFICE.documentserver

## License

GNU AGPL v3.0

## Author Information

This role was created by [ONLYOFFICE](https://www.onlyoffice.com/).
