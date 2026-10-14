# Security Controls and Compliance Context

This is an engineering exercise, not a formal compliance certification or audit finding. Validate these implementation themes against the organization's current control catalogue.

| Security objective | Lab implementation | Verification evidence | Boundary / follow-up |
|---|---|---|---|
| Least privilege | Explicit per-user supplementary groups; private home permissions | id -nG, stat and verification playbook | Validate sudoers, SSH and application authorization separately |
| Controlled identity attributes | Central data file for names, UID/GID, shell and home path | Inventory review and getent output | Coordinate identifiers with LDAP/AD/SSSD and shared storage |
| Secure home directories | Home directory owner/group and mode 0750 | stat plus assertions | Confirm organizational access requirements before applying 0750 broadly |
| Repeatable change | Ansible modules express desired state | Syntax check, check mode and second run | Use change approval and staged rollout in production |
| Reduced credential exposure | No static password, private key or token is committed | Repository secret review | Use approved Vault/secret-management workflow if required |
| Accountability | Verification commands and documented test evidence | Saved playbook output and change record | Forward outputs to central audit/SIEM where required |

## NCA ECC context

Account lifecycle and group authorization work can support IAM/access-control objectives where applicable. Do not claim a specific NCA ECC control is satisfied from this lab alone. Confirm exact control IDs, version, applicability, evidence requirements and approved interpretations with the organization's compliance owner.
