# Enterprise Linux User, Group & Access Management Automation with Ansible

An idempotent Ansible lab for local Linux account provisioning, group membership, login-shell configuration, home-directory placement, permissions and post-change verification.

> **Scope and safety:** the default inventory targets localhost only. This is a portfolio/lab implementation, not a claim that the playbooks have been validated against a live enterprise fleet. Review UID/GID assignments and inventory before using them on managed systems.

## Objectives

- Create Unix groups with stable lab GIDs.
- Provision seven sample accounts from one data file.
- Control shell and home-directory settings.
- Reconcile supplementary group membership as an explicit desired state.
- Verify users, groups, shells, home paths, ownership, permissions and membership.
- Keep changes repeatable and reviewable with check mode.
- Keep passwords and credentials out of source control.

## Repository layout

- inventory.ini — safe localhost-by-default inventory.
- ansible.cfg — project-scoped Ansible defaults.
- vars/users.yml — central user and group definitions.
- create-groups.yml — create managed groups.
- create-users.yml — provision accounts after groups exist.
- modify-groups.yml — apply declared supplementary-group membership.
- modify-shells.yml — update shells after validating users and shell paths.
- modify-home-dirs.yml — manage home-directory locations and permissions.
- advanced-user-management.yml — combined desired-state deployment.
- verify-user-management.yml — independent checks with explicit pass/fail behavior.
- docs/ — architecture, operating steps, security controls, test matrix and portfolio wording.

## Quick start

Run commands from this directory on an Ansible control node. Use a disposable lab VM or dedicated test environment first.

~~~~bash
ansible-inventory -i inventory.ini --graph
ansible-inventory -i inventory.ini --list

for playbook in create-groups.yml create-users.yml modify-groups.yml \
  modify-shells.yml modify-home-dirs.yml advanced-user-management.yml \
  verify-user-management.yml; do
  ansible-playbook -i inventory.ini "$playbook" --syntax-check
done

# Preview changes first; -K prompts for the become password
ansible-playbook -i inventory.ini advanced-user-management.yml --check --diff -K

# Apply and independently verify
ansible-playbook -i inventory.ini advanced-user-management.yml -K
ansible-playbook -i inventory.ini verify-user-management.yml -K

# Re-run to assess idempotency
ansible-playbook -i inventory.ini advanced-user-management.yml -K
~~~~

The default inventory target is localhost. For remote lab use, configure approved remote hosts and change each play's hosts value only after reviewing the impact.

## Security considerations

- No password hashes, private keys or secrets are supplied or committed.
- Password provisioning is separate. Use an approved identity provider or Ansible Vault-protected password hashes if required; never store plaintext credentials in YAML.
- modify-groups.yml treats the groups list in vars/users.yml as authoritative and can remove memberships not declared there. Review before use on existing accounts.
- A shell change does not itself grant authorization. Validate sudo, SSH, PAM and group-based access independently.
- Coordinate UIDs/GIDs with LDAP/AD/SSSD, NFS, containers and existing host identities before enterprise rollout.
- Account deletion is intentionally outside this lab's automated scope.

## Documentation

- docs/architecture.md
- docs/operations-and-troubleshooting.md
- docs/security-controls.md
- docs/test-matrix.md
- docs/resume-achievement.md
