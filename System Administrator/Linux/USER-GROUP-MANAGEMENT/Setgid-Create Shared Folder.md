
1. Creates a new group called `team`.
2. Adds `bob`, `sue`, and `tim` to the `team` group.
3. Makes a new directory called `/home/team`.
4. Makes the group owner of the `/home/team` directory be the `team` group.
5. sets the setgid permission to the `/home/team` directory

## Setting Setgid

Use the following syntax to add the setgid permission symbolically:

````shell
chmod g+s <file|directory>
`````

To add the setgid permission numerically, add 2000 to the file's existing permissions (assume in the following example that the directory originally had 775 for its permissions):

````shell
chmod 2775 <file|directory>
`````

To remove the setgid permission symbolically, run:

````shell
chmod g-s <file|directory>
`````

To remove the setgid permission numerically, subtract 2000 from the file's existing permissions:

````shell
chmod 0775 <file|directory>
`````


## Sticky Bit

The sticky bit permission is used to prevent other users from deleting files that they do not own in a shared directory.


````shell
chmod o+t <directory>

To set the sticky bit permission numerically, add 1000 to the directory's existing permissions (assume the directory in the following example originally had 775 for its permissions):

chmod 1775 <file|directory>
`````


To remove the sticky permission symbolically, run:

````
chmod o-t <directory>
`````

