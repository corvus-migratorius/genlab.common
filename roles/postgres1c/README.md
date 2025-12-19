postgres1c
=========

Installs postgrespro1c (https://1c.postgres.ru/) as a system service.

Requirements
------------

Linux (tested on Ubuntu 22.04)

Role Variables
--------------

`postgres1c_major_ver`: major version of the distribution to be installed
`postgres1c_postgres_pw`: password for user 'postgres'
`postgres1c_postgres_pw_path`: path to the (Ansible-encrypted) YAML file containing a password (see `molecule/default/secrets/`)

Dependencies
------------

- community.postgresql

Example Playbook
----------------

See `molecule/default/coverge.yaml` for an example.

License
-------

BSD

Author Information
------------------

Danilkin Danila (MIPT) and Alexander Gorelyshev

Genlab, LLC

corvus-migratorius@proton.me
