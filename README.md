# Aelve operations

This repository contains scripts and playbooks and whatever. [See instructions in Notion.](https://www.notion.so/aelve/Operations-0161f58f52df4278a025ec5b850b6563)

## Ansible playbooks

  * `ansible-playbook playbook/ssh_keyscan.yml` -- add hosts' fingerprints to `known_hosts`. Run this if you're getting messages like `The authenticity of host 's1.staging.guide.aelve.com (...)' can't be established`.

  * `ansible-playbook playbook/ssh.yml` -- add Aelve members' SSH keys to various machines. Rerun it during onboarding.

  * `ansible-playbook playbook/terminator.yml` -- set up a SSL terminator. Rerun it whenever a domain is added.

  * `ansible-playbook playbook/guide-staging.yml` -- deploy or update `staging.guide.aelve.com`.

  * `ansible-playbook playbook/wiki.yml` -- deploy or update `wiki.aelve.com`.

## Troubleshooting

### Ansible playbooks are stuck with `[__NSPlaceholderDate initialize] may have been in progress in another thread when fork() was called.`

Run `export OBJC_DISABLE_INITIALIZE_FORK_SAFETY=YES` before running the playbook.
