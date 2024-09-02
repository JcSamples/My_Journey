### Access PostgreSQL

````Shell
sudo -i -u postgres
psql
`````

#### Check user permissions

````sql
Check the permissions granted to the user by running:

SELECT grantee, privilege_type FROM information_schema.role_table_grants WHERE table_name = 'rengine';

`````

````sql
sudo -i -u postgres
psql

-- List all databases
\l

-- List all users (roles)
\du

-- Check privileges
\dp

-- SQL queries to see details of roles and databases
SELECT * FROM pg_roles;
SELECT * FROM pg_database;

-- Disconnect from the database and exit psql
\q

exit

`````
