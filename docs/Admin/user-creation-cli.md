# User and Group Management - CLI

This section describes how to create and configure users and groups using the command-line interface (CLI).

## Prerequisites

Before creating a user, ensure that:

- You have the required administrative privileges.

- The username is unique.

- The required groups already exist.

- The UID and GID values are unique when specified manually.

- The user's password meets the configured password policy.


---

## Adding a User

Use the `useradd` command to create a user account.

### Syntax

```bash
useradd [options] <username>
```

### Example

The following command creates a user named `shavak` and creates the user's home directory:

```bash
useradd -m shavak
```

The user account is created in a locked state until a password is assigned.

---

## User Information

When creating a user, collect or configure the following information:

| Field                  | Description                                                             | Example                    |
| ---------------------- | ----------------------------------------------------------------------- | -------------------------- |
| **Username**           | Unique name used to identify and log in to the account.                 | `shavak`                   |
| **First Name**         | User's first name.                                                      | `Shavak`                   |
| **Last Name**          | User's last name.                                                       | `Patel`                    |
| **Full Name**          | Complete name of the user. This can be specified using the `-c` option. | `Shavak Patel`             |
| **Email**              | Email address associated with the user account.                         | `shavak@example.com`       |
| **User ID (UID)**      | Unique numeric identifier assigned to the user.                         | `1001`                     |
| **Default Group**      | Primary group assigned to the user.                                     | `developers`               |
| **Additional Groups**  | Other groups to which the user belongs.                                 | `engineering,project-team` |
| **Home Directory**     | Directory used as the user's home directory.                            | `/home/shavak`             |
| **Login Shell**        | Shell used when the user logs in.                                       | `/bin/bash`                |
| **Account Expiration** | Date on which the user account expires.                                 | `2027-12-31`               |
| **Password**           | Password used to authenticate the user.                                 | Configured using `passwd`  |

 The standard Linux `useradd` command does not provide a dedicated `--email` option. If your product stores email separately from the Linux account, configure the email through the appropriate product command or interface.

---

## ``useradd`` Options

The following options can be used when creating a user:

| Option            | Description                                                                                                                                                                                                                     |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `-c <comment>`    | Specifies a comment for the user account. This is generally used to specify the user's full name.                                                                                                                               |
| `-d <directory>`  | Specifies the user's home directory instead of the default `/home/<username>/`.                                                                                                                                                 |
| `-e <YYYY-MM-DD>` | Specifies the date on which the user account expires.                                                                                                                                                                           |
| `-f <days>`       | Specifies the number of days after password expiration before the account is disabled. `0` disables the account immediately after password expiration. `-1` prevents the account from being disabled after password expiration. |
| `-g <group>`      | Specifies the user's default group. The group must already exist.                                                                                                                                                               |
| `-G <groups>`     | Specifies additional groups for the user. Multiple groups must be separated by commas. The groups must already exist.                                                                                                           |
| `-m`              | Creates the user's home directory if it does not already exist.                                                                                                                                                                 |
| `-M`              | Prevents creation of the user's home directory.                                                                                                                                                                                 |
| `-n`              | Prevents creation of a private group for the user.                                                                                                                                                                              |
| `-r`              | Creates a system account.                                                                                                                                                                                                       |
| `-p <password>`   | Specifies an encrypted password for the user.                                                                                                                                                                                   |
| `-s <shell>`      | Specifies the user's login shell. The default is `/bin/bash`.                                                                                                                                                                   |
| `-u <uid>`        | Specifies the user's UID. The UID must be unique and meet the system's UID requirements.                                                                                                                                        |

---
## Adding a Group

Groups are used to organize users and manage access or permissions collectively.

Use the `groupadd` command to create a group.

### Syntax

```bash
groupadd [options] <groupname>
```

### Example

```bash
groupadd developers
```

This command creates a group named `developers`.

## `groupadd` Options

|Option|Description|
|---|---|
|`-g <gid>`|Specifies the GID for the group. The GID must be unique.|
|`-r`|Creates a system group with a system-reserved GID.|
|`-f`|Causes the command to exit successfully if the specified group already exists. If the specified GID is unavailable, a unique GID may be selected.|

---

## Assigning Groups to a User

A user can have one default group and multiple additional groups.

### Default Group

Use `-g` to specify the user's default group:

```bash
useradd -m -g developers shavak
```

In this example:

- **Username:** `shavak`
    
- **Home directory:** `/home/shavak/`
    
- **Default group:** `developers`
    

### Additional Groups

Use `-G` to assign additional groups:

```bash
useradd -m -g developers -G engineering,project-team shavak
```

The resulting configuration is:

|Setting|Value|
|---|---|
|Username|`shavak`|
|Home directory|`/home/shavak/`|
|Default group|`developers`|
|Additional groups|`engineering`, `project-team`|
|Login shell|`/bin/bash`|

> **Note:** The groups specified with `-g` and `-G` must exist before they can be assigned to the user.

---

## Setting the User Password

After creating the user, use the `passwd` command to assign a password and unlock the account.

### Syntax

```bash
passwd <username>
```

### Example

```bash
passwd shavak
```

Enter and confirm the password when prompted.

## Password Requirements

The password must:

- Contain at least **8 characters**.
    
- Contain **letters and numbers**.
    
- Contain **special characters**.
    
- Include at least **one uppercase character**.
    
- Include at least **one lowercase character**.
    

---

## Complete User Creation Example

The following example demonstrates how to create the groups, create the `shavak` user, assign group memberships, and configure the password.

### Step 1: Create the Groups

```bash
groupadd developers
groupadd engineering
groupadd project-team
```

### Step 2: Create the User

```bash
useradd -m \
  -c "Shavak Patel" \
  -g developers \
  -G engineering,project-team \
  -s /bin/bash \
  shavak
```

### Step 3: Set the Password

```bash
passwd shavak
```

### User Configuration

|Property|Value|
|---|---|
|Username|`shavak`|
|First Name|`Shavak`|
|Last Name|`Patel`|
|Email|`shavak@example.com`|
|Full Name|`Shavak Patel`|
|Home Directory|`/home/shavak/`|
|Default Group|`developers`|
|Additional Groups|`engineering`, `project-team`|
|Login Shell|`/bin/bash`|
|Password|Configured using `passwd`|

> **Important:** The email address shown above is an example user attribute. Standard `useradd` does not store an email address as a separate field. If your product has an email field, configure it using the product's supported user-management mechanism.

---

## Verifying the User

After creating the user, verify that the account exists:

```bash
id shavak
```

To verify the user's group memberships:

```bash
groups shavak
```

To view the user's account information:

```bash
getent passwd shavak
```

To verify the user's home directory:

```bash
ls -ld /home/shavak
```

---

## Common Issues

### Username Already Exists

Check whether the username already exists:

```bash
id shavak
```

### Group Does Not Exist

Create the group before assigning it to the user:

```bash
groupadd developers
```

### UID Already Exists

If you specify a UID using `-u`, ensure that the UID is not already assigned to another user.

### Home Directory Is Not Created

Use the `-m` option:

```bash
useradd -m shavak
```

### Password Does Not Meet Requirements

If the password is rejected, verify that it meets the configured password policy, including the required length, uppercase and lowercase characters, numbers, and special characters.

---

