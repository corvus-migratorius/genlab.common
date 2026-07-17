samba_crazymax
=========

Deploys a crazymax/samba docker container

Requirements
------------

- docker
- community.docker collection installed

Role Variables
--------------

samba_crazymax_compose_path — samba crazymax docker compose path
samba_crazymax_server_string — server string
config — path for config (see [config.yml](molecule/default/files/config.yml))
secrets — path for secrets (see [config.yml](molecule/default/files/secrets.yml))
samba_crazymax_subnet — subnet which is allowed to be connected
path_storage — storage path

Dependencies
------------

- genlab.common.docker_ubuntu — for docker installation

Example Playbook
----------------

see [converge.yml](molecule/default/converge.yml)

License
-------

BSD

Author Information
------------------

Alexander Gorelyshev corvus-migratorius@proton.me
