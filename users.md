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



# nosuSudo Power

- user should exit already
- user need to have password setup already for sudo

## add exiting user to wheel group
`usermod -aG wheel <username>`  

## universal sudoers config file
- `/etc/sudoers`
- edit this file with `visudo`

## edit this file of the user to give all permission
- `sudo vim /etc/sudoers.d/<username>`
- add this to the file
    - `<username> ALL=(ALL)   ALL`

## to give sudo permission to user
- `%wheel     ALL=(ALL)     ALL, newuser`
    - add newuser to wheel group

## to give user passwordless sudo access
- `<user> ALL=(ALL) NOPASSWD:ALL`

## give user from a certain group passwordless access
- `%<admins> ALL=(ALL) NOPASSWD:ALL`
    - notice `%`
