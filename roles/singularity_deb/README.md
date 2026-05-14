singularity
=========

Install Singularity from a DEB file hosted on the official Github repo.

Requirements
------------

Role Variables
--------------

- `singularity_deb_os_name`: Ubuntu codename, default: `jammy`
- `singularity_deb_version`: Singularity version, default: `3.9.9`

Both variables are used in building a Github release URL.

Example Playbook
----------------

See: [converge.yml](molecule/default/converge.yml)

License
-------

MIT

Author Information
------------------

corvus-migratorius@proton.me
