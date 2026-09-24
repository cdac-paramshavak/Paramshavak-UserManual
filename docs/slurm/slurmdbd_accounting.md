# Slurmdbd Setup:

This guide walks you to a working Slurm accounting database, then shows how to create accounts and users and give them priorities with sacctmgr.


| Component |  Function |
|-----------|------------|
| `slurmctld` | The Slurm controller (the "brain") that schedules jobs. |
| `slurmd` | The daemon running on each compute node that executes jobs. |
| `slurmdbd` | The Slurm Database Daemon — the middleman that stores accounting data. |
| `MariaDB` | The SQL database where `slurmdbd` stores accounting information. |
| `munge` | Authentication service that allows Slurm daemons to trust each other. |
| `sacctmgr` | Command used to manage clusters, accounts, users, and QOS in the database. |
| `sacct` / `sshare` / `sprio` | Commands used to view job history, fair-share usage, and job priority. |


Install and prepare MariaDB


**Installation and starting the Database service :**

````bash

sudo dnf install -y mariadb-server mariadb
sudo systemctl enable --now mariadb
systemctl status mariadb

````

enable --now starts it immediately and on every reboot.

Create the database and user

!!! warning "The database name created should be added to the slurmdbd.conf file. Follows in the below steps"  

**Creating New Database For the slurm accounting :**

````bash
sudo mariadb


CREATE DATABASE IF NOT EXISTS slurm_acct_db;
CREATE USER IF NOT EXISTS 'slurm'@'localhost' IDENTIFIED BY 'Slurm_Acct_Db_2026x9Kq';
GRANT ALL PRIVILEGES ON slurm_acct_db.* TO 'slurm'@'localhost';
FLUSH PRIVILEGES;

````


**Verify the database creation :**

````bash
SHOW DATABASES;
SHOW GRANTS FOR 'slurm'@'localhost';
EXIT;
````

You should see slurm_acct_db in the list.

Query to setup the password for the Database :

ALTER USER 'slurm'@'localhost' IDENTIFIED BY 'NewPasswordHere';

!!! warning "Do not create tables (job_table, user_table, ...) yourself. slurmdbd builds the whole schema automatically on first start."  




Setup Slurmdbd : 


**Command:**

````bash

sudo dnf install -y slurm-slurmdbd

sudo chmod 600 /etc/slurm/slurmdbd.conf

ls -l /etc/slurm/slurmdbd.conf
## Output :
## -rw------- 1 root root 208 Jan 2 12:03 /etc/slurm/slurmdbd.conf

sudo vi /etc/slurm/slurmdbd.conf

````

Then Configuration File /etc/slurm/slurmdbd.conf should contain something like:

**Command:**

````bash 
AuthType=auth/munge
DbdHost=localhost

PidFile=/var/run/slurm/slurmdbd.pid

SlurmUser=root

StorageType=accounting_storage/mysql
StorageHost=localhost
StoragePort=3306
StorageUser=slurm
StoragePass=slurm@123
StorageLoc=slurm_acct_db # name the created database
````



**Enable few parameters in slurm.conf:**

````bash 
 # Replace/uncomment the lines in the configuration files
sudo vi /etc/slurm/slurmdbd.conf

 # Replace/uncomment the lines 


# JOB PRIORITY
PriorityWeightQOS=1000

# LOGGING AND ACCOUNTING
AccountingStorageType=accounting_storage/slurmdbd

JobAcctGatherType=jobacct_gather/linux
````



**Start slurmdbd:**

````bash 
sudo systemctl enable --now slurmdbd

systemctl restart slurmdbd
# restart the service 
systemctl status slurmdbd

````

Once the service is in Running state  Check the Tables are created :

**Command:**

````bash 
sudo mariadb -e "USE slurm_acct_db; SHOW TABLES;"

````
Slurmdbd Accounting Setup Done !

## Create the Linux users

A Slurm user must also be a Linux user

**User creation:**

````bash 
sudo useradd -m user1
sudo useradd -m user2
sudo useradd -m user3
# set passwords or SSH keys as your site requires
passwd user1

````

## Create accounts
Accounts are groups.


