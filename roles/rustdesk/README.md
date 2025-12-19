rustdesk
========

Deploy a Rustdesk server

Requirements
------------

Ports:  

- `tcp`: `21115, 21116, 21117, 21118, 21119`
- `udp`: `21116`
```

Role Variables
--------------

`rustdesk_server_version`: contains rustdesk-server version to be installed  
`rustdesk_client_version`: contains rustdesk-client version for executable to be configured

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

malyuk.ss@genlab.llc
