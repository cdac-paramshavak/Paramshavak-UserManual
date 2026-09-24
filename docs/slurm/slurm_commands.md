# User commands (clients)

| Command | Category | What it does |
|---|---|---|
| `sbatch` | Submit | Submit a batch script to the queue. |
| `srun` | Submit / launch | Run a command on allocated resources, or launch tasks inside a job. |
| `salloc` | Submit | Get an allocation for interactive work. |
| `squeue` | Query | Show jobs in the queue. |
| `sinfo` | Query | Show partition and node state. |
| `scontrol` | Query / admin | Detailed view and control of jobs, the node, partitions. |
| `scancel` | Control | Cancel jobs. |
| `sstat` | Query | Live statistics of a running job. |
| `sacct` | Accounting | History of finished and running jobs. |
| `sacctmgr` | Accounting admin | Manage clusters, accounts, users, QOS. |
| `sreport` | Accounting | Usage reports. |
| `sshare` | Accounting | Fair-share usage tree. |
| `sprio` | Accounting | Priority factors of pending jobs. |

---



Common Slurm Commands

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



For detailed information about Slurm commands, configuration, scheduling, job management, and administration, refer to the official Slurm documentation:

<a href="https://slurm.schedmd.com/" target="_blank" rel="noopener">
Slurm Documentation
</a>