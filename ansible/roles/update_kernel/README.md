# Role: update_kernel

Installs newer kernel image and linux-headers from debian backports as specified in the `update_kernel_version` variable. By default, will reboot the system via handler unless `update_kernel_reboot` is set to false. 