**Example account creation:**

````bash 
sudo sacctmgr -i add account physics   Description="Physics dept"   Organization="university"
sudo sacctmgr -i add account chemistry Description="Chemistry dept" Organization="university"
````

**Example account:**

````bash 
sacctmgr show account format=Account,Descr,Org
sacctmgr show assoc tree format=Cluster,Account,User
````

## Create the QOS levels and set QOS priority

A QOS (Quality of Service) is a named priority tier. A higher number means higher priority.

**Example Qos :**

````bash

# Background / scavenger work
sudo sacctmgr -i add qos low    Priority=10

# Urgent work, restricted so it cannot be abused
sudo sacctmgr -i add qos high   Priority=1000 MaxWall=04:00:00 MaxJobsPerUser=5 Flags=DenyOnLimit

# 'normal' exists already: just give it a priority
sudo sacctmgr -i modify qos where name=normal set Priority=100
````


sacctmgr show qos format=Name,Priority,MaxWall,MaxJobsPU,Flags

How the QOS number turns into scheduling priority

Slurm normalizes QOS priority against the highest QOS priority in the system:

QOS factor = QOS priority / highest QOS priority    (0.0 to 1.0)

Contribution to job priority = PriorityWeightQOS x QOS factor


### Useful QoS Options

| Option | Purpose | Example |
|---|---|---|
| `Priority` | Defines the QoS priority level. | `Priority=1000` |
| `MaxWall` | Maximum runtime allowed per job. | `MaxWall=04:00:00` |
| `MaxJobsPerUser` (`MaxJobsPU`) | Maximum number of running jobs per user. | `MaxJobsPerUser=5` |
| `MaxSubmitJobsPerUser` | Maximum number of submitted jobs per user, including queued and running jobs. | `MaxSubmitJobsPerUser=20` |
| `MaxTRESPerUser` | Maximum resources that a user can use through the QoS. | `MaxTRESPerUser=cpu=16` |
| `MaxTRESPerJob` | Maximum resources that a single job can request through the QoS. | `MaxTRESPerJob=cpu=8` |
| `GrpTRES` | Maximum total resources that all jobs using the QoS can consume collectively. | `GrpTRES=cpu=24` |
| `UsageFactor` | Multiplier applied to the charged usage for fair-share/accounting purposes. | `UsageFactor=2` |
| `Flags=DenyOnLimit` | Prevents job submission when a QoS limit would be exceeded instead of allowing the job to wait. | `Flags=DenyOnLimit` |

Examples:

sudo sacctmgr -i modify qos where name=high set MaxTRESPerUser=cpu=16 UsageFactor=2
sudo sacctmgr -i modify qos where name=low  set UsageFactor=0.5




# Create Slurm users and link them to accounts

** Assign commands :**

````bash 
sudo sacctmgr -i add user user1 Account=physics   DefaultAccount=physics
sudo sacctmgr -i add user user2   Account=physics   DefaultAccount=physics
sudo sacctmgr -i add user user3 Account=chemistry DefaultAccount=chemistry

````

**User QOS adding Example :**

````bash 

# user1 may use low, normal and high; default is normal
sudo sacctmgr -i modify user where name=user1 set QOS=low,normal,high DefaultQOS=normal

# user2 and user3 may use only low and normal
sudo sacctmgr -i modify user where name=user2   set QOS=low,normal DefaultQOS=normal
sudo sacctmgr -i modify user where name=user3 set QOS=low,normal DefaultQOS=normal

# Add or remove a single QOS

sudo sacctmgr -i modify user where name=user2 set QOS+=high     # grant high
sudo sacctmgr -i modify user where name=user2 set QOS-=high     # revoke high
````

**User Set limits  Example :**

````bash 

# Per user: max 10 running jobs, 50 in the system, 16 CPUs at once
sudo sacctmgr -i modify user where name=user1 account=physics set MaxJobs=10 MaxSubmitJobs=50 GrpTRES=cpu=16


# Whole-account CPU caps (server has 32 CPUs in this example)
sudo sacctmgr -i modify account where name=physics   set GrpTRES=cpu=20
sudo sacctmgr -i modify account where name=chemistry set GrpTRES=cpu=12

