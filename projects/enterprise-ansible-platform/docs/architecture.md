# Architecture

## Trust zones

1. Control plane: Ansible control node and CI.
2. Management plane: SSH and sudo.
3. Web zone: HTTP/HTTPS service tier.
4. Application zone: internal application services.
5. Data zone: PostgreSQL and MariaDB.
6. Operations zone: bastion, utilities, monitoring and backup.

## Automation flow

Change request -> review/approval -> CI -> Ansible -> Vault secret retrieval -> SSH/sudo -> facts -> role -> handler -> verification -> evidence.

The same role model scales beyond this 30-node lab by changing inventory membership.
