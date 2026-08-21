# gitlab_ce

This role installs and configures Gitlab Community Edition on Ubuntu.

## What this role does

- install dependencies for install gitlab
- install gitlab
- generate self-signed certificate
- print initial password for root (expires in 24 hours)

## Supported platforms

The role metadata currently targets:

- Ubuntu 24.04

## Variables

The role exposes the following variables in defaults/main.yml:

- gitlab_ce_version - pinned version of the gitlab-ce deb package
- gitlab_ce_fqdn - domain name for gitlab (gitlab requires it)
- gitlab_ce_ssl_dir - directory that will contain ssl-certificates
- gitlab_ce_cert_days - expires_in for ssl-certificates
- gitlab_ce_puma_workers - workers for handle http-requests
- gitlab_ce_sidekiq_concurrency - how much CPU-threads will use for handle background-tasks


## Example playbook

See: [converge.yml](molecule/default/converge.yml)

## License

MIT

## Authors

Mondrunov Elveg - jollypunk1@gmail.com