# Linux, Networking & Cloud Infrastructure

## 1. Project Overview

This project demonstrates the deployment and configuration of a Linux server using Microsoft Azure.

An Ubuntu Linux Virtual Machine was created in Azure, configured with essential Linux administration and networking settings, secured using firewalls, and used to host a website with the Nginx web server.

## 2. Technologies and Tools

- Microsoft Azure
- Ubuntu Server 24.04 LTS
- Linux Command Line Interface (CLI)
- SSH
- UFW Firewall
- Azure Network Security Group (NSG)
- Nginx Web Server
- GitHub

## 3. Azure Virtual Machine Setup

Created an Ubuntu Server 24.04 LTS virtual machine using Microsoft Azure.

**Configuration:**
- Virtual Machine Name: `codomax-linux-vm`
- Resource Group: `codomax-devops-rg`
- Operating System: Ubuntu Server 24.04 LTS
- Region: East Asia

Connected to the virtual machine remotely using SSH and a private key.

Example SSH command:

```bash
ssh -i "path-to-private-key.pem" azureuser@PUBLIC_IP
```

**Note:** The actual private key must be kept secure and must never be uploaded to GitHub.

## 4. Linux Administration

Practised Linux command-line operations and system administration.

### Basic Linux Commands

| Command | Purpose |
|---|---|
| `whoami` | Display current username |
| `hostname` | Display computer name |
| `uptime` | Show system uptime |
| `uname -r` | Display kernel version |
| `who` | Show logged-in users |
| `ls -l` | List files with permissions |
| `mkdir` | Create a directory |
| `touch` | Create an empty file |
| `cat` | Display file contents |
| `sudo apt update` | Update package information |
| `sudo apt upgrade -y` | Upgrade installed packages |

### User and Group Management

Created a Linux user named `intern` and a group named `devops`.

Commands:

```bash
sudo adduser intern
sudo groupadd devops
sudo usermod -aG devops intern
groups intern
```

### File Permissions

Practised changing file permissions using `chmod`.

```bash
chmod 755 README.md
ls -l README.md
```

## 5. Linux Networking

Practised networking commands to inspect the server's network configuration and connectivity.

| Command | Purpose |
|---|---|
| `ip addr` | Display IP addresses |
| `ip link` | Display network interfaces |
| `ip route` | Display routing table |
| `ping -c 4 google.com` | Test network connectivity |
| `nslookup google.com` | Check DNS name resolution |
| `sudo ss -tulnp` | Display listening ports and sockets |

Verified internet connectivity and DNS resolution from the Ubuntu server.

## 6. Firewall Configuration

Configured the Ubuntu UFW firewall to control incoming network connections.

Commands:

```bash
sudo ufw status
sudo ufw allow OpenSSH
sudo ufw allow 80/tcp
sudo ufw enable
sudo ufw status verbose
```

Allowed:
- Port 22 (SSH) for remote server access.
- Port 80 (HTTP) for website access.

The default incoming policy was set to deny, with explicitly allowed services.

## 7. Azure Network Security Group (NSG)

Configured an inbound security rule in Azure to allow HTTP traffic.

**HTTP inbound rule:**
- Protocol: TCP
- Destination Port: 80
- Action: Allow
- Priority: 310
- Rule Name: Allow-HTTP

This allowed external users to access the Nginx web server through the virtual machine's public IP address.

## 8. Nginx Web Server Deployment

Installed Nginx on the Ubuntu virtual machine.

Installation:

```bash
sudo apt update
sudo apt install nginx -y
```

Started Nginx and enabled it to start automatically after system reboots.

```bash
sudo systemctl enable --now nginx
```

Checked the service status:

```bash
sudo systemctl status nginx
```

Verified the local web server response:

```bash
curl -I http://localhost
```

**Result:** Received `HTTP/1.1 200 OK`, confirming that the Nginx web server was responding successfully.

## 9. Website Connectivity Testing

Opened the virtual machine's public IP address in a web browser using HTTP.

Successfully accessed the default **Welcome to nginx!** page from outside the virtual machine.

This confirmed that:
- Nginx was running.
- The Ubuntu firewall allowed HTTP traffic.
- The Azure NSG allowed inbound HTTP traffic.
- External browser connectivity was working.

## 10. Project Screenshots

Screenshots will be added to the `screenshots` folder as evidence of the completed tasks.

## 11. Conclusion

Successfully deployed an Ubuntu Linux server using Microsoft Azure and hosted a website using Nginx.

This project provided practical experience in Linux command-line operations, user and permission management, SSH connectivity, IP addressing, DNS resolution, firewall configuration, Azure network security, and web server deployment.

It strengthened my understanding of Linux administration, networking, and cloud infrastructure.
