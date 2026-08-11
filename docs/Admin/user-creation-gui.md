# User Management Using MATE User Manager

## 1. Overview

**MATE User Manager (`mate-user-manager`)** is a graphical tool used to create and manage local user accounts.

This guide explains how to create a user using the available fields in MATE User Manager.

The user creation form contains the following fields:

- **Username**

- **Full Name**

- **Account Type**

- **Password**


---

# 2. Launch MATE User Manager

Launch **MATE User Manager** from the system application menu.

Alternatively, open a terminal and run:

```bash
mate-user-manager
```

If prompted, provide the required administrator credentials.
![mate-user-startup](../image/mate-user-manager-start-menu.png)



![](../image/mate-user-window.png)


---

# 3. Create a New User

To create a new user:

1. Open **MATE User Manager**.
    
2. Select the option to **Add** or **Create** a user.
    
3. Enter the required user information.
    
4. Select the appropriate account type.
    
5. Enter and confirm the password.
    
6. Review the information.
    
7. Save or create the user.
    

**[Screenshot 2: Create User window]**

---

# 4. User Parameters

The user creation screen contains the following parameters.

|Parameter|Example|Description|
|---|---|---|
|**Username**|`shavak`|Unique name used to identify the user account.|
|**Full Name**|`Shavak Shavak`|Full name associated with the user account.|
|**Account Type**|`Standard User`|Determines the type of account and associated privileges.|
|**Password**|User-defined|Password used to authenticate the user.|

---

# 5. Username

The **Username** identifies the user account on the system.

For this example, enter:

```text
shavak
```

### Requirements

- The username must be unique.
    
- Do not use a username that already exists.
    
- Use the naming convention defined by your organization.
    

**[Screenshot 3: Username field]**

---

# 6. Full Name

The **Full Name** field identifies the person associated with the account.

For this example, enter:

```text
Shavak Shavak
```

**[Screenshot 4: Full Name field]**

The full name can be displayed by the system when identifying the user.

---

# 7. Account Type

The **Account Type** determines the type of account being created.

Select the appropriate account type based on the user's responsibilities.

For this example:

```text
Standard User
```

Possible account types displayed by the system may vary depending on the Linux distribution and MATE User Manager configuration.

**[Screenshot 5: Account Type selection]**

### Standard User

A standard user should be used for normal day-to-day activities without unnecessary administrative privileges.

### Administrator

If an administrator account is available, use it only when the user requires administrative privileges.

> **Security Recommendation:** Follow the principle of least privilege and assign administrator privileges only when required.

---

# 8. Password

Enter a password for the user account.

For security, the password should comply with the configured system password policy.

### Password Requirements

The password should:

- Contain at least **8 characters**.
    
- Include uppercase characters.
    
- Include lowercase characters.
    
- Include numbers.
    
- Include special characters.
    

**[Screenshot 6: Password fields]**

> **Note:** The actual password requirements may be enforced by the system's password policy. Follow the password requirements displayed by the application.

---

# 9. Complete User Creation Example

For the example user `shavak`, enter the following information:

|Field|Value|
|---|---|
|**Username**|`shavak`|
|**Full Name**|`Shavak Shavak`|
|**Account Type**|`Standard User`|
|**Password**|Enter a password that meets the password policy|

### Procedure

1. Enter `shavak` in the **Username** field.
    
2. Enter `Shavak Shavak` in the **Full Name** field.
    
3. Select **Standard User** under **Account Type**.
    
4. Enter the user's password.
    
5. Confirm the password if a confirmation field is provided.
    
6. Review the entered information.
    
7. Click **Create**, **Add**, **Save**, or the equivalent button.
    

**[Screenshot 7: Completed Create User form]**

---

# 10. User Creation Result

After the user is successfully created, the `shavak` account should appear in the user list.

The resulting configuration is:

```text
Username:      shavak
Full Name:     Shavak Shavak
Account Type:  Standard User
Password:      Configured
```

**[Screenshot 8: User displayed in user list]**

---

# 11. Groups

Groups are used to organize users and manage access to system resources.

If the version of MATE User Manager being used provides group management, groups can be managed separately from the basic user creation form.

For example:

```text
developers
engineering
project-team
```

The `shavak` user can be assigned to the required groups according to the organization's access requirements.

> **Note:** If group assignment is not available in the user creation screen, group membership must be configured using the available group-management interface or another supported system administration method.

---

# 12. Modifying a User

To modify an existing user:

1. Open **MATE User Manager**.
    
2. Select the user.
    
3. Open the user settings or properties.
    
4. Modify the required information.
    
5. Save or apply the changes.
    

Depending on the version, available settings may include:

- Username.
    
- Full Name.
    
- Account Type.
    
- Password.
    

**[Screenshot 9: User modification screen]**

---

# 13. Changing a User Password

To change an existing user's password:

1. Select the user.
    
2. Open the user settings.
    
3. Enter the new password.
    
4. Confirm the password if required.
    
5. Apply the changes.
    

**[Screenshot 10: Change password]**

Ensure that the new password complies with the configured password policy.

---

# 14. Deleting a User

To delete a user:

1. Select the user from the user list.
    
2. Select **Delete** or the equivalent option.
    
3. Review the confirmation message.
    
4. Confirm the deletion.
    
5. Authenticate if prompted.
    

**[Screenshot 11: Delete user confirmation]**

> **Warning:** Deleting a user can affect the user's files, permissions, and access to system resources. Verify that the account is no longer required before deleting it.

---

# 15. Verification

After creating the user, verify that the account appears in MATE User Manager.

For the `shavak` example, verify:

|Parameter|Expected Value|
|---|---|
|Username|`shavak`|
|Full Name|`Shavak Shavak`|
|Account Type|`Standard User`|
|Password|Configured|

The account can also be verified from the command line:

```bash
id shavak
```

To view the user's account information:

```bash
getent passwd shavak
```

---

# 16. Troubleshooting

## Username Already Exists

If the username cannot be created, verify that another account with the same username does not already exist.

```bash
id shavak
```

## Password Rejected

If the password is rejected, ensure that it complies with the system password policy.

## Account Type Cannot Be Selected

Verify that you have the required administrative privileges and that the selected account type is supported by the installed version.

## User Is Not Created

Verify that:

- All required fields are completed.
    
- The username is unique.
    
- The password meets the password policy.
    
- You have sufficient administrative privileges.
    

---

# 17. Summary

Creating a user with MATE User Manager requires the following information:

1. **Username** — Enter a unique username.
    
2. **Full Name** — Enter the user's full name.
    
3. **Account Type** — Select the appropriate account type.
    
4. **Password** — Enter a password that meets the configured password policy.
    
5. **Create/Save** — Save the user configuration.
    

### Quick Example

```text
Username:      shavak
Full Name:     Shavak Shavak
Account Type:  Standard User
Password:      Configured according to password policy
```

After creation, verify that the user appears in the MATE User Manager user list and that the account has the correct account type and access.