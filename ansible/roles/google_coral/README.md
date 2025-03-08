# Role: google_coral

Installs drivers necessary for using Google Coral M2/PCIe TPU module. 

## Tasks

### main.yml

Adds the Google Cloud SDK repository with GPG signing key. Installs needed dependencies (linux-headers-amd64, dkms). Depending on current kernel version, will either install the gasket-dkms module from the Google repository or install a manually built deb file (more info below). Creates the `apex` user group and gives read/write permissions to that group. This is needed for applications to utilize the coral TPU. Then adds the user specified in the `google_coral_user` variable to that group. Finally, will trigger a system reboot if needed and the `google_coral_reboot` variable is set. 

### stable.yml

Installs the `gasket-dkms` and `libedgetpu1-std` modules from the Google Cloud SDK repository if kernel version is older than 6.12

### manual.yml

Installs the `libedgetpu1-std` module from the Google Cloud SDK repository. Then manually copies a built deb file to the host that includes a fix for kernel versions at 6.12 or newer. These fixes have pending pull requests on the gasket-dkms repository, so the official package is not available yet. 

**Commit**: https://github.com/google/gasket-driver/commit/4b2a1464f3b619daaf0f6c664c954a42c4b7ce00
**PR**: https://github.com/google/gasket-driver/pull/35
