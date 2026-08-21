# gitlab_runner

This role installs and configures GitLab Runner on Ubuntu.

## What this role does

- install dependencies for install gitlab-runner
- install gitlab-runner
- render config.toml with a docker executor
- enable and start the gitlab-runner service

## Supported platforms

The role metadata currently targets:

- Ubuntu 24.04

## Variables

The role exposes the following variables in defaults/main.yml:

- gitlab_runner_version - pinned version of the gitlab-runner deb package
- gitlab_runner_url - url of the gitlab instance (runner requires it)
- gitlab_runner_token - runner authentication token (glrt-...)
- gitlab_runner_name - runner name shown in gitlab
- gitlab_runner_certs_dir - directory that will contain ca-certificate for self-signed gitlab
- gitlab_runner_ca_fetch - pull the tls-certificate from gitlab and trust it (needed for self-signed gitlab)
- gitlab_runner_executor - executor type
- gitlab_runner_concurrent - how much jobs runner handles in parallel
- gitlab_runner_docker_image - default image for the docker executor
- gitlab_runner_docker_volumes - volumes mounted into job containers

## Example playbook

See: [converge.yml](molecule/default/converge.yml)

## License

MIT

## Authors

Mondrunov Elveg - jollypunk1@gmail.com
