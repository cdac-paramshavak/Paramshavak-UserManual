# Accessing PARAM SHAVAK from Linux

Linux users can access the PARAM SHAVAK server remotely using the
**SSH (Secure Shell)** protocol.

SSH provides secure command-line access to the server and allows users
to execute Linux commands, manage files, submit HPC jobs, and monitor
SLURM workloads remotely.

## Prerequisites

Before connecting to the PARAM SHAVAK server, ensure that:

- The Linux system has network connectivity to the PARAM SHAVAK server.
- The PARAM SHAVAK server hostname or IP address is available.
- A valid PARAM SHAVAK username is available.
- The corresponding account password or SSH key is available.
- SSH service is accessible on the server.
- The SSH port is known. The default SSH port is `22`.

## Check SSH Client

Most Linux distributions provide the OpenSSH client by default.

To verify that SSH is installed:

**Command:**

````bash
```ssh -V
````
If SSH is not installed, install the OpenSSH client using the appropriate
package manager.

### RHEL / Rocky Linux / AlmaLinux

**Command:**

````bash
    sudo dnf install openssh-clients
    sudo apt install openssh-client
````

During the first connection to a server, SSH may display a message
similar to the following: