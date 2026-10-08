# Enterprise Linux Fleet Automation Platform

Production-style Ansible reference architecture for managing up to 30 heterogeneous Linux servers across RHEL and Ubuntu, covering web, application, database, infrastructure, monitoring and backup tiers.

> Portfolio note: this repository documents and automates an enterprise-scale lab/reference architecture. The 30-node inventory uses reserved/private lab addresses and does not represent a live production estate.

## Architecture

Ansible Control Node -> SSH + sudo -> 30 managed Linux servers

WEB (6) | APP (10) | DB (6) | INFRA (4) | MONITORING (2) | BACKUP (2)

The estate is split evenly: 15 Ubuntu and 15 RHEL.

## Engineering coverage

- Static inventory with tier and OS groups.
- Common baseline and OS-specific package handling.
- SSH hardening, firewall policy and security banners.
- Application, web and database roles with handlers and templates.
- Rolling patch orchestration with serial, failure thresholds and maintenance tags.
- Fact-driven conditional logic for RHEL vs Ubuntu.
- Check mode, syntax validation and a verification playbook.
- Ansible Vault pattern for credentials; no credentials are committed.
- CI workflow for syntax checks and Ansible linting.
- Operations and security-control documentation for interview discussion.

## Quick start

cd projects/enterprise-ansible-platform
python3 -m pip install --user ansible ansible-lint
ansible-galaxy collection install -r requirements.yml
ansible-inventory -i inventory/hosts.ini --graph
ansible-playbook -i inventory/hosts.ini playbooks/site.yml --syntax-check
ansible-playbook -i inventory/hosts.ini playbooks/site.yml --check --diff -k -K

## Security boundary

The inventory uses fictional RFC1918 data under 10.30.0.0/24. Replace host addresses and secrets for real use. Do not commit SSH passwords, private keys, API tokens or database credentials.

For production, extend this pattern with MFA/PAM, centralized secrets management, central logging, vulnerability scanning, formal change-ticket integration, signed approvals, backup immutability and HA database design.
