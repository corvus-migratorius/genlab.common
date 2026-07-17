platform1c
=========

Role for deploying 1c server

Requirements
------------

None

Role Variables
--------------

platform1c_version — 1c version
platform1c_config — 1c config (see [test.yaml](molecule/default/files/test.yaml))
platform1c_admin_pw_path — 1c admin credentials (see [platform1c.yaml](secrets/platform1c.yaml))
platform1c_oneget_pw_path — oneget credentials (see [oneget.yaml](secrets/oneget.yaml))
platform1c_platformfile — 1c server archive (e.g. server64_with_all_clients_8_3_26_1540.zip)
platform1c_download_method — download method. `'manual'` or `'oneget'`

Dependencies
------------

None

Example Playbook
----------------

```yaml
roles:
- role: genlab.common.platform1c
    platform1c_version: "8.3.26.1540"                                            # required
    platform1c_config: "{{ role_path }}/molecule/default/files/test.yaml"        # required
    platform1c_admin_pw_path: "secrets/platform1c.yaml"                          # required
    platform1c_oneget_pw_path: "secrets/oneget.yaml"                             # required if using oneget
    platform1c_platformfile: "{{ role_path }}/molecule/default/files/server64_with_all_clients_8_3_26_1540.zip"  # if platfrom1c_download_methond == manual
    platform1c_download_method: 'manual' # required. manual or oneget
```

License
-------

BSD

Author Information
------------------

Danilkin Danila
