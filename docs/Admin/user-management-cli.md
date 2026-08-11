## User Management - CLI

This section provides system administrators with a command-line reference for managing existing Linux user accounts.

---
## Viewing User Information
## Check User Details

Use the `id` command to display the user's UID, primary group, and supplementary groups.

```
id username
```

Example:

```
id john
```

Example output:

```
uid=1001(john) gid=1001(john) groups=1001(john),1002(developers)
```
## View User Account Information

Use `getent` to retrieve the user's account information.

```
getent passwd username
```

Example:

```
getent passwd john
```

The output contains:

```
username:x:UID:GID:comment:home-directory:login-shell
```

---

## Managing User Groups

Groups are used to control access to files, directories, applications, and system resources.

## Add User to a Group

```
sudo usermod -aG groupname username
```

Example:

```
sudo usermod -aG developers john
```

Verify:

```
id john
```

> **Important:** Always use `-aG` when adding a supplementary group. Omitting `-a` can replace the user's existing supplementary group memberships.

## Remove User from a Group

```
sudo gpasswd -d username groupname
```

Example:

```
sudo gpasswd -d john developers
```

Verify:

```
groups john
```

## Change the Primary Group

```
sudo usermod -g groupname username
```

Example:

```
sudo usermod -g developers john
```

Verify:

```
id john
```

---

## Password Management
## Change User Password

```
sudo passwd username
```

Example:

```
sudo passwd john
```

The administrator will be prompted to enter the new password.


## Check Password Status

```
sudo passwd -S username
```

Example:

```
sudo passwd -S john
```

This can be used to determine whether the password is active, locked, or otherwise restricted.

## Force Password Change at Next Login

```
sudo chage -d 0 username
```

Example:

```
sudo chage -d 0 john
```

## View Password Aging Information

```
sudo chage -l username
```

Example:

```
sudo chage -l john
```

## Set Maximum Password Age

```
sudo chage -M 90 username
```

Example:

```
sudo chage -M 90 john
```

This sets the maximum password age to 90 days.

---

## Locking and Unlocking User Accounts
## Lock a User Account

```
sudo passwd -l username
```

Example:

```
sudo passwd -l john
```

An account may be locked when access needs to be temporarily disabled.

## Unlock a User Account

```
sudo passwd -u username
```

Example:

```
sudo passwd -u john
```

Verify:

```
sudo passwd -S john
```

> **Note:** Locking a password does not necessarily disable every possible authentication mechanism. Consider SSH keys, service accounts, and other authentication methods when disabling access.

---
## Account Expiration
## View Account Expiration

```
sudo chage -l username
```

## Set an Account Expiration Date

```
sudo usermod -e YYYY-MM-DD username
```

Example:

```
sudo usermod -e 2026-12-31 john
```

## Remove Account Expiration

```
sudo usermod -e "" username
```

Example:

```
sudo usermod -e "" john
```

---

## Modifying User Account Properties
## Change Login Shell

```
sudo usermod -s /bin/bash username
```

Example:

```
sudo usermod -s /bin/bash john
```

To prevent interactive login where appropriate:

```
sudo usermod -s /usr/sbin/nologin username
```

---

## Change User Home Directory

```
sudo usermod -d /new/home/path username
```

To move the existing home directory:

```
sudo usermod -d /new/home/path -m username
```

> **Warning:** Verify application dependencies and file ownership before moving a user's home directory.

---

## Change User Description

```
sudo usermod -c "John Doe - IT Administrator" john
```

Verify:

```
getent passwd john
```

---

## Managing User Privileges

User privileges should follow the principle of least privilege.
## Check Sudo Privileges

```
sudo -l -U username
```

Example:

```
sudo -l -U john
```

This displays the commands and permissions available to the user through `sudo`.

---

## Removing a User Account

User deletion should only be performed after the account owner and required data have been reviewed.

## Delete the User Account

```
sudo userdel username
```

## Delete the User and Home Directory

```
sudo userdel -r username
```

> **Warning:** The `-r` option can remove the user's home directory and associated local mail spool. Confirm that required data has been backed up or transferred before using it.

Before deletion, identify files owned by the account:

```
sudo find / -user username -ls 2>/dev/null
```

