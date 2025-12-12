ansible-borgmatic
=========

This is a wrapper around the `borgmatic` role from the `maxhoesel.borgbackup` collection.

The wrapper solve the most outstading issue with the current implementation of the original role: inability to install latest (or arbitrary) versions of `borgmatic` and `borg`.

In the case of Borg we are fetching a release from Github.

In the case of Borgmatic we are installing it via `pipx`, as recommended by their official documentation found here: https://torsion.org/borgmatic/docs/how-to/set-up-backups/.

Requirements
------------

- `maxhoesel.borgbackup` collection installed (see `requirements.yml`);

Role Variables
--------------

None

Dependencies
------------

None

Example Playbook
----------------

See `molecule/default/converge.yml`

License
-------

BSD

Author Information
------------------

corvus-migratorius@proton.me
