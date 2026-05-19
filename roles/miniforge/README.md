Role Name
=========

Install the Miniforge distribution for each supplied user and, optionally, deploy Mamba environment from provided YAML files.

Requirements
------------

None

Role Variables
--------------

`miniforge_release`: Miniforge release version
`miniforge_script_path`: where to download the installation script
`miniforge_release_base_url`: base URL
`miniforge_create_envs`: whethere to create environments for each user or not

`miniforge_users`: a list of dictionaries representing user accounts that need Miniforge
`manifest_dir`: path to folder on the Ansible controller host where environment files are kept
`miniforge_condarc`: a dictionary that will be YAMLified into the condarc file

NOTE: `miniforge_users` items must have `name` string attribute and, optionally, a `mamba_files` list attribute (filenames must be available under the `manifest_dir`).

Dependencies
------------

None

Example Playbook
----------------

See `molecule` > `default` > `converge.yml`

----------------

License
-------

BSD

Author Information
------------------

corvus-migratorius@proton.me
masayganova@gmail.com
