ansible-mount-device
=========

Mount the given block device.

This is essentially a thin wrapper about `ansible.posix.mount` created to standardize handling mounts.

Requirements
------------

None

Role Variables
--------------

`devices`: a list of objects, describing which device should be mounted, and how (see below for an example) 

Dependencies
------------

None

Example Playbook
----------------

See: [converge.yml](molecule/default/converge.yml)

License
-------

BSD

Author Information
------------------

corvus-migratorius@proton.me
