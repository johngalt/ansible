# Role: backrest

Installs/upgrades restic and backrest. Requires bzip2 which will be installed if not present.

## Tasks

### restic.yml

Downloads version of restic from GitHub as defined in the `backrest_restic_version` variable. Copies binary to /usr/local/bin. 

### install.yml

Downloads version of backrest from GitHub as defined in `backrest_version` variable. Will check current installed version of backrest via a regex match from the systemd service file.

### systemd.yml

Creates systemd service for running backrest. Can configure what user to run the service on via the `backrest_user` variable. Similarly, can configure the host and port via `backrest_host` and `backrest_port` variables. 
