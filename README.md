# Linux-Operation-Essentials
Notes from LFCS on Pluralsight

## Introducing the LFCS
### Reading Operating System Data
Read operating system info
```
$ cat /etc/system-release
$ lsb_release -d
```

lsb_release is only available after you installed it
```
$ rpm -qf $(which lsb_release)
```

Version of kernel
```
$ uname -r
$ cat /proc/version
```

Bootup arguments
```
$ cat /proc/cmdline
```

```
$ lsblk
```

## Starting and Stopping CentOS 7
### Introduction and Using wall
```
# write username
# wall < messageFile
```

### Shutdown Commands
Legacy commands
```
# init --help
# telinit --help
```

-h halt; -r reboot
```
# shutdown -h 10 message
# shutdown -c
```

This file will occur when it has less than 5 mins to shutdown
```
# ls /run/nologin
```

### Changing Runlevels & Set Default
graphical.target is level 5
```
# who -r
# runlevel
```

multi-user.target is level 3
rescue.target is level 1
```
# systemctl get-default
# systemctl set-default multi-user.target
# systemctl isolate multi-user.target
# who -r
# systemctl isolate rescue.target
```

### Selecting Runlevels at Boot
Booting to Rescue.Target, single user (root) mode
  1. ESC in GRUB
  2. e to edit
  3. Search for linux16 line and ctrl+e
  4. Append systemd.unit=rescue.target
  5. After repairing the system, ctrl+x or F10 to exit

## The Boot Process
### Managing GRUB Recovery
Modify GRUB configuration, change GRUB_DISABLE_RECOVERY="false"
```
# vi /tec/default/grub
# grub2-mkconfig -o /boot/grub2/grub.cfg
# reboot
```

### Reset Lost Root Passwords
Boot to initramfs
  1. ESC in GRUB
  2. e to edit
  3. Search for linux16 and ctrl_e
  4. remove "rhgb quiet", append "rd.break enforcing=0"
  5. remount root
     ```
     # mount -o remount,rw /sysroot
     # chroot /sysroot
     # passwd
     # exit
     # mount -o remount,ro /sysroot
     # exit
     ```
  6. restore security context
     root password is stored in /etc/shadow
     ```
     # restorecon /etc/shadow
     # setenforce 1
     ```

## Managing GRUB2
### Introduction and Re-installing GRUB
Re-install GRUB
```
# grub2-install /dev/sda
```

UEFI based machine, use
```
# yum reinstall grub2-efi shim
```

### Manage GRUB2 Defaults
```
# vi /etc/default/grab
# grub2-mkconfig -o /boot/grub2/grub.cfg
```

### Manage Persistent Setting with grubby
```
# grubby --default-kernel
# grubby --set-defalt /boot/vmlinuz-XXXX
# grubby --info=ALL
# grubby --info=1
# grubby --remove-args="rhgb quiet" --update-kernel /boot/vmlinz-XXXX
```

### Password Protect GRUB2
```
# vi /etc/grub.d/01_users
```

The superusers is not related to your linux users
```
#!/bin/sh -e
cat << EOF
  set superusers="username"
  password username password
EOF
```

```
# grub2-mkconfig -o /boot/grub2/grub.cfg
```

Or use encrypted password, you'll have a hashed password
```
# grub2-mkpasswd-pbkdf2
```

Then edit `/etc/grub.d/01_users`
```
#!/bin/sh -e
cat << EOF
  set superusers="username"
  password_pbkdf2 username hashed_pw
EOF
```

```
# grub2-mkconfig -o /boot/grub2/grub.cfg
# reboot
```

### Custom GRUB2 Entries
```
# cat <<END > custom
menuentry 'Erics CentOS' {
  insmod gzio
  insmod part_msdos
  insmod xfs
  set root='hd0,msdos1'
  linux16 /vmlinuz-3.10.0-514.10.2.el7.x86_64 root=/dev/mapper/centos-root ro crashkernel=auto rd.lvm.lv=centos/root rd.lvm.lv=centos/swap
  initrd16 /initramfs-3.10.0-514.10.2.el7.x86_64.img
}
END
```

```
# vi /etc/grub.d/40_custom
```

and read in custom file to `/etc/grub.d/40_custom`, inside vim:
```
:r /root/custom
```

```
# grub2-mkconfig -o /boot/grub2/grub.cfg
# reboot
```

## Managing Linux Processes
## Process Priority
## Monitor Linux Performance
## Using Sysstat to Monitor Performance
## Managing Shared Libraries
## Scheduling Tasks in Linux
## Log Files and Logrotate
## Introducing SELinux
## Managing Software on CentOS 7
## Configuration Management Tools
