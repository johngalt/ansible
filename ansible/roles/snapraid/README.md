# Role: snapraid

Installs and configures snapraid, snapraid-btrfs, snapper, and snapraid-btrfs-runner.

## Tasks

### install_snapraid.yml

Installs/updates snapraid based on defined `snapraid_version` variable. Installs dependencies from apt, then pulls snapraid source from github into temporary directory. Configures, makes, and installs snapraid. 

### configure_snapraid.yml

First verifies the paths for the defined `snapraid_data_dirs`, `snapraid_content_files`, and `snapraid_parity_files` exists. Then creates a snapraid config at the location defined by `snapraid_config_path` based off the template `snapraid.j`. 

The list variable `snapraid_data_dirs` expects absolute paths of directories to be backed up by snapraid. The list variable `snapraid_content_files` expects absolute paths to where you want generated *.content* files to end up at. The list variable `snapraid_parity_files` expects an absolute path to the snapraid parity file. This does not allow for multiple parity files (not yet done). 

### install_snapper.yml

Adds openSUSE repository key to debian keyring. Then adds the openSUSE snapper repository to apt sources (signed by openSUSE gpg key). Will then install the `snapper` and `libsnapper` packages from that repository. 

### install_snapraid-btrfs.yml

Clones the snapraid-btrfs source from github to a temporary directory. Then copies the snapraid-btrfs script to /usr/local/bin. 

### configure_snapper.yml

First gets current list of snapper configs (if any are set already). If a snapper config doesn't exist for a data directory defined in `snapraid_data_dirs`, it is then created. It uses the "default" template, which is slightly modified to disable the `TIMELINE_CREATE` feature, since snapraid-btrfs-runner handles creating snapshots prior to snapraid sync.

### install_snapraid-btrfs-runner.yml

Clones the snapraid-btrfs-runner repository. Can use a custom defined repository if personal edits are made to the script via the `snapraid_btrfs_runner_repo` variable. Supports ssh key as well via `snapraid_btrfs_runner_repo_key`. Creates a config file based on the `snapraid-btrfs-runner.j2` template. Pulls in variables defined in `snapraid_btrfs_runner_conf` dictionary variable. Then creates/starts a systemd timer service to run the script. Can configure when the systemd timer runs via the `snapraid_btrfs_runner_timer` variable (uses OnCalendar timing rather than cron).
