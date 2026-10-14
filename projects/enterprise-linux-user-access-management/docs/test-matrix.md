# Test Matrix

| Test | Method | Expected result |
|---|---|---|
| Inventory | ansible-inventory -i inventory.ini --graph | The local target is visible and no unintended remote hosts are targeted |
| Syntax | ansible-playbook -i inventory.ini <playbook>.yml --syntax-check | Every playbook parses |
| Preview | Run combined playbook with --check --diff | Proposed changes are displayed without intentionally applying them |
| Group provisioning | Run create-groups.yml then getent group devops | Managed groups exist with declared lab GIDs |
| Account provisioning | Run create-users.yml, then getent passwd alice | Configured account appears with expected home and shell |
| Group membership | Run modify-groups.yml then id alice | Expected supplementary groups are present |
| Shell validation | Run modify-shells.yml | Executable target shells are accepted and applied |
| Home location | Run modify-home-dirs.yml then stat /opt/users/alice | Home location, ownership and mode match desired state |
| Combined deployment | Run advanced-user-management.yml | Groups, accounts and home directories converge |
| Verification | Run verify-user-management.yml | All assertions pass when host matches the data file |
| Idempotency | Run combined deployment a second time | Existing compliant state should show no unexpected changes |
| Negative case | On disposable VM only, temporarily configure a missing group or invalid shell | A precheck/assertion fails; restore valid data afterward |

Do not run negative-case mutations on a workstation or shared production system. Save command output, date, target name and approved change/ticket identifier as evidence.
