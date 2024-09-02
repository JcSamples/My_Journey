
**Skeleton Directory**

By default, the contents of the `/etc/skel` directory are copied into the new user's home directory. The resulting files are also owned by the new user. By using the `-k` option with the `useradd` command, the contents of a different directory can be used to populate a new user's home directory. When specifying the skeleton directory with the `-k` option, the `-m` option must be used or else the `useradd` command will fail with an error.

The following example uses `/home/sysadmin` as the skeleton directory:

**root@localhost:~#** useradd -mk /home/sysadmin jane
**root@localhost:~#** ls /home/jane
Desktop  Documents  Downloads  Music  Pictures  Public  Templates  Videos

**Shell**

While the default shell is specified in the `/etc/default/useradd` file, it can also be overridden with the `useradd` command using the `-s` option at the time of account creation:

**root@localhost:~#** useradd -s /bin/bash jane

It is common to specify the `/sbin/nologin` shell for accounts to be used as system accounts.

**Comment**

The comment field, originally called the General Electric Comprehensive Operating System (GECOS) field, is typically used to hold the user's full name. Many graphical login programs display this field's value instead of the account name. The `-c` option of the `useradd` command allows for the value of this field to be specified.

**root@localhost:~#** useradd -c 'Jane Doe' jane