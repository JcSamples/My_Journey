### Specify password policy

````shell
/etc/login.defs
`````

## 16.3.5.2 Managing Password Aging

The `chage` command provides many options for managing the password aging information found in the `/etc/shadow` file.

Here's a summary of the chage options:

|Short Option|Long Option|Description|
|---|---|---|
|`-l`|`--list`|List the account aging information|
|`-d LAST_DAY`|`--lastday LAST_DAY`|Set the date of the last password change to `LAST_DAY`|
|`-E EXPIRE_DATE`|`--expiredate EXPIRE_DATE`|Set account to expire on `EXPIRE_DATE`|
|`-h`|`--help`|Show the help for the `chage` command|
|`-I INACTIVE`|`--inactive INACTIVE`|Set account to permit login for `INACTIVE` days after password expires|
|`-m MIN_DAYS`|`--mindays MIN_DAYS`|Set the minimum number of days before the password can be changed to `MIN_DAYS`|
|`-M MAX_DAYS`|`--maxdays MAX_DAYS`|Set the maximum number of days before a password should be changed to `MAX_DAYS`|
|`-W WARN_DAYS`|`--warndays WARN_DAYS`|Set the number of days before a password expires to start displaying a warning to `WARN_DAYS`|

A good example of the `chage` command would be to change the maximum number of days that an individual's password is valid to be 60 days:

````shell
**root@localhost:~#** chage -M 60 jane
**root@localhost:~#** grep jane /etc/shadow | cut -d: -f1,5
jane:60
`````

