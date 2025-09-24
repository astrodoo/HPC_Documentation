# Accessing the HPC System
The standard method for accessing Argon is via **SSH (Secure Shell)**. You’ll need an SSH client installed on your workstation:

- **Linux/macOS**: SSH is built-in. Open a terminal and initiate a session.
- **Windows**: Install an SSH client. The recommended option is **SecureCRT**, which is licensed by the University of Iowa.

## Connection Instructions

### On Campus or Connected via VPN

```bash
user@local ~> ssh HawkID@argon.hpc.uiowa.edu
```

### Off Campus Without VPN

To enhance security, Argon uses an alternate SSH port when accessed from outside the campus network without VPN:

```bash
user@local ~> ssh -p 40 HawkID@argon.hpc.uiowa.edu
```

!!! info 
    For Windows users, enter the appropriate values in your SSH client’s configuration fields.  
    When prompted, enter your **HawkID password**. If successful, you’ll be logged into one of Argon’s login nodes.

---

## Login Node Behavior

Argon uses **multiple login nodes**, and SSH connections are distributed in a **round-robin** fashion. While you generally don’t need to worry about which node you're connected to, be aware that different sessions may land on different nodes.

Each login node has both an **internal name** (visible in your shell) and an **external alias**. This mapping may be useful if you need to reconnect to the same node:

| Internal Name              | External Name (Alias)                      |
|---------------------------|--------------------------------------------|
| argon-itf-login-3.hpc     | argon-itf-login-3.hpc.uiowa.edu *(argon-login-3.hpc.uiowa.edu)* |
| argon-itf-login-4.hpc     | argon-itf-login-4.hpc.uiowa.edu *(argon-login-4.hpc.uiowa.edu)* |
| argon-login-5.hpc         | argon-login-5.hpc.uiowa.edu                |
| argon-login-6.hpc         | argon-login-6.hpc.uiowa.edu                |

