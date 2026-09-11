# Ansible CLI for Configuration Management

## Ad-Hoc Commands (Quick Actions)

Test connection and ping all managed hosts defined in the default inventory:
```bash
ansible all -m ping
```

Execute a raw shell command across all database servers:
```bash
ansible db_servers -m shell -a "uptime"
```

Securely gather system information and hardware facts from web servers:
```bash
ansible web_servers -m setup
```

## Playbook Execution

Run a configuration playbook using a custom inventory file:
```bash
ansible-playbook -i inventory.ini site.yml
```

Perform a dry-run execution of a playbook to preview changes without applying them:
```bash
ansible-playbook -i inventory.ini site.yml --check
```

Limit a playbook execution to a specific host group or target machine:
```bash
ansible-playbook -i inventory.ini site.yml --limit web_servers
```

Execute a playbook starting exactly at a specific named task tag:
```bash
ansible-playbook -i inventory.ini site.yml --tags "packages,config"
```

## Ansible Vault (Secrets Management)

Create a new encrypted file to store sensitive group variables:
```bash
ansible-vault create secret_vars.yml
```

Edit an existing encrypted secrets file on the fly:
```bash
ansible-vault edit secret_vars.yml
```

Encrypt an existing plain-text configuration file:
```bash
ansible-vault encrypt credentials.yml
```

Decrypt an encrypted file back into plain-text permanence:
```bash
ansible-vault decrypt credentials.yml
```

Run a playbook that requires an interactive prompt for the vault password:
```bash
ansible-playbook -i inventory.ini site.yml --ask-vault-pass
```
