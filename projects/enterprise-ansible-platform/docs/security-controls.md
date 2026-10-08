# Security Control Mapping

| Area | Automation evidence |
|---|---|
| Least privilege | Dedicated application service account; root login disabled |
| Secure remote access | SSH hardening and explicit AllowGroups |
| Host hardening | auditd, secure permissions, legacy telnet disabled |
| Network control | UFW and firewalld managed from variables |
| Change control | CI syntax/lint and rolling patch workflow |
| Recovery | Backup-tier inventory and documented production extension |
| Auditability | Git history and verification playbook |
| Secrets | Vault integration point; no plaintext credentials |
| Availability | serial patching and failure threshold |

This is an engineering mapping for a lab/reference project, not a certification claim.
