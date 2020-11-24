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
 5. Adds a new sudo user and disables root login for SSH.

### Usage
 1. Create a Duo account and make a UNIX Application.
 2. Gather the secrets for the application and place them in 'duo_vars.secret.yaml'. See duo_vars.secret.yaml.example for syntax.
 3. After saving your secrets in duo_vars.secret.yaml, encrypt it using `ansible-vault encrypt duo_vars.secret.yaml`.
 4. Create a text file with your chosen vault password (default is ~/.ansible_vault)
 5. Restrict the permission on the password file using `chmod 600 ~/.ansible_vault`
 6. Add host(s) to the host file. Specify the desired SSH port and sudo timeout (grace period from 2FA when using sudo)
 7. If you wish to add a new SSH user and disable root SSH login, modify new_user_creds.secret.yaml in the same way as the Duo secrets. SSH keypairs will be dropped in the defined directory (put it outside the Git repo). Otherwise, comment out the ssh_user role and its associated variable include. 
 8. Connect to the hosts via SSH and drop into root: `sudo su root`. **Leave these open until you've verified full functionality. Being logged in as root will circumvent any authentication issues with SSH or sudo.**
 9. Execute playbook with `ansible-playbook main.yaml`
 10. Connect to the system over SSH and verify configurations against [Duo's guide](https://duo.com/docs/duounix), if desired.
 11. Ensure you can access the servers via SSH and use sudo before closing the root sessions.  
