# user defualt files - (*)
- for passwords and defult age of password
- cahnge this to stop user to login 
- `/etc/login.defs`
- `/etc/default/useradd`

# commands
- `useradd` : adding user
    - `-d` : add user home directory
    - `-p` : password
    - `c` : for comment
- `userdel` : deleteing user
- `chage` : for password expiration 


# local user
- locla user can only modify only 2 dirs
- `/home/<usrename>`
- `/tmp`