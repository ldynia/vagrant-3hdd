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
