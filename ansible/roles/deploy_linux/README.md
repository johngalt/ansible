# Role: deploy_linux

Runs initial tasks on new linux install. Requires sudo to be installed. 

## Tasks

### main.yml

Enables passwordless sudo after confirming sudo is installed.

### users.yml

Loops through items in `deploy_linux_users` list and creates user accounts. If groups are defined in users, the groups will be created first. Additionally, will add ssh public keys to each defined users authorized_keys file if needed. 

### sshd.yml

Disables root login through SSH. Disables PAM authentication. Disables password logins and forces passkey authentication. Restarts ssh service via handler if tasks result in change.

### debian.yml

Runs Debian-specific tasks. Mainly, enables unattended upgrades. If variable `deploy_linux_deb_backports_enabled` is set to `true`, will add backports repository to apt sources. 
