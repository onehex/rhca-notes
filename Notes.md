# Other Notes
https://github.com/pushkar100/notes-linux-admin
https://github.com/jrandj/redha

# user
## user defualt files - (*)
- for passwords and defult age of password
- cahnge this to stop user to login 
- `/etc/login.defs`
- `/etc/default/useradd`

## commands
- `useradd` : adding user
    - `-d` : add user home directory
    - `-p` : password
    - `c` : for comment
- `userdel` : deleteing user
- `chage` : for password expiration 


# local user
- local user can only modify only 2 dirs
- `/home/<usrename>`
- `/tmp`


# sudo
> Give USER Ultra powerfull abilities to destroy everything (no really)

- user should exit already
- user need to have password setup already for sudo

## add exiting user to wheel group
- `usermod -aG wheel <username>`  
    - this add user to to `/etc/group`

## universal sudoers config file
- `/etc/sudoers`
- should not edit
- safe edit this file with `visudo`


## user sudoers file
- `/etc/sudoers.d/<user>`
> edit this

### edit this file of the user to give all permission
- `sudo vim /etc/sudoers.d/<username>`
- add this to the file
    - `<username> ALL=(ALL)   ALL`


### to give user passwordless sudo access
- `<user> ALL=(ALL) NOPASSWD:ALL`

### give user from a certain group passwordless access
- `%<admins> ALL=(ALL) NOPASSWD:ALL`
    - notice `%`

### allow only specific commands
- in user's `/etc/sudoer.d/<username>` file
- `<user>   ALL=(root)  /path/to/commands, /command2, NOPASSWD:ALL`
- get path of the command
    - `which <command>`


# Permission
- give permission to all
    - `chmod a+rwx <file/dir>`
    - a for all

- add to multiple
    - `chmod ugo-rwx <file/dir>`

## numeric file permissions
0 = no permission
1 = execute
2 = write
4 = read


# Special Permissions

## sticky bit
- you need 777 permission to set sticky bit
    - `chmod 777 /dir`
- stick bit
    - `chmod o+t /dir`


# Umask
- defualt dir permission - `777`
- defualt file permission - `666`
```
## directory
defualt     7 7 7
umask       0 2 2
result      7 5 5

## file
defualt     6 6 6
umask       0 2 2
result      6 4 4
```

## example
- you wan defulat perssion of 552 on dir and 432 on files
- what would be the umask

dir umask = 777 - 553 = 224
file umask = 666 - 432 = 234

to set defualt perssion set umask


# LVM
https://blog.victormendonca.com/2020/11/18/linux-logical-volume-manager/


# graphical targets

## set cli as defualt target
`systemctl set-default multi-user.target`

## set gui as defualt target
`systemctl set-default graphical.target`

## GO in GUI Temprary
`init 5`


# Go into emeergency mode with
`init 6`

- find line with `vmlinuz` and to the end of the line and add `rd.break` and press `ctrl + x`

# Passwrod Breaking Steps
1. rd.break
2. mount -o remount,rw /sysroot
3. chroot /sysroot
4. passwd root
5. touch /.autorelable
6. exit
7. exit




# Process
> when program loaded into memory and start running becomes a process

# commands
- `top`
- `ps aux`
- `sleep 1000`
- kill process
    - `kill <PID>`
    - `kill -9 <PID>` <-- force kill
- `w`
- `uptime`
- `lscpu`


# services
commands
start stop enable disable restart
mask  --> isolate service from update/change
unmask --> remove mask


# logs
- common directories
    - /var/log
        - messages  <-- logs
        - secure  <-- 
        - cron
        - boot.log  <-- generated on/before boot time

- logs generated because of this file (importent)
    - /etc/rsyslog.conf

## Events
> see in book

- journalctl
    - `-n`
    - -l
    - --since "2023-04-12 09:30:00" --until "2023-05-12 09:00:00"
    - --since "-1 hour"
    - -p
        - error
        - alert
        - notice
        - warning
        - info
        - debug


# Time
- timedatectl
- timedatectl list-timezones
- timedatectl set-timezone Aisa/Kolkata

# time sync (Q)
> rhel9 uses chrony
vim /etc/chrony.conf
add this , address will be given?
`server <address> ibrust`
`systemctl restart chronyd`
`chronyc sources -v`



# Job Scheduel

- /etc/crontab

`crontab -e -ls u <username>`
enter --> new screen with file --> add this and save
`17  11  *   *   *   <username> mkdir /test`
> remember firs * is minute second * is hour
> this is a recuring job 

- list jobs
    - `crontab -lu <username>`

## Networking
cidr.xyz

## show network address
ip a
ip addr


## set ip from GUI
corner > wired connection > wired settings > ip4 > manual

## set ip from commandline
nmcli connection show

nmcli con mod ens160 ip4.addresses 192.168.12.14/24 ipv4.gateway 192.168.12.254 ipv4.dns 192.168.254.254 ip4.method manual

nmcli connection down ens160

nmcli connection up ens160


## hostname
hostname
hostnamectl set-hostname newhost.name.com

bash


## nameserver
/etc/resolv.conf
> restart netwrok manager entry will come back


# tuned
yum install tuned
systemctl restart tuned
tuned-adm profile
tuned-adm recommend
tuned-adm profile virtual-guest
tuned-adm profile balanced
tuned-adm profile active

# firewall
yum install firewalld
firewall-cmd --list-all
firewall-cmd --get-services

## add service to firewall
firewall-cmd --permanent --add-service=http
> permanent is important

firewall-cmd --list-services
firewall-cmd --reload
firewall-cmd --list-services

firewall-cmd --permanent --add-port=443/tcp
firewall-cmd --reload
firewall-cmd --list-ports

firewall-cmd --permanent --remove-port=443/tcp
firewall-cmd --reload
firewall-cmd --list-ports

firewall-cmd --permanent --remove-service=http
firewall-cmd --reload
firewall-cmd --list-services



# SELinux
ls -lZ

## change context
chcon -t httpd_sys_content_t demo.txt

restorecon -v demo2.txt <-- change defualt context

## change mode
vim /etc/selinux/config
    - SELINUX=<mode>  <-- change mode permanently


- setenforce

- check enforce
    - getenforce


setsebool -P samba_enable_home_dirs
setsebool -P samba_enable_home_dirs on
setsebool -P samba_enable_home_dirs off


# SSH

# NFS


# Bash Script

## backup
```bash
#!/bin/bash

read -p "enter dir to backup (ex: /etc) : " SOR
read -p "enter destination to save backup (ex: /home): " DEST

tar -cvjf $DEST/backup.tar.bz2 $SOR 

```


# podman