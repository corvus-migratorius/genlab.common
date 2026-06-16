Slurm
=====

Install and configure a Slurm cluster on RHEL/CentOS or Debian/Ubuntu servers

Role Variables
--------------

All variables are optional. If nothing is set, the role will install the Slurm client programs, munge, and
create a `slurm.conf` with a single `localhost` node and `debug` partition.
See the [defaults](defaults/main.yml) and [example playbooks](#example-playbooks) for examples.

For the various roles a slurm node can play, you can either set group names, or add values to a list, `slurm_roles`.

- `slurm_roles: ['controller']`
- `slurm_roles: ['exec']`
- `slurm_roles: ['dbd']`
- `slurm_roles: ['restd']`

General config options for slurm.conf go in `slurm_config`, a hash. Keys are Slurm config option names.

Partitions and nodes go in `slurm_partitions` and `slurm_nodes`, lists of hashes. The only required key in the hash is `name`, which becomes the `PartitionName` or `NodeName` for that line. All other keys/values are placed on to the line of that partition or node.

Options for the additional configuration files [acct_gather.conf](https://slurm.schedmd.com/acct_gather.conf.html),
[cgroup.conf](https://slurm.schedmd.com/cgroup.conf.html) and [gres.conf](https://slurm.schedmd.com/gres.conf.html)
may be specified in the `slurm_acct_gather_config`, `slurm_cgroup_config` (both of them hashes) and
`slurm_gres_config` (list of hashes) respectively.

The role installs Slurm from source code distributed by SchedMD. Set
`slurm_version` to the version you want to deploy.

The role will:

1. Download the corresponding source archive from SchedMD.
2. Install the required build dependencies for the target operating system.
3. Configure Slurm with the selected role-specific features.
4. Build and install Slurm from source.

You can use `slurm_create_user` (a bool) to pre-create a Slurm user. You can specify `slurm_user_name`, `slurm_group_name`, `slurm_user_gid`, `slurm_user_uid`. If `slurm_roles: ['restd']` is set, than role create `slurmrestd` user. You can specify its gid and uid. 

Note that this role requires root access, so enable ``become`` either globally in your playbook / on the commandline or just for the role like [shown below](#example-playbooks).

Requirements
------------
When the `dbd` role is enabled, the role installs and configures slurmdbd, but it does not install or manage a MariaDB/MySQL server.
A running MySQL-compatible database must be available before starting slurmdbd. You can provision the database manually or by using a dedicated database role such as https://galaxy.ansible.com/ui/standalone/roles/geerlingguy/mysql/

Example Playbooks
-----------------

Minimal setup, all services on one node:

```yaml
- name: Slurm all in One
  hosts: all
  vars:
    slurm_roles: ['controller', 'exec', 'dbd']
  roles:
    - role: genlab.common.slurm
      become: True
```

More extensive example:

```yaml
- name: Slurm execution hosts
  hosts: all
  roles:
    - role: galaxyproject.slurm
      become: True
  vars:
    slurm_cgroup_config:
      CgroupMountpoint: "/sys/fs/cgroup"
      CgroupAutomount: yes
      ConstrainCores: yes
      TaskAffinity: no
      ConstrainRAMSpace: yes
      ConstrainSwapSpace: no
      ConstrainDevices: no
      AllowedRamSpace: 100
      AllowedSwapSpace: 0
      MaxRAMPercent: 100
      MaxSwapPercent: 100
      MinRAMSpace: 30
    slurm_config:
      AccountingStorageType: "accounting_storage/none"
      ClusterName: cluster
      GresTypes: gpu
      JobAcctGatherType: "jobacct_gather/none"
      MpiDefault: none
      ProctrackType: "proctrack/cgroup"
      ReturnToService: 1
      SchedulerType: "sched/backfill"
      SelectType: "select/cons_res"
      SelectTypeParameters: "CR_Core"
      SlurmctldHost: "slurmctl"
      SlurmctldLogFile: "/var/log/slurm/slurmctld.log"
      SlurmctldPidFile: "/var/run/slurmctld.pid"
      SlurmdLogFile: "/var/log/slurm/slurmd.log"
      SlurmdPidFile: "/var/run/slurmd.pid"
      SlurmdSpoolDir: "/var/spool/slurmd"
      StateSaveLocation: "/var/spool/slurmctld"
      SwitchType: "switch/none"
      TaskPlugin: "task/affinity,task/cgroup"
      TaskPluginParam: Sched
    slurm_create_user: yes
    slurm_gres_config:
      - File: /dev/nvidia[0-3]
        Name: gpu
        NodeName: gpu[01-10]
        Type: tesla
    slurm_munge_key: "../../../munge.key"
    slurm_nodes:
      - name: "gpu[01-10]"
        CoresPerSocket: 18
        Gres: "gpu:tesla:4"
        Sockets: 2
        ThreadsPerCore: 2
    slurm_partitions:
      - name: gpu
        Default: YES
        MaxTime: UNLIMITED
        Nodes: "gpu[01-10]"
    slurm_roles: ['exec']
    slurm_user:
      comment: "Slurm Workload Manager"
      gid: 888
      group: slurm
      home: "/var/lib/slurm"
      name: slurm
      shell: "/usr/sbin/nologin"
      uid: 888
```

License
-------

MIT

Author Information
------------------

- [Nate Coraor](https://github.com/natefoo)
- [Helena Rasche](https://github.com/erasche)

[View contributors on GitHub](https://github.com/galaxyproject/ansible-slurm/graphs/contributors)
