# Users in Linux

## Users

Different kinds of users in Linux:

- **Root User**: The superuser account, which has the highest level of access and privileges.
  - ID: 0
  - There is only one root user in the system.
- Regular Users: Normal users who have limited access and privileges.
  - ID: 1 to 65534
  - We can allow regular users to execute certain commands as root using `sudo`.
- Service Users: Users created for running services.
  - They run only specific services and do not have login access.
  - This allow tu safely run services without giving them root access.

## Groups

All users belong to a primary group and can be part of multiple secondary groups.

## Managing Users

### Locating User Information

Stored in various files:

- `/etc/passwd`: Contains user account information.
  - Username, User ID, Group ID, Home Directory, Shell.
- `/etc/shadow`: Stored encrypted passwords and aging information
  - Only accessible by root user
- `/etc/group`
  - Contains information about the groups and their members
  - Readable by all users

```bash
cat /etc/passwd
sudo cat /etc/shadow
```

### Examples

#### Add new user

`useradd` main args:

- `-m`: create home directory
- `-d`: set custom home directory
- `-s`: specify default shell
- `-g`: specify primary group instead of default config

```bash
sudo useradd -m -d /home/new-user new-user
```

#### Set password for a user

Can allow user to change their password or create one if no password set.

`passwd` main args:

- `-S`: show password status for a given user
- `-d`: delete password
- `-l`: lock account
- `-u`: unlock account
- `-e`: expire password
- `-n`: set minimum days before password change
- `-x`: set maximum days before password change

```bash
passwd -S
sudo passwd -S ANOTHER_USER
```

#### Modify User details

`usermod` main args:

- `-c`: change user description
- `-s`: change default shell
- `-d`: change home directory (dangerous)
- `-l`: change username
- `-g`: change primary group
- `-G`: change secondary group
- `-aG`: add secondary group
