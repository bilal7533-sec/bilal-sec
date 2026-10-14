# Portfolio and Interview Notes

## Portfolio description

Built a data-driven Ansible lab for Linux user and group lifecycle operations, covering account provisioning, supplementary group reconciliation, login-shell and home-directory changes, explicit file permissions, idempotent execution and post-change assertions.

## Technologies

Ansible, YAML, Linux users/groups, UID/GID management, SSH/sudo operations, getent, id, stat, check mode and Ansible Lint.

## Interview discussion points

- Why does one central user data file reduce configuration drift?
- What is the difference between a primary group and supplementary groups?
- Why can append: false be risky when managing pre-existing accounts?
- Why should a change be previewed and then verified independently?
- Why is a shell path not the same thing as an authorization control?
- How should local account management integrate with LDAP/AD, SSSD, PAM, sudo and SIEM?
- What is required before extending a localhost demonstration to many production servers?

Describe this as a lab/project unless you have personally run and captured the stated validation on the relevant target hosts. Do not represent a sample localhost inventory as production fleet experience.
