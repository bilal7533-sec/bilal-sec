# Operations and Troubleshooting

## Recommended runbook

1. Review configured hosts with ansible-inventory -i inventory.ini --graph.
2. Validate syntax with ansible-playbook -i inventory.ini advanced-user-management.yml --syntax-check.
3. Preview changes on a disposable test host using --check --diff.
4. Apply the combined desired state with ansible-playbook -i inventory.ini advanced-user-management.yml -K.
5. Run verify-user-management.yml and retain console output as evidence.
6. Re-run the combined playbook and inspect whether unexpected changes remain.

## Useful read-only checks

~~~~bash
getent passwd alice
getent group devops
id alice
getent passwd alice | cut -d: -f6,7
stat -c '%U:%G %a %n' /opt/users/alice
grep -E '^(alice|bob|carol|david|eve|frank|grace):' /etc/passwd
~~~~

## Common failures

- **A required group is missing:** run create-groups.yml first, or use the combined playbook.
- **UID/GID already exists:** inspect getent passwd <uid> and getent group <gid>. Select approved unused identifiers rather than forcing a collision.
- **Shell path is invalid:** confirm it is executable and an approved login shell where applicable; the shell playbook checks existence and executable state.
- **Permission denied:** check SSH identity and sudo/become privileges. Do not put passwords in command history or source files.
- **Home move fails:** confirm the destination parent exists, the account is present, disk space is available and permissions permit the move. Back up important data before changing a real account's home path.
- **A group disappears from a user's memberships:** inspect vars/users.yml. modify-groups.yml uses append: false, making the configured supplementary-group list authoritative.
- **Verification fails on ownership or mode:** inspect the actual path with stat; re-run home-directory tasks only after confirming desired owner and mode.
- **Check mode differs from runtime:** some operating-system effects cannot be fully predicted during check mode. Validate on an isolated test VM before wider rollout.

## Recovery principles

Capture existing account/group metadata and back up important home directories before production changes. Prefer a controlled forward fix over deleting users or groups. This lab intentionally has no automatic user-deletion task.
