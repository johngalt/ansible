# Role: gitea_runner

Installs runner agent for gitea actions.

## Tasks

### install.yml

Creates user account for the user to run the runner agent as. Defined in the `gitea_runner_user` variable. Downloads release from github based off of version defined in the `gitea_runner_version` varaible. Copies the binary from the release to `/usr/local/bin/`.

### configure.yml

Registers the act_runner service to your gitea instance. Uses the provided information from the `gitea_runner_instance` and `gitea_runner_token` variables. 

### systemd.yml

Creates a systemd service to automatically run the act_runner. Configures the service to run as the user defined in the `gitea_runner_user` variable.
