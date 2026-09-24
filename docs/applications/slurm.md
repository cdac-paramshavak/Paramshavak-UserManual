# Slurm 
The primary Slurm components are:

* **`slurmctld`** – The central Slurm controller daemon that runs on the management or controller node. It manages jobs, partitions, node states, scheduling, and resource allocation.
* **`slurmd`** – The Slurm compute-node daemon that runs on each compute node. It receives and executes jobs assigned by `slurmctld` and reports the node status back to the controller.
* **Backup Controller** – An optional secondary `slurmctld` daemon can be configured to provide failover and improve controller availability.

The `slurmd` daemons communicate with the central `slurmctld` daemon and participate in the hierarchical communication structure used by Slurm. This architecture enables Slurm to efficiently manage jobs and resources across multiple compute nodes.


```
Slurm command options are **case-sensitive**. Most Slurm commands also provide a brief summary of available options through the `--help` option.
```

## Common Slurm Commands

The following commands are commonly used by HPC users and administrators to submit jobs, monitor workloads, manage resources, and inspect cluster status.

## `sbatch`

`sbatch` submits a job script to Slurm for execution. The job is placed in the queue and executed when the required resources become available.

The submitted script commonly contains one or more `srun` commands for launching parallel tasks.

**Command:**

````bash
sbatch
````

## `scancel`

`scancel` cancels a pending or running job or job step.

It can also be used to send signals to processes associated with a running job or job step.

**Command:**

````bash
scancel
````

## `scontrol`

`scontrol` is an administrative command used to view and modify Slurm configuration and runtime state.

It can be used to manage jobs, nodes, partitions, reservations, and other Slurm resources.

!!! warning

```
Many `scontrol` operations require administrator or `root` privileges.
```

**Command:**

````bash
scontrol
````

## `sinfo`

`sinfo` displays information about Slurm partitions and compute nodes.

It can be used to view node availability, partition status, node states, and resource information. The command provides several filtering, sorting, and formatting options.

**Command:**

````bash
sinfo
````


## `squeue`

`squeue` displays the current state of jobs and job steps managed by Slurm.

It is commonly used to monitor running and pending jobs. By default, jobs are displayed according to their scheduling priority.

**Command:**

````bash
squeue
````

## `srun`

`srun` launches a job or job step on resources managed by Slurm.

It provides numerous options for specifying resource requirements, including:

* Number of nodes
* Number of CPUs or tasks
* Memory requirements
* Specific nodes
* Node features
* GPU resources
* Time limits

A single Slurm job can contain multiple job steps that execute sequentially or concurrently using the allocated resources.

**Command:**

````bash
srun
````


## `sstat`

`sstat` displays resource utilization information for a currently running job or job step.

It can be used to monitor resource consumption such as CPU and memory usage while a job is executing.

**Command:**

````bash
sstat
````

## `sview`

`sview` provides a graphical user interface for viewing and, where permitted, modifying Slurm cluster state.

It can display information about:

* Jobs
* Nodes
* Partitions
* Reservations
* Other Slurm-managed resources

**Command:**

````bash
sview
````



## `salloc`

`salloc` allocates resources for a job in real time. It is commonly used to obtain an interactive allocation and start a shell on the allocated resources.

Once the allocation is granted, `srun` can be used to launch parallel tasks.

**Command:**

````bash
salloc
````

## `sattach`

`sattach` attaches the standard input, output, and error streams of the current terminal to a running Slurm job or job step.

It can also be used to attach to or detach from a running job multiple times.

**Command:**

````bash
sattach
````

Slurm provides a comprehensive workload management and scheduling framework for HPC clusters, enabling users and administrators to efficiently manage compute resources, submit and monitor jobs, and control cluster workloads.


##Slurmdbd Setup:

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



## `sacctmgr`

**Command:**

````bash
sacctmgr
````



## `sacct`

`sacct` displays accounting information for jobs and job steps. It can be used to view information about both active and completed jobs, including resource usage and job status.

**Command:**

````bash
sacct
````




For detailed information about Slurm commands, configuration, scheduling, job management, and administration, refer to the official Slurm documentation:

<a href="https://slurm.schedmd.com/" target="_blank" rel="noopener">
Slurm Documentation
</a>