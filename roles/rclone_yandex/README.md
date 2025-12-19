rclone_yandex
=============

Mount a Yandex Disk share via `rclone`. 

Requirements
------------

None

Role Variables
--------------

`rclone_config_path`: where to keep the configuration file (default: `/root/rclone.conf`)
`rclone_mountpoint`: where to mount the Yandex Disk share
`rclone_group`: how to name the group that will own the mountpoint

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
