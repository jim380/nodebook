# Create a New User
[ [ Intro ] ](README.md) -- [ [**New User**](user.md) ] -- [ [Hard Drive](harddrive.md) ] -- [ [Daemon](daemon.md) ]

-----
## Add a New User `storj`
Add a new user ```storj``` of which the directory will be placed in the `/home` directory. The name of the directory will be the same as the user’s name.
- `useradd -m -s /bin/bash storj`

You should now see the new user's directory `storj` listed under `/home`.
- `$ ls -la /home`
```
total 16
drwxr-xr-x  4 root   root   4096 Feb 17 01:09 .
drwxr-xr-x 23 root   root   4096 Jan 11 19:28 ..
drwxr-xr-x 18 odroid odroid 4096 Feb 14 19:35 odroid
drwxr-xr-x 11 storj  storj  4096 Feb 17 01:40 storj
```
You can further check if `storj` is on the lists of users as well as groups on the system.
- `$ cat /etc/passwd`
```
storj:x:1001:1001::/home/storj:/bin/bash
```
- `$ cat /etc/group`
```
storj:x:1001:
```

## Set a password for `storj`
- `$ passwd storj`
```
Enter new UNIX password:  
Retype new UNIX password:  
passwd: password updated successfully
```

## Delegate Rights to `storj` to Run `sudo` Commands
- `$ sudo adduser storj sudo`
```
Adding user `storj' to group `sudo' ...  
Adding user storj to group sudo  
Done
```

## Login as `storj`
Exit out current ssh session.
- `$ exit`

Log in with `storj`.
- `$ ssh storj@<IP>`

Install Node Version Manager (NVM) Shell.
- `$ wget -qO- https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh | bash`

Log out and then log in as `storj` again.
- `$ ssh storj@<IP>`

---
Let's get started: [Hard Drive](harddrive.md)