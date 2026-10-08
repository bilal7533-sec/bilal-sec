# Operations Runbook

## Day 1

ansible-inventory -i inventory/hosts.ini --graph
ansible all -m ping -k
ansible-playbook -i inventory/hosts.ini playbooks/site.yml --check --diff -k -K

## Rolling patching

Use a maintenance window and roll in small batches:

ansible-playbook -i inventory/hosts.ini playbooks/patch.yml --limit web_servers --check -k -K
ansible-playbook -i inventory/hosts.ini playbooks/patch.yml --limit web_servers -k -K

Recommended production workflow: change ticket -> approval -> CI -> canary -> serial batches -> health check -> ticket closure.

## Failure handling

Investigate by layer:
Reachability -> SSH service -> Identity -> Authentication -> Policy -> Authorization -> Application.

Capture ansible setup facts, journalctl output, service state, package state and firewall state before changing configuration.
