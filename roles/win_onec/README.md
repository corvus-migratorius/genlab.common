win_onec
=========

Install onec on windows machines

Requirements
------------

None

Role Variables
--------------

None

Dependencies
------------

ansible.windows

Example Playbook
----------------

```yaml
roles:
  - role: genlab.common.win_onec
      win_onec_archive_src: files/windows64full_8_3_26_1540.rar
      win_onec_version: 8.3.26.1540
```

License
-------

BSD

Author Information
------------------

malyuk.ss@genlab.llc
