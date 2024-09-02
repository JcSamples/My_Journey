

**Creating Groups**

````Shell
groupadd -r pesquisa
groupadd -r vendas

Questionar sempre se é necessário especificar o GID
`````

The research and sales groups that have just been added were added within the reserved range (between 1-999) because the `-r` option was used.  
With this option, group identifiers (GIDs) are automatically assigned a value lower than the lowest normal user UID.


**Confirming Group Creation**


````Shell
grep vendas /etc/group
cat /etc/groups
`````

**getent Command: Checking Group Data**

````C#
getent group pesquisa
`````

**Changing the Name of an Existing Group**

````C
groupmod -n [novo nome] [nome antigo]
`````

**Changing GroupID**

````C#
groupmod -g 10003 assistentes
`````

**Deleting a Group**

````C
groupdel [nome do grupo a eliminar]
`````
