# Understanding Slurm

Understanding Slurm on a Single-Node Server

## What is Slurm, and why used?


Slurm (originally Simple Linux Utility for Resource Management) is an open-source workload manager. It does three jobs:

*Resource management*:	Tracks the server's CPUs, memory and GPUs and hands them out to jobs.
*Job scheduling*:	Decides which job runs and when, using a queue, priorities and policies.
*Accounting*:	Records who ran what, for how long, using which resources (via slurmdbd).



## Components in detail

| Daemon | Default Port / Role | Description |
|---|---:|---|
| `slurmctld`| `6817` | **Central manager:** Tracks nodes and jobs, runs the scheduler, and decides which jobs start. |
| `slurmd` | `6818` | **Node agent:** Registers node resources, receives job-launch requests, starts and monitors jobs. |
| `munge` | None *(local socket)* | **Authentication:** Signs and verifies messages so Slurm components can authenticate and trust each other. |
| `slurmdbd` | `6819` | **Accounting gateway:** Receives accounting information from Slurm and communicates with the SQL database. |
| `slurmrestd` | Configurable | **REST API:** Optional service that provides HTTP/REST access to Slurm for web applications and external tools. |




* **`slurmctld`** – The central Slurm controller daemon that runs on the management or controller node. It manages jobs, partitions, node states, scheduling, and resource allocation.
* **`slurmd`** – The Slurm compute-node daemon that runs on each compute node. It receives and executes jobs assigned by `slurmctld` and reports the node status back to the controller.

The `slurmd` daemons communicate with the central `slurmctld` daemon and participate in the hierarchical communication structure used by Slurm. This architecture enables Slurm to efficiently manage jobs and resources across multiple compute nodes.



## Supporting services

| Service / Component | Purpose |
|---|---|
| **MariaDB** | Stores accounting data such as job records, users, accounts, QoS, limits, and usage. |
| **cgroups** *(Linux kernel)* | Confines each job to its allocated CPU and memory resources. |
| **Time synchronization** *(chrony)* | Keeps the system clock synchronized. MUNGE credentials are time-sensitive, so accurate time is required. |
| **Hostname resolution** | Ensures the server's short hostname resolves correctly. See [Section 9](#9-hostname-resolution). |



## Job Submission and Execution Flow


The life cycle at a glance

| # | Stage | Who does it | Job state |
|---|---|---|---|
| 1 | **Submit**: user sends the request | `sbatch` / `srun` / `salloc` | (none yet) |
| 2 | **Validate**: check account, QOS, limits, resource request | `slurmctld` (+ `slurmdbd` data) | (none yet) |
| 3 | **Queue**: job gets an ID and waits | `slurmctld` | `PENDING` |
| 4 | **Prioritize and schedule**: rank the queue, find resources | `slurmctld` scheduler | `PENDING` |
| 5 | **Allocate**: reserve CPUs and memory | `slurmctld` | `RUNNING` (or `CONFIGURING` briefly) |
| 6 | **Launch**: start the job on the node | `slurmd` + `slurmstepd` | `RUNNING` |
| 7 | **Execute**: script and job steps run inside a cgroup | `slurmstepd` | `RUNNING` |
| 8 | **Complete**: exit, cleanup, resources freed | `slurmstepd`, `slurmd`, `slurmctld` | `COMPLETING` then final state |
| 9 | **Account**: record stored | `slurmctld` to `slurmdbd` to MariaDB | final state |
| 10 | **Purge**: forgotten by the controller | `slurmctld` after `MinJobAge` | (`sacct` only) |

---




## 
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




For detailed information about Slurm commands, configuration, scheduling, job management, and administration, refer to the official Slurm documentation:

<a href="https://slurm.schedmd.com/" target="_blank" rel="noopener">
Slurm Documentation
</a>