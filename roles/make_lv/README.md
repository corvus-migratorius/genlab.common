ansible-make-lv
=========

Role for creating simple lv disks with 1 group and 1 volume

Requirements
------------

None

Role Variables
--------------

None

Dependencies
------------

None

Example Playbook
----------------

All variables
```yaml
roles:
    - role: genlab.ansible_make_lv
      virtual_group: "group"
      logical_volume: "volume"
      lvm_dev: "/dev/sda"
      make_lv_size: 100%FREE
      make_lv_fs_type: ext4
      make_lv_storage_mountpoint: "/mnt"
      make_lv_storage_mountpoint_mode: "0775"
      make_lv_mountpoint_owner: root
      make_lv_mountpoint_group: root
      make_lv_is_container: false # disables udev in LVM if true
```

Minimal variables
```yaml
roles:
    - role: genlab.ansible_make_lv
      virtual_group: "group"
      logical_volume: "volume"
      lvm_dev: "/dev/sda"
```

Defaults
```yaml
make_lv_size: 100%FREE
make_lv_fs_type: ext4
make_lv_storage_mountpoint: "/mnt"
make_lv_storage_mountpoint_mode: "0775"
make_lv_mountpoint_owner: root
make_lv_mountpoint_group: root
make_lv_is_container: false # disables udev in LVM if true
```

License
-------

BSD

Author Information
------------------

malyuk.ss@genlab.llc
