
MODIFY USER

The `usermod` command offers many options for modifying an existing user account. Many of these options are also available with the `useradd` command at the time the account is created. The following chart provides a summary of the `usermod` options:

|Short Option|Long Option|Description|
|---|---|---|
|`-c`|`COMMENT`|Sets the value of the GECOS or comment field to `COMMENT`.|
|`-d HOME_DIR`|`--home HOME_DIR`|Sets `HOME_DIR` as a new home directory for the user.|
|`-e EXPIRE_DATE`|`--expiredate EXPIRE_DATE`|Set account expiration date to `EXPIRE_DATE`.|
|`-f INACTIVE`|`--inactive INACTIVE`|Set account to permit login for `INACTIVE` days after password expires.|
|`-g GROUP`|`--gid GROUP`|Set `GROUP` as the primary group.|
|`-G GROUPS`|`--groups GROUPS`|Set supplementary groups to a list specified in `GROUPS`.|
|`-a`|`--append`|Append the user's supplemental groups with those specified by the `-G` option.|
|`-h`|`--help`|Show the help for the `usermod` command.|
|`-l NEW_LOGIN`|`--login NEW_LOGIN`|Change the user's login name.|
|`-L`|`--lock`|Lock the user account.|
|`-s SHELL`|`--shell SHELL`|Specify the login shell for the account.|
|`-u NEW_UID`|`--uid NEW_UID`|Specify the user's UID to be `NEW_UID`.|
|`-U`|`--unlock`|Unlock the user account.|

### Modify Groups

| `groupmod` -n | change the name of a group   |
| ------------- | ---------------------------- |
| `groupmod` -g | change the GID for the group |

````shell
groupmod -g 10003 clerks
`````

````shell
find / -nogroup    = Find orfan files
`````

