# Assignment3p1
## Introduction
Welcome to my Bash scripting project! This guide will walk you on how to generate a static `index.html` file containing your system's information. The script will be scheduled to run daily at 05:00 using a `systemd` service and timer. The generated HTML file will be served by an nginx web server, with  security provided by a firewall configured using `ufw`.

---
## Prerequisites
To get started, pleas ensure you meet the following requirements:
- **Operating System**: Arch Linux with Bash.
- **Permissions**: Root access to execute the scripts.
---
## Setting up the System User and Directory Structure
1. Run the following command to create a system user with a home directory in `/var/lib/webgen` with a non-login shell:
```bash
sudo useradd -r -d /var/lib/webgen -s /usr/sbin/nologin webgen
```
#### What does this command do?
`useradd`: Command to add a new user to the system.
`-r`:  Creates a system user 
`-d /var/lib/webgen`:  Specifies the home directory for the user as `var/lib/webgen`
`-s /usr/sbin/nologin`: Sets the user's shell to prevent the user from logging into the system interactively
`webgen`: The name of the user being created

>[!NOTE]
>**What is the benefit of creating a system user for this task rather than using a regular user or root?**
>Using a system user enhances security by limiting privileges and preventing interactive logins, reducing risks compared to using a regular user or root. It isolates processes, simplifies monitoring, and ensures tasks have only the access they need. This approach minimizes potential damage and ensures a more secure, maintainable system.


2. Create the home directory structure
```bash
sudo mkdir /var/lib/webgen/bin /var/lib/webgen/HTML
```

3.  Copy the `generate_index` script into the `/var/lib/webgen/bin` folder
```bash
sudo cp assignment3/2420-as2-start/generate_index /var/lib/webgen/bin
```

4. Give ownership to `webgen` and make `generate_index` executable
```bash
sudo chown -R webgen:webgen /var/lib/webgen
sudo chmod 700 /var/lib/webgen/bin/generate_index
```

---
