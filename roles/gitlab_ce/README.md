# gitlab_ce

This role installs and configures Gitlab Community Edition on Ubuntu.

## What this role does

- install dependencies for install gitlab
- install gitlab
- generate self-signed certificate
- schedule backups with systemd timers (application backup and upload of
  /etc/gitlab to S3-compatible object storage)
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

### SMTP

Mail is configured only when `gitlab_ce_smtp_username` and `gitlab_ce_smtp_password` are defined (they have no defaults).

- gitlab_ce_smtp_address - smtp server
- gitlab_ce_smtp_port - smtp port
- gitlab_ce_smtp_domain - smtp domain
- gitlab_ce_smtp_authentication - authentication method (default: login)
- gitlab_ce_smtp_enable_starttls_auto - use STARTTLS (default: true)
- gitlab_ce_smtp_tls - use implicit TLS (default: false)
- gitlab_ce_smtp_pool - keep smtp connections in a pool (default: false)
- gitlab_ce_smtp_openssl_verify_mode - certificate verification (default: peer)
- gitlab_ce_email_from - sender address
- gitlab_ce_email_reply_to - reply-to address
- gitlab_ce_email_display_name - sender display name (default: Gitlab)

### Backups

Two systemd timers: `gitlab-backup.timer` dumps the application, and
`gitlab-config-backup.timer` uploads an archive of /etc/gitlab to object storage.
Both units write to the journal, so there is no log file to rotate.

They run as root: `gitlab-backup` requires it, and the archive contains
gitlab-secrets.json, so nothing here can be done by an unprivileged user. The keys
are written to /root/.aws/credentials as root:root 0600 and handed to the unit with
`LoadCredential=`, so the aws process sees a 0400 copy in `$CREDENTIALS_DIRECTORY`
while /root itself stays hidden. The archive is built in the unit's own /tmp
(`PrivateTmp=yes`), invisible to the rest of the host and wiped when the unit stops.

If `gitlab_ce_aws_access_key_id` and `gitlab_ce_aws_secret_access_key` are not defined,
the role leaves the credentials file alone and the unit uses whatever is already
configured on the host.

- gitlab_ce_backup_enabled - deploy the application backup timer (default: true)
- gitlab_ce_backup_on_calendar - OnCalendar for it (default: *-*-* 03:00:00)
- gitlab_ce_config_backup_enabled - deploy the configuration backup timer
  (default: false, it needs the object storage settings below)
- gitlab_ce_config_backup_on_calendar - OnCalendar for it (default: *-*-* 03:30:00)
- gitlab_ce_config_backup_s3_endpoint - endpoint-url for the aws cli
- gitlab_ce_config_backup_s3_target - destination of the archive
- gitlab_ce_aws_region - region for the aws cli
- gitlab_ce_aws_access_key_id - access key, keep it in vault
- gitlab_ce_aws_secret_access_key - secret key, keep it in vault

Variables without a listed default are not in defaults/main.yml and must be passed
by the playbook, see [converge.yml](molecule/default/converge.yml).

## Example playbook

See: [converge.yml](molecule/default/converge.yml)

## License

MIT

## Authors

Mondrunov Elveg - jollypunk1@gmail.com