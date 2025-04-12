# PostgreSQL Cheat-Sheet

## Connect to PostgreSQL

| Command                                  | Description                                           |
| ---------------------------------------- | ----------------------------------------------------- |
| `psql -U postgres`                       | Connect to PostgreSQL as the `postgres` user          |
| `psql -U <user> -d <database>`           | Connect to PostgreSQL as a specific user and database |
| `psql -U <user> -d <database> -h <host>` | Connect to PostgreSQL on a specific host              |

## PostreSQL CLI Commands

| Command            | Description                                              |
| ------------------ | -------------------------------------------------------- |
| `\c <database>`    | Connect to a specific database                           |
| `\password <user>` | Change password for a specific user                      |
| `\l`               | List all databases                                       |
| `\d+`              | Show detailed information about various database objects |
| `\dt`              | List all tables in the current database                  |
| `\du`              | List all users                                           |
| `\df`              | List all functions                                       |
| `\dv`              | List all views                                           |
| `\dn`              | List all schemas                                         |
| `\dp`              | List all permissions                                     |
| `\di`              | List all indexes                                         |
| `\ds`              | List all sequences                                       |
| `\d+`              | Show detailed information about various database objects |
| `\q`               | Quit psql                                                |
| `\x`               | Toggle expanded output                                   |

## Backup and Restore

| Command                           | Description                    |
| --------------------------------- | ------------------------------ |
| `pg_dump <database> > backup.sql` | Backup a database to a file    |
| `psql <database> < backup.sql`    | Restore a database from a file |

## Examples

Dump multiple tables from a db running on docker:

```bash
docker exec -t CONTAINER pg_dump -U DB_USER -d DB --table=T1 --table=T2 > tables.sql
```

Then restore them:

```bash
cat tables.sql | docker exec -i CONTAINER psql -U DB_USER -d DB
```

Dump multiple tables from a db running on k8s:

```bash
k exec -it postgresql-0 -- pg_dump "postgresql://DB_USER:DB_PASSWD@127.0.0.1:5432/DB_NAME" --table=T1 --table=T2 > tables.sql
```

## Create New User and New DBs with Permissions

I'll guide you through the process of creating a new user in PostgreSQL, associating a database with that user, and granting the necessary permissions. Here are the steps you should follow:

1 Connect to PostgreSQL as a superuser (usually 'postgres'):

```bash
psql -U postgres
```

2 Create a new user (replace 'newuser' with your desired username):

```bash
CREATE USER newuser WITH PASSWORD 'your_password';
```

3 Create a new database and make the new user the owner:

```bash
CREATE DATABASE newdb WITH OWNER newuser;
```

4 Grant all privileges on the new database to the new user:

```bash
GRANT ALL PRIVILEGES ON DATABASE newdb TO newuser;
```

5 Connect to the new database:

```bash
\c newdb
```

6 Grant schema usage and create permissions to the new user:

```bash
GRANT USAGE, CREATE ON SCHEMA public TO newuser;
```

7 Grant all privileges on all tables in the public schema to the new user:

```bash
GRANT ALL PRIVILEGES ON ALL TABLES IN SCHEMA public TO newuser;
```

8 Grant all privileges on all sequences in the public schema to the new user:

```bash
GRANT ALL PRIVILEGES ON ALL SEQUENCES IN SCHEMA public TO newuser;
```

9 Set the default privileges for the new user to be able to create tables and run migrations:

```bash
ALTER DEFAULT PRIVILEGES FOR USER newuser IN SCHEMA public
 GRANT ALL ON TABLES TO newuser;
```

```bash
ALTER DEFAULT PRIVILEGES FOR USER newuser IN SCHEMA public
 GRANT ALL ON SEQUENCES TO newuser;
```

These steps will create a new user with the ability to create tables and run migrations on the associated database. The user will have full rights on the 'newdb' database and all its objects.
