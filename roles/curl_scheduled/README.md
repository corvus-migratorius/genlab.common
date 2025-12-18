curl_scheduled
=========

Configure curl to run on schedule by deploying a systemd service + timer. Useful for sending heartbeats.

Requirements
------------

None

Role Variables
--------------

- `args`: arguments to the curl command

- `url`: address to be accessed by curl

- `schedule`: string compatible with systemd timer `OnSchedule` option (default: `minutely`)


Dependencies
------------

None

Example Playbook
----------------

See `molecule/default/converge.yml`.

License
-------

BSD

Author Information
------------------

msayganova@genlab.llc

corvus-migratorius@proton.me
