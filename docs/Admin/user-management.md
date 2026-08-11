## User Management
This section describes the methods to create user and user groups using GUI and CLI.

### User, Group and Quota Management using Command Line	
This section describes steps to add and manage a user or user group through command line interface.

### Environment Variables	

Environment variables are values that are visible to all of the software running on a computer. These are often used to tell the operating system how it should behave, and to point software packages to the required directory location to find important files.

To view the environment variables:

- Login to your Linux account and type the command env. This shows a list of all the environment variables that your account currently sees.

- Some are found in all Linux systems, some are specific to the bash shell, and some are specific to a given computer program. The following table lists a selection of the environment variables that are amongst the most important ones for account configuration.

- Some environment variables are redundant. For example, the variables LIBRARY_PATH, LD_LIBRARY_PATH, LIBPATH, and SHLIB_PATH point the operating system to static libraries and shared object files (so files are dynamic linked libraries, equivalent to .dll files in Windows).

- There are multiple environment variables doing the same job because some are used by different shells, or Linux distributions. Since different programs look at different ones, a redundant configuration keeps all of the programs finding the paths to the libraries.

The value of an environment variable can be displayed with the echo command. For example, the PATH environment variable tells the operating system where to look for programs to run. You can see where the run script program resides by typing which run_script.

Table 3 - Environment Variables

| Variable                     | Definition |
|-------------------------------|-----------|
| CLASSPATH                     | Java programs uses this to find their libraries |
| DISPLAY                       | Tells X Windows where to display graphics |
| HISTSIZE                      | Number of commands displayed by the history command |
| HOME                          | Your home directory |
| HOST, HOSTNAME                | The computer (or cluster node) you are logged in |
| INCLUDEDIR, INCLUDE           | Paths to header files |
| LD_LIBRARY_PATH, LIBRARY_PATH, LIBPATH, SHLIB_PATH | Paths to static linked and dynamic linked libraries |
| LS_COLORS                     | Allows customizing colors used by the ls command |
| MANPATH                       | Paths to data for the man command |
| PATH                          | Paths to find executable files |
| PS1                           | Changes the bash command prompt |
| PWD                           | Current working directory |
| TERM                          | Terminal display settings |
| USER, LOGNAME                 | User name |




Use the following run_script command to see all of the directories that the operating system is looking for.

``` echo $PATH	```

You can set new environment variables, or add data to existing environment variables. For example, you may want to create some of your own programs and scripts. In order to find specific when you run them, you can put them in a new sub-directory, typically


named /home/MYNAME/bin. In order to tell the operating system to look for your programs in this directory, you could add a line into the .bashrc.local file. For example:

``` export PATH="$PATH:/home/MYNAME/bin"	```

Note that by including $PATH: in the new value of PATH, you are appending a new directory onto the existing path list. The directory names are separated by colons. If you leave out this $PATH: part of the line you would be taking away all of the paths to the operating system commands, thus breaking most of the functionality of your account.

Environment variables can be used in shell scripts. For example, if you want a shell script to create a directory with your user name, you can use the following line:

For example:

``` mkdir /scratch/$USER	```

Environment variables are accessible within most compiled computer languages. There is a mechanism for accessing them.

Note: Some of variables have been exported and can be found in /etc/bashrc file
