# Duo-Linux-2FA
Automatically deploy Duo 2FA on major Linux distributions.

### Supported Distributions
 - Ubuntu
 - Debian
 - CentOS

### Overview
 1. Performs common SSH hardening tasks, including changing the SSH port.
 2. Installs the duo-unix PAM module.
 3. Reconfigures SSH to use public key and Duo for two-factor authentication.
 4. Updates PAM configurations.

### Usage

 1. Create a Duo account and make a UNIX Application.
 2. Gather the secrets for the application and place them in 'duo_vars.secret.yaml'. See duo_vars.secret.yaml.example for syntax.
 3. After saving your secrets in duo_vars.secret.yaml, encrypt it using `ansible-vault encrypt duo_vars.secret.yaml`.
 4. Create a text file with your chosen vault password (default is ~/.ansible_vault)
 5. Restrict the permission on the password file using `chmod 600 ~/.ansible_vault`
 6. Add host(s) to the host file. Specify the desired SSH port and sudo timeout (grace period from 2FA when using sudo)
 7. Execute playbook with `ansible-playbook main.yaml`
