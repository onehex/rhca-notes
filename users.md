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