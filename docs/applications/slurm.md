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

## `sbcast`

`sbcast` transfers a file from the local disk of the submitting system to the local disks of the compute nodes allocated to a job.

This can be useful for diskless environments or when transferring frequently accessed files locally can provide better performance than accessing them through a shared filesystem.

**Command:**

````bash
sbcast
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

## `sprio`

`sprio` displays detailed information about the factors that contribute to a job's scheduling priority.

It is particularly useful for understanding why one pending job may be scheduled before another.

**Command:**

````bash
sprio
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

## `strigger`

`strigger` is used to configure and monitor Slurm event triggers.

Triggers can be configured for events such as:

* A compute node changing state
* A node becoming unavailable
* A job approaching its time limit
* Other Slurm state changes

**Command:**

````bash
strigger
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


## `sacct`

`sacct` displays accounting information for jobs and job steps. It can be used to view information about both active and completed jobs, including resource usage and job status.

**Command:**

````bash
sacct
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

For detailed information about Slurm commands, configuration, scheduling, job management, and administration, refer to the official Slurm documentation:

<a href="https://slurm.schedmd.com/" target="_blank" rel="noopener">
Slurm Documentation
</a>