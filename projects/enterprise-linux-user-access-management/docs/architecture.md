# Architecture and Desired-State Model

## Control flow

Ansible control node → inventory target → privilege escalation → managed groups → user accounts → supplementary memberships → login shell and home path → independent verification.

The default inventory target is localhost. A production deployment would replace that target with approved managed hosts and rely on controlled SSH identity, host-key verification, sudo policy and a change window.

## Data-driven configuration

The file vars/users.yml is the single source of truth for demonstration users and supplementary groups. The playbooks import it through vars_files to reduce configuration drift.

- managed_groups: group names and example GIDs.
- users: account name, example UID, comment, shell, home path and supplementary groups.

## Idempotency model

Ansible group, user and file modules express desired state. A second run should normally report no changes if the host already conforms to the data file. Verification uses read-only lookups and assertions to detect drift.

## Important boundary

The project manages local Unix accounts only. It does not configure LDAP, Active Directory, SSSD, PAM, SSHD, sudoers policy, MFA or password rotation. Those controls must be designed and tested separately before calling the overall access-management system enterprise-ready.
