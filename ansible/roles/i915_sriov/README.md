# Role: i915_sriov

Installs latest i915-sriov-dkms custom kernel module from [Github](https://github.com/strongtz/i915-sriov-dkms). Requires linux kernel version > 6.8. This module allows for the use of virtual functions (VFs) from the integrated GPU on newer intel CPUs. Having the module installed on Proxmox host and guest allows passing through VFs of the iGPU to VMs (rather than passing through the entire iGPU and losing functionality of it on the host). 

## Tasks

### main.yml

Checks if current installed kernel will support the i915-sriov-dkms module prior to installing. Will only run the `install` task if the module is not already installed OR the version defined in `i915_sriov_version` is newer than the installed version. 

### install.yml

First installs needed dependencies (linux-headers, build-essential, dkms). Then downloads the release of the i915-sriov-dkms module as specified by the version variable `i915_sriov_version`. The deb file is installed via apt. The task then updates the grub settings to enable functionality of the module. If there are changes, several handlers are ran including `update-grub` and `update-initramfs`. Finally, a reboot is triggered if needed and allowed by the `i915_sriov_reboot` setting variable.
