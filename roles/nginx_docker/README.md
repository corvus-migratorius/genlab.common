ansible-nginx-docker
=========

Deploy NGINX as a Docker container

Requirements
------------

Docker

Role Variables
--------------

None

Dependencies
------------

Soft dependency on `genlab.docker_ubuntu` (any means of installing Docker on the managed machine should be fine).

Example Playbook
----------------

```yaml
roles:
    - role: genlab.nginx_docker
```

License
-------

BSD

Author Information
------------------

corvus-migratorius@proton.me
