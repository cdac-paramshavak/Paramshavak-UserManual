# Additional Linux Commands

This chapter provides information on additional Linux commands that can be used for PARAM Shavak


## The uptime Command
In Linux, the uptime command shows how long the system is running and the number of users that are currently logged in. It also displays load average for 1, 5 and 15 minutes intervals.

<img src="/img/img20.png" alt="alt">

## The w Command
The w command displays users currently logged in and their process along-with shows load averages. It also shows the login name, tty name, remote host, login time, idle time, JCPU, PCPU, command and processes.

<img src="/img/img21.png" alt="alt">

Following is a list of available options:

-h: Displays no header entries.
-s: Without JCPU and PCPU.
-f: Removes from field.
-V: (upper letter) – Shows versions.


## The users Command
The users command displays currently logged in users. This command does not have parameters other than help and version.
<img src="/img/img22.png" alt="alt">


## The who Command
The who command simply returns user name, date, time and host information. The who command is similar to w command. Unlike w, the who command does not print what users are doing. Let’s illustrate and see the difference between who and w commands.
<img src="/img/img23.png" alt="alt">

Following is a list of the who command Options:

-b: Displays last system reboot date and time.
-r: Shows current runlet.
-a, –all: Displays all information cumulatively.


## The whoami Command
The whoami command prints the name of the current user. You can also use the whoami command to display the current user. If you are logged in as a root using the sudo command, the whoami command returns root as current user. Use the whoami command if you want to know the exact user logged in.
<img src="/img/img24.png" alt="alt">


## The ls Command
The ls command displays list of files in human readable format.
<img src="/img/img25.png" alt="alt">

Sort file as per last modified time.
<img src="/img/img26.png" alt="alt">


## The crontab Command
List schedule jobs for current user with the crontab command and -l option.
<img src="/img/img27.png" alt="alt">

Edit the crontab with the -e option. The following example opens schedule jobs in VI editor. Make necessary changes and quit pressing the: wq keys which saves the setting automatically.

``` crontab -e ```



## The less Command
The less command allows viewing the file promptly. You can do page up and down. Press q to quit from fewer windows.

<img src="/img/img28.png" alt="alt">

<img src="/img/img29.png" alt="alt">




## The more Command
The more command allows to quickly view file and shows details in percentage. You can do page up and down. Press q to quit out from more windows.

<img src="/img/img30.png" alt="alt">

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

You can combine more and less command with cat command to view file content if that does not fit in single screen / page.

<img src="/img/img31.png" alt="alt">

## The cd Command (change directory)
The cd command (change directory) takes you to the fileA directory.

``` cd /fileA	```


## The pwd Command (print working directory)
The pwd command return with present working directory.

<img src="/img/img32.png" alt="alt">

## The sort Command
Sorting lines of text files in ascending order. You can use the -r options to sort in descending order.

<img src="/img/img33.png" alt="alt">

## The vi Command
vi is the most popular text editor available in most of the UNIX-like OS. Following examples open file in read only with -R option. Press: q to quit from the vi window.

``` vi -R /etc/shadows	```


## The ssh Command (Secure Shell)
The ssh command is used to login into remote host. For example, the following ssh
command connects to remote host (192.168.1.1) using user as narad.

``` ssh narad@192.168.1.1	```


## The ftp and sftp Commands
The ftp or sftp commands are used to connect to remote host.ftp is (file transfer protocol) and sftp is (secure file transfer protocol). For example the following command connects to ftp host (192.168.50.2).
<img src="/img/img34.png" alt="alt">

Putting multiple files in remote host with mput similarly you can do mget to download multiple files from remote host.

<img src="/img/img35.png" alt="alt">

## The service Command
The service command calls the script located at /etc/init.d/ directory and executes the script. There are two ways to start any service. For example, you start the service called httpd with the following service command.

``` service httpd start	```

or

``` /etc/init.d/httpd start	```


## The free command
The free command shows free, total and swap memory information in bytes.

<img src="/img/img36.png" alt="alt">




The free command with -t options shows total memory used and available memory in bytes.

<img src="/img/img37.png" alt="alt">




## The top Command
The top command displays processor activity of the system and also displays tasks managed by kernel in real-time. It shows details of the processor and memory that are being used. Use the top command with u option. This displays specific user process details as follows. Press O (uppercase letter) to sort as desired by you. Press q to quit from top screen.
<img src="/img/img38.png" alt="alt">





## The tar Command
The tar command is used to compress files and folders in Linux. For example the following command creates an archive for /home directory with file name as archive- name.tar.

``` tar -cvf archive-name.tar /home	```

To extract tar archive file, use the option as follows.

``` tar –xvf archive-name.tar	```


## The grep Command
The grep command searches for a given string in a file. Only test123 user displays from /etc/passwd file. You can use the -i option for ignoring case sensitive.
<img src="/img/img39.png" alt="alt">


## The find Command
The find command used to search files, strings and directories. test123 word in ‘/’ partition and return the output.
<img src="/img/img40.png" alt="alt">

## The lsof Command
The lsof command means list of all open files. Following is a list of the lsof
commands to open files by user test123.

<img src="/img/img41.png" alt="alt">



## The last command
With the last command you can watch the user’s activity in the system. This command can execute normal user also. It displays complete user’s info such as terminal, time, date, system, re-booter, boot, and kernel version. It is a useful command for troubleshooting.

<img src="/img/img42.png" alt="alt">

<img src="/img/img43.png" alt="alt">




You can use last with username to know for specific user’s activity as follows.
<img src="/img/img44.png" alt="alt">


## The ps command
The ps command displays the details of the processes running in the system. Following example, show test123 only.
<img src="/img/img45.png" alt="alt">


## The kill command
Use the kill command to terminate a process. First find the process id using the ps
command as follows and kill the process with kill -9 command.

<img src="/img/img46.png" alt="alt">



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

grep pattern files – search for pattern in files

grep -r pattern dir – search recursively for pattern in dir

command | grep pattern – search for pattern in the output of command

locate file – find all instances of file

### System Info

date – show the current date and time

cal – show this month's calendar

uptime	– show current uptime

w – display who is online

whoami– who you are logged in as


finger user– display information about user

uname -a – show kernel information

cat /proc/cpuinfo – cpu information

cat /proc/meminfo – memory information

man command– show the manual for command

df – show disk usage

du – show directory space usage

free – show memory and swap usage

whereis app – show possible locations of app

which app – show which app will be run by default

### Compression

tar cf file.tar files – create a tar named file.tar containing files

tar xf file.tar – extract the files from file.tar

tar czf file.tar.gz files – create a tar with Gzip compression

tar xzf file.tar.gz – extract a tar using Gzip

tar cjf file.tar.bz2 – create a tar with Bzip2 compression

tar xjf file.tar.bz2 – extract a tar using Bzip2

gzip file – compresses file and renames it to file.gz gzip -d file.gz – decompresses file.gz back to file Network
ping host – ping host and output results

whois domain – get whois information for domain

dig domain – get DNS information for domain

dig -x host– reverse lookup host

wget file – download file


wget -c file – continue a stopped download

### Shortcuts

Ctrl+C – halts the current command

Ctrl+Z– stops the current command, resume with fg in the foreground or bg in the background

Ctrl+D – log out of current session, similar to exit

Ctrl+W – erases one word in the current line

Ctrl+U – erases the whole line

Ctrl+R – type to bring up a recent command

!! - repeats the last command

exit – log out of current session

