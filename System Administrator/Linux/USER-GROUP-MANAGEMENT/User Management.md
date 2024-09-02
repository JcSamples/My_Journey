
Some changes will only take effect when the user logs out and logs in

**Create User** 

````shell
1-useradd -G [Group] -c 'Comment at login' -m [user]
2-passwd [user]


The -m option makes the [user] the owner of their own group.

Add to secondary group:

usermod -aG [Group] [User]

`````

**Delete user**

````C
userdel -r [user]
`````

**Confirm**

````shell
getent group [group name]
getent group [user]
getent passwd [user]
getent shadow [user]
`````

````shell
useradd -D
useradd -k "this option allows the home directory to be different"
useradd -D -f 30 
"The -f 30 option specifies that users with expired passwords can still log in
for thirty days before their accounts are disabled."

`````


Check information about Mail-Pool and Password Expiration The mail-pool is simply like creating an email folder for the user.

````C
/etc/default/useradd
`````

**MANIPULAÇÃO**

| useradd -g       | assign a different primary group                  |
| ---------------- | ------------------------------------------------- |
| useradd -D       | check and manipulate user information             |
| useradd -b       | allows specifying a different base directory      |
| useradd -e       | allows specifying a day when the password expires |
| useradd -s       | allows specifying a different shell               |
| useradd -D -f 30 | makes the account inactive after 30 days          |


ADDING TO GROUPS

Specify primary group
````c#
**root@localhost:~#** useradd -g users jane
`````

Specify supplementary groups

````c#
**root@localhost:~#** useradd -G sales,research jane
`````

Assign user to an existing directory

````c#
**root@localhost:~#** useradd -md /test/jane jane
```