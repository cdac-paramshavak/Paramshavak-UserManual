# Additional Linux Commands

This chapter provides information on additional Linux commands that can be used for PARAM Shavak


## The uptime Command
In Linux, the uptime command shows how long the system is running and the number of users that are currently logged in. It also displays load average for 1, 5 and 15 minutes intervals.

 ```uptime``` 

 ``13:39:21 up 5 days,  2:17,  3 users,  load average: 0.01, 0.01, 0.00``


## The w Command
The w command displays users currently logged in and their process along-with shows load averages. It also shows the login name, tty name, remote host, login time, idle time, JCPU, PCPU, command and processes.

 ```#w```

 ```13:38:57 up 5 days,  2:17,  3 users,  load average: 0.01, 0.01, 0.00``

```USER     TTY        LOGIN@   IDLE   JCPU   PCPU WHAT```

```admin    seat0     Thu11    0.00s  0.00s  0.00s /usr/libexec/gdm-wayland-session``` ```--register-session gnome-session```

``` admin    tty2      Thu11    5days  0.02s  0.02s /usr/libexec/gnome-session-binary```

``` root     pts/1     13:38    1.00s  0.01s  0.01s w```

Following is a list of available options:

-h: Displays no header entries.
-s: Without JCPU and PCPU.
-f: Removes from field.
-V: (upper letter) – Shows versions.


## The users Command
The users command displays currently logged in users. This command does not have parameters other than help and version.

``` # users ```

```admin admin root```

## The who Command
The who command simply returns user name, date, time and host information. The who command is similar to w command. Unlike w, the who command does not print what users are doing. Let’s illustrate and see the difference between who and w commands.

``#who`` 

``admin    seat0        2026-08-06 11:24 (login screen)``

``admin    tty2         2026-08-06 11:24 (tty2)``

``root     pts/1        2026-08-11 13:38 (10.208.55.129)``

Following is a list of the who command Options:

-b: Displays last system reboot date and time.
-r: Shows current runlet.
-a, –all: Displays all information cumulatively.


## The whoami Command
The whoami command prints the name of the current user. You can also use the whoami command to display the current user. If you are logged in as a root using the sudo command, the whoami command returns root as current user. Use the whoami command if you want to know the exact user logged in.

``# whoami ``

``admin``




## The cp Command
The cp command copies file from source to destination preserving same mode.

``` cp -p fileA fileB ```

You will be prompted before overwriting any file.

``` cp -i fileA fileB ```

## The mv Command
Rename fileA to fileB. The -i option prompts before overwrite. Asks for confirmation if exist already.

``` mv -i fileA fileB ```

## The cat Command
The cat command used to view multiple file at the same time.

``` cat fileA fileB ```



## The rm command
The rm command is used to remove or delete a file without prompting for confirmation.
``` rm filename  ```

Use the -i option to get confirmation before removing it. Using the options -r and -f
removes the file forcefully without confirmation.


Note: Do not use this command until or unless you are sure what you are doing.

``` rm -i test.txt ```


rm: remove regular file `test.txt'?	


## The mkdir command
The mkdir command is used to create directories under Linux.

``` mkdir directoryname	```

### File Commands

```ls``` – directory listing

```ls -al```	– formatted listing with hidden file

```cd dir``` - change directory to dir

```cd``` – change to home

```pwd``` – show current directory

```mkdirdir``` – create a directory dir

```rm file``` – delete file

```rm -r dir``` – delete directory dir

```rm -f file``` – force remove file

```rm -rfdir``` – force remove directory dir

```cp file1 file2``` – copy file1 to file2

```cp -r dir1 dir2``` – copy dir1 to dir2; create dir2 if it doesn't exist

```mv file1 file2``` – rename or move file1 to file2 if file2 is an existing directory, moves file1 into directory file2

```ln -s file link``` – create a symbolic link link to a file

```touch file``` – create or update file

```cat > file``` – places standard input into file

```more file``` – output the contents of file

```head file``` – output the first 10 lines of file

```tail file``` – output the last 10 lines of file


```tail -f file``` – output the contents of file as it grows, starting with the last 10 lines

### Process Management

```ps``` – display your currently active processes

```top``` – display all running processes

```kill pid``` – kill process id pid

```killallproc``` – kill all processes named proc *

```bg ```– lists stopped or background jobs; resume a stopped job in the background

```fg ```– brings the most recent job to foreground

### ssh

```ssh user@host``` – connect to host as user

```ssh -p port user@host``` – connect to host on port

```ssh-copy-id user@host ```– add your key to host for user to enable a keyed or password less login

Searching

``` grep ``` pattern files – search for pattern in files

``` grep -r pattern dir``` – search recursively for pattern in dir

```` grep pattern ``` – search for pattern in the output of command

``` locate file ``` – find all instances of file

### System Info

```date``` – show the current date and time

```cal``` – show this month's calendar

```uptime```	– show current uptime


```finger user```– display information about user

```uname -a``` – show kernel information

```cat /proc/cpuinfo``` – cpu information

```cat /proc/meminfo ```– memory information

```man ```command– show the manual for command

```df ```– show disk usage

```du ```– show directory space usage

```free ```– show memory and swap usage

```whereis app``` – show possible locations of app

```which app ```– show which app will be run by default

### Compression

```tar cf file.tar ```files – create a tar named file.tar containing files

```tar xf file.tar ```– extract the files from file.tar

```tar czf file.tar.gz ```files – create a tar with Gzip compression

```tar xzf file.tar.gz``` – extract a tar using Gzip

```tar cjf file.tar.bz2 ```– create a tar with Bzip2 compression

```tar xjf file.tar.bz2``` – extract a tar using Bzip2

```gzip file``` – compresses file and renames it to file.gz gzip -d file.gz – decompresses file.gz back to file Network
```ping host``` – ping host and output results

```whois domain``` – get whois information for domain

``` dig domain ```– get DNS information for domain

```wget file``` – download file


```wget -c file ```– continue a stopped download

```exit – ```log out of current session

### Shortcuts

Ctrl+C – halts the current command

Ctrl+Z– stops the current command, resume with fg in the foreground or bg in the background

Ctrl+D – log out of current session, similar to exit

Ctrl+W – erases one word in the current line

Ctrl+U – erases the whole line

Ctrl+R – type to bring up a recent command

!! - repeats the last command

