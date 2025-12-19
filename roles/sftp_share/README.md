sftp_share
=========

Creates a user account and directories for a secured SFTP data exchange (one user = one share).

The role creates a dedicated SSH config under `/etc/ssh/sshd_config.d/`, configuring:

- chroot into the directory of the share
- limits commands to `internal-sftp`
- further controls SFTP permissions for the share

Disk quota management is not included.

Requirements
------------

None

Role Variables
--------------

`sftp_username` — user account name on the sFTP server  
`sftp_pubkey` — the public part of the SSH key the user will be using to connect to the server
`sftp_root` — directory to put the SFTP shares under
`sftp_transfers_groupname` — group owning `{{sftp_root}}/{{sftp_username}}-uploads/transfers`
`sftp_permissions` — list of permissions, see below for supported (default: `open,close,read,write,lstat,fstat,opendir,readdir,remove,mkdir,rmdir,realpath,rename`)

List Of SFTP Operations
------------------------
`open` — open a file for reading or writing  
`close` — close an opened file  
`read` — read data from a file  
`write` — write data to a file  
`lstat` — get file attributes without following symlinks  
`fstat` — get attributes of an opened file  
`setstat` — change file attributes (chmod, chown, etc.)  
`fsetstat` — change attributes of an opened file  
`opendir` — open a directory for reading  
`readdir` — read the contents of a directory  
`remove` — delete a file  
`mkdir` — create a new directory  
`rmdir` — remove an empty directory  
`realpath` — resolve absolute path of a file or directory (inside chroot)  
`stat` — get file attributes (follows symlinks)  
`rename` — rename a file or directory  
`readlink` — read the target of a symbolic link  
`symlink` — create a symbolic link  

For example: 

- Default: `open,close,read,write,lstat,fstat,opendir,readdir,remove,mkdir,rmdir,realpath,rename`  
- Read only: `open,close,read,lstat,fstat,opendir,readdir,realpath,stat`  
- Required to establish an SFTP connection: `realpath`

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
