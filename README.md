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
## Managing GRUB2
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
