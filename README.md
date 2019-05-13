# Aelve operations

This repository contains scripts and playbooks and whatever. [See instructions in Notion.](https://www.notion.so/aelve/Operations-0161f58f52df4278a025ec5b850b6563)

## Ansible playbooks

  * `ansible-playbook playbook/ssh_keyscan.yml` -- add hosts' fingerprints to `known_hosts`. Run this if you're getting messages like `The authenticity of host 's1.staging.guide.aelve.com (...)' can't be established`.

  * `ansible-playbook playbook/ssh.yml` -- add Aelve members' SSH keys to various machines. Rerun it during onboarding.

  * `ansible-playbook playbook/terminator.yml` -- set up a SSL terminator. Rerun it whenever a domain is added.