# Per-job cap
sudo sacctmgr -i modify user where name=user2 account=physics set MaxTRES=cpu=8

# Remove a limit: set it to -1
sudo sacctmgr -i modify user where name=user1 account=physics set MaxJobs=-1

````

**Review the whole configuration:**

````bash


sacctmgr show assoc tree format=Cluster,Account,User,Fairshare,DefaultQOS,QOS%25
sacctmgr show qos format=Name,Priority,MaxWall,MaxJobsPU,MaxTRESPU,UsageFactor,Flags
sacctmgr show user withassoc format=User,DefaultAccount,AdminLevel,Account,QOS%20
````

**Modify and remove:**

````bash

## 

# Change a user's default account
sudo sacctmgr -i modify user where name=user2 set DefaultAccount=chemistry

# Change a QOS priority
sudo sacctmgr -i modify qos where name=high set Priority=2000

# Remove a QOS from one user
sudo sacctmgr -i modify user where name=user2 set QOS-=high

# Remove a user from one account (history is kept)
sudo sacctmgr -i delete user where name=user2 account=chemistry

# Remove a user completely
sudo sacctmgr -i delete user name=user2

# Delete an account (needs no users or sub-accounts)
sudo sacctmgr -i delete account name=physics_lab1

# Delete a QOS (first remove it from users)
sudo sacctmgr -i delete qos where name=low

```` 
## Commands purpose 

### Useful `sacctmgr` and QoS Commands

| Task | Command | Purpose |
|---|---|---|
| **Show associations** | `sacctmgr show assoc tree format=Account,User,Fairshare,DefaultQOS,QOS%25` | Display account/user associations, fair-share values, default QoS, and allowed QoS. |
| **Add account** | `sacctmgr -i add account NAME Description="..." Organization="..."` | Create a new Slurm account. |
| **Add user** | `sacctmgr -i add user NAME Account=ACCT DefaultAccount=ACCT` | Add a Slurm user and associate the user with an account. |
| **Create QoS** | `sacctmgr -i add qos NAME Priority=N MaxWall=HH:MM:SS` | Create a QoS with a priority and maximum wall time. |
| **Change QoS priority** | `sacctmgr -i modify qos where name=NAME set Priority=N` | Change the priority assigned to a QoS. |
| **Allow QoS list** | `sacctmgr -i modify user where name=U set QOS=a,b,c DefaultQOS=b` | Set the QoS values a user is allowed to use and define the default QoS. |
| **Add one QoS** | `sacctmgr -i modify user where name=U set QOS+=name` | Add a QoS to the user's existing allowed QoS list. |
| **Remove one QoS** | `sacctmgr -i modify user where name=U set QOS-=name` | Remove a QoS from the user's allowed QoS list. |
| **Set account fair-share** | `sacctmgr -i modify account where name=A set Fairshare=N` | Set the fair-share value for an account. |
| **Set user fair-share** | `sacctmgr -i modify user where name=U account=A set Fairshare=N` | Set the fair-share value for a user association. |
| **Set QoS limits** | `sacctmgr -i modify qos where name=NAME set MaxJobs=N MaxSubmitJobs=N GrpTRES=cpu=N` | Set job-count and aggregate resource limits for a QoS. |
| **Remove a limit** | `sacctmgr -i modify qos where name=NAME set MaxJobs=-1` | Remove the QoS `MaxJobs` limit. |
| **Delete user from account** | `sacctmgr -i delete user where name=U account=A` | Remove the user's association with the specified account. |
| **Show job priority factors** | `sprio -l` | Display the factors contributing to pending-job priority. |
| **Show fair-share usage** | `sshare -a` | Display fair-share information for accounts and users. |
| **Submit with QoS** | `sbatch --account=A --qos=high job.sh` | Submit a batch job using a specific account and QoS. |

For detailed information about Slurm commands, configuration, scheduling, job management, and administration, refer to the official Slurm documentation:

<a href="https://slurm.schedmd.com/" target="_blank" rel="noopener">
Slurm Documentation
</a>