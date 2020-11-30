# Duo-Linux-2FA
Automatically deploy Duo 2FA on major Linux distributions.

### Supported Distributions
 - Ubuntu
 - Debian
 - CentOS

### Overview
This Ansible playbook either configures just Duo 2FA, or performs additional setup and hardening, depending on the tag used:

|                                  | base | full |
|----------------------------------|------|------|
| Hardens SSH configuration        |      | ✓    |
| Installs and configures firewall |      | ✓    |
| Installs and configures Duo      | ✓    | ✓    |
| New SSH user w/ keys             |      | ✓    |
| Disables root SSH access         |      | ✓    |

### Usage
 1. Create a Duo account and make a UNIX Application.
 2. Gather the secrets for the application and place them in 'duo_vars.secret.yaml'. See duo_vars.secret.yaml.example for syntax.
 3. After saving your secrets in duo_vars.secret.yaml, encrypt it using `ansible-vault encrypt duo_vars.secret.yaml`.
 4. Create a text file with your chosen vault password (default is ~/.ansible_vault)
 5. Restrict the permission on the password file using `chmod 600 ~/.ansible_vault`
 6. Add host(s) to the host file. Specify the desired SSH port and sudo timeout (grace period from 2FA when using sudo)
 7. If you wish to add a new SSH user and disable root SSH login, modify new_user_creds.secret.yaml in the same way as the Duo secrets. SSH keypairs will be dropped in the defined directory (put it outside the Git repo). 
 8. Execute playbook with `ansible-playbook main.yaml --tags "base"` or `--tags "full"`
