# VirtualBox
This project contains setup for a single machine with 3 hard drives.

# Installation

Priori to running `vagrant up` you have to do:

```bash
{
  vboxmanage createmedium --filename $PWD/disk-1.vdi --size 1024 --format VDI
  vboxmanage createmedium --filename $PWD/disk-2.vdi --size 1024 --format VDI
  vboxmanage createmedium --filename $PWD/disk-3.vdi --size 1024 --format VDI
}
```

# Help
Run below command to get list of available storage controllers.
```bash
$ vboxmanage showvminfo sandbox
```

# Notes
Remember to run `vagrant destroy`.


# Logic Volume Group  

```bash
# Crate physical volume
$ pvcreate /dev/sdb /dev/sdc /dev/sdd

# Crate volume group  
$ vgcreate compare01_data_vg1 /dev/sdb /dev/sdc /dev/sdd
$ vgchange -ay compare01_data_vg1

# Create logical volume
$ lvcreate -n data -l 100%VG compare01_data_vg1

# Create file system on logical volume volume
$ mkfs.ext4 /dev/mapper/compare01_data_vg1-data

# Mount logical volume
$ mkdir /mnt/compare_data
$ mount -t ext4 /dev/mapper/compare01_data_vg1-data /mnt/compare_data/

# List block id
$ blkid
/dev/mapper/compare01_data_vg1-data: UUID="11d841c9-1902-4648-8b74-3a47de7396f7" TYPE="ext4"

# Mount device in /etc/fstab
UUID=11d841c9-1902-4648-8b74-3a47de7396f7 /mnt/storage            ext4    defaults	  0 0
```
