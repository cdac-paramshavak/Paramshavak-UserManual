# Remote Access to PARAM SHAVAK

Users can access the PARAM SHAVAK server remotely using **SSH (Secure Shell)** from systems such as **Windows, Linux, or macOS**.

SSH provides secure command-line access to the server 

## Linux Terminal / Windows PowerShell

Before connecting to the PARAM SHAVAK server, ensure that:

- The client system has network connectivity to the PARAM SHAVAK server.
- The PARAM SHAVAK server hostname or IP address is available.
- A valid PARAM SHAVAK username is available.
- The corresponding account password or SSH key is available.
- The SSH port is known. The default SSH port is `22`.

---

Modern versions of Windows provide an **OpenSSH client** through PowerShell or Windows Terminal.


Linux - RHEL / Rocky Linux / AlmaLinux 

```bash
sudo dnf install openssh-clients
```
Ubuntu / Debian
```bash
sudo apt install openssh-client
```
Verify the SSH client using:

The basic SSH command is the same regardless of whether the connection is initiated from Windows or Linux.


**Command:**

````bash

ssh -V # check the installation


ssh username@server-ip # 

Example: 

ssh user@192.168.1.100

````

During the first connection, SSH may display a message similar to:
```text
The authenticity of host '192.168.1.100' can't be established.
Are you sure you want to continue connecting (yes/no/[fingerprint])?

yes
```

After accepting the host key, SSH prompts for authentication. 

```text
username@server-ip's password:
```
!!! note 
The password is not displayed on the terminal while it is being entered. This is normal SSH behavior.


## Other Available Connection Methods

| Method | Purpose |
|---|---|
| PuTTY | Graphical SSH terminal |
| VS Code Remote SSH | Remote development and terminal access |
| MobaXterm | SSH, X11 forwarding, and file transfer |
| WSL | Linux environment with SSH access |

## SSH Login from Windows Using PuTTY

Windows users can access the PARAM SHAVAK server remotely using **SSH (Secure Shell)**. A commonly used SSH client for Windows is **PuTTY**.

PuTTY provides a graphical interface for establishing an SSH connection to the PARAM SHAVAK server.

!!! note

    The server must be reachable from the user's network, and the user must have a valid PARAM SHAVAK account and password before attempting to connect.

#### Prerequisites

Before connecting to the server, ensure that you have:

- A Windows computer with network access to the PARAM SHAVAK server.
- The **hostname or IP address** of the server.
- A valid **username**.
- The corresponding **password**.
- SSH service accessible on **TCP port 22**.

## Download PuTTY

Download PuTTY from the official [PuTTY website](https://www.putty.org/).


!!! tip

    Download PuTTY only from the official website or an approved software repository.

#### Configure the SSH Connection

After launching PuTTY, the **PuTTY Configuration** window is displayed.

Enter the following information:

| Setting | Value |
|---|---|
| **Host Name (or IP Address)** | PARAM SHAVAK server hostname or IP address |
| **Port** | `22` |
| **Connection Type** | `SSH` |



<img src="/image/putty01.jpg" alt="alt">

<p style="text-align: center;">Figure - PuTTY Configuration Dialog Box</p>

#### PuTTY Configuration

Enter the server hostname or IP address in the **Host Name (or IP Address)** field.


#### Establish the SSH Connection

After entering the server details:

1. Click **Open**.
2. PuTTY opens a terminal window.
3. During the first connection, PuTTY may display a **Security Alert** asking you to confirm the server's SSH host key.
4. Verify the server information with the system administrator if required.
5. Click **Accept** to continue.

The PuTTY terminal then displays the login prompt.

## Enter the Username

At the login prompt, enter your PARAM SHAVAK account username.

**Command:**

```text
login as: username

Press **Enter**.

## Enter the Password

Enter the password associated with your PARAM SHAVAK account and press **Enter**.

```

<img src="/image/putty02.jpg" alt="alt">
<p style="text-align: center;">Figure - PuTTY Terminal Window</p>


After successful authentication, the server displays the login message and any configured system announcements.

You are now logged in to the PARAM SHAVAK server and can use the available Linux commands, applications, and HPC/SLURM commands according to your account permissions.


## VS Code Remote SSH

**Visual Studio Code Remote SSH** allows users to connect to the PARAM SHAVAK server remotely and work directly on the server from the Windows desktop.

It is useful for users who need to:

- Access the PARAM SHAVAK server remotely.
- Open and edit files stored on the server.
- Open a remote terminal.
- Run Linux commands.
- Develop and test applications directly on the server.
- Work with source code and installed development environments.

#### Prerequisites

Before using VS Code Remote SSH, ensure that:

- Visual Studio Code is installed on the Windows system.
- The **Remote - SSH** extension is installed.
- The PARAM SHAVAK server is reachable through the network.
- SSH access is enabled on the server.
- A valid PARAM SHAVAK username and password are available.

#### Download Visual Studio Code

Download and install Visual Studio Code from the official
[Visual Studio Code website](https://code.visualstudio.com/).

#### Install the Remote - SSH Extension

1. Open **Visual Studio Code**.
2. Select **Extensions** from the left-side Activity Bar.
3. Search for **Remote - SSH**.
4. Install the **Remote - SSH** extension published by Microsoft.

#### Connect to the PARAM SHAVAK Server

1. Open Visual Studio Code.
2. Press:

```text
Ctrl + Shift + P

```ssh username@server-ip
```

## MobaXterm

**MobaXterm** is a Windows-based terminal application that provides multiple remote-access features in a single interface.

It can be used to connect to the PARAM SHAVAK server using **SSH** and provides additional features such as **SFTP, SCP, and X11 forwarding**.

MobaXterm is useful when users require command-line access, file transfer, or graphical application access from a Windows system.

#### Prerequisites

Before connecting to the PARAM SHAVAK server using MobaXterm, ensure that:

- MobaXterm is installed on the Windows system.
- The PARAM SHAVAK server is reachable from the Windows system.
- SSH service is enabled on the server.
- The server hostname or IP address is available.
- A valid PARAM SHAVAK username and password are available.

#### Download MobaXterm

Download MobaXterm from the official [MobaXterm website](https://mobaxterm.mobatek.net/).

Install or run the appropriate version according to your organization's software policy.

#### Create an SSH Session

1. Launch **MobaXterm**.
2. Click **Session** from the top menu.
3. Select **SSH**.
4. Enter the PARAM SHAVAK server hostname or IP address.
5. Specify the SSH port.
6. Enter the PARAM SHAVAK username.
7. Click **OK**.
8. Enter the password when prompted.

Use the following connection settings:

| Setting | Value |
|---|---|
| **Remote host** | PARAM SHAVAK server hostname or IP address |
| **Port** | `22` |
| **Username** | PARAM SHAVAK username |

#### SSH Connection

After successful authentication, MobaXterm opens an SSH terminal connected to the PARAM SHAVAK server.





