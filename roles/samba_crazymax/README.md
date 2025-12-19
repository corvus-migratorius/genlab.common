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
secrets_wg — path for secrets_wg (see [config.yml](molecule/default/files/secrets_wg.yml))
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
