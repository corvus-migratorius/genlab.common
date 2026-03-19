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
      size: 100%FREE
      fs_type: ext4
      storage_mountpoint: "/mnt"
      storage_mountpoint_mode: "0775"
      mountpoint_owner: root
      mountpoint_group: root
      is_container: false # disables udev in LVM if true
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
size: 100%FREE
fs_type: ext4
storage_mountpoint: "/mnt"
storage_mountpoint_mode: "0775"
mountpoint_owner: root
mountpoint_group: root
is_container: false # disables udev in LVM if true
```

License
-------

BSD

Author Information
------------------

malyuk.ss@genlab.llc
