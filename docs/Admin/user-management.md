## User Management
This section describes the methods to create user and user groups using GUI and CLI.

### User, Group and Quota Management using Command Line	
This section describes steps to add and manage a user or user group through command line interface.

### Adding a New User	

To add a user to the system:

- Issue the useradd command to create a locked user account:
- useradd<username>
- Unlock the account by issuing the passwd command to assign a password and set password aging guidelines:

- passwd<username>

| Option       | Description |
|-------------|-------------|
| **-c <comment>**   | <comment> can be replaced with any string. This option is generally used to specify the full name of a user. |
| **-d <home-dir>**  | Home directory to be used instead of default `/home/<username>/` |
| **-e <date>**      | Date for the account to be disabled in the format YYYY-MM-DD |
| **-f <days>**      | Number of days after the password expires until the account is disabled. If 0 is specified, the account is disabled immediately after the password expires. If -1 is specified, the account is not to be disabled after the password expires. |
| **-g <group-name>** | Group name or group number for the user's default group. The group must exist prior to being specified here. |
| **-G <group-list>** | List of additional (other than default) group names or group numbers, separated by commas, of which the user is a member. The groups must exist prior to being specified here. |
| **-m**            | Create the home directory if it does not exist. |
| **-M**            | Do not create the home directory. |
| **-n**            | Do not create a user private group for the user. |
| **-r**            | Create a system account with a UID less than 500 and without a home directory |
| **-p <password>**  | The password encrypted with crypt |
| **-s**            | User's login shell, which defaults to `/bin/bash` |
| **-u <uid>**       | User ID for the user, which must be unique and greater than 499 |


Note: The password must be of 8 characters. It should combination of alphabets, numbers and special characters. You must include at least one upper case character and one lower case character.


### Adding a Group	

To add a group to the system, use the following command.

- groupadd<group-name>

| Option       | Description |
|-------------|-------------|
| **-g <gid>**  | Group ID for the group, which must be unique and greater than 499 |
| **-r**        | Create a system group with a GID less than 500. When used with `-g <gid>` and `<gid>` already exists, `groupadd` will choose another unique GID for the group. |
| **-f**        | Another unique `<gid>` for the group. |
`


## User and Group Management using GUI	

The User Manager allows you to view, modify, add, and delete local users and groups. To use the User Manager, the following conditions must be met:

- You must be running the X Window System

- Have root privileges

- The system-config-users RPM package must be installed.

To start the User Manager from the desktop:

- Click System (on the panel) >Administration>Users & Groups.

Note: You can also type the command system-config-users at a shell prompt (for example, in an XTerm or a GNOME terminal).



<img src="/img/img13.png" alt="alt">
<p style="text-align: center;">Figure 7- User Manager</p>


- To view a list of local users on the system, click the Users tab.

- To view a list of local groups on the system, click the Groups tab.

- To find a specific user or group, type the first few letters of the name in the Search filter field. Press Enter or click the Apply filter but- ton. The filtered list is displayed.


- To sort the users or groups, click on the column name. The users or groups are sorted according to the value of that column.

- Red Hat Enterprise Linux reserves user IDs below 500 for system users. By default, User Manager does not display system users. To view all users, including the system users, go to Edit >Preferences and uncheck Hide system users and groups from the dialog box.


 Type the password in the Password and Confirm Password fields. The password must be at least six characters.

Note: The password must be of 8 characters. It should combination of alphabets, numbers and special characters. You must include at least one upper case character and one lower case character.

- Select a login shell. If you are not sure which shell to select, accept the default value of /bin/bash. The default home directory is /home/<username>/. You can change the home directory that is created for the user, or you may choose not to create the home directory by unselecting Create home directory.

Note: If you select to create the home directory, default configuration files are copied from the /etc/skel/directory into the new home directory.
Red Hat Enterprise Linux uses the user private group (UPG) scheme. The UPG scheme does not add or change anything in the standard UNIX way of handling groups; it offers


a new convention. Whenever you create a new user, by default, a unique group with the same name as the user is created. If you do not want to create this group, unselect Create a private group for the user.


### Adding a New User	

To add a new user:

- Click the Add User button. A window as shown in the Create New User figure appears.


<img src="/img/img14.png" alt="alt">
<p style="text-align: center;">Figure 8 - Create New User Window</p>
