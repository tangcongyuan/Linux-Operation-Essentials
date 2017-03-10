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
