# Role: zfs

Installs ZFS support from debian backports repository. 

## Tasks

### main.yml

Pins `zfs-linux` apt src to use backports repository. Then installs the `zfsutils-linux` and `zfs-dkms` modules from apt. 
