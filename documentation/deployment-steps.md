# Linux, Networking & Cloud Infrastructure – Deployment Steps

## 1. Create an Azure Virtual Machine

Created an Ubuntu Linux virtual machine using Microsoft Azure.

**VM Configuration:**
- VM Name: `codomax-linux-vm`
- Resource Group: `codomax-devops-rg`
- Operating System: Ubuntu Server 24.04 LTS
- Region: East Asia
- Username: `azureuser`

## 2. Connect to the Linux Server Using SSH

Connected to the Azure virtual machine remotely from Windows PowerShell using an SSH private key.

Command:

```bash
ssh -i "path-to-private-key.pem" azureuser@PUBLIC_IP
```

The SSH connection provided secure remote access to the Ubuntu server.

**Security note:** The private SSH key must be stored securely and must never be uploaded to GitHub.

## 3. Update the Ubuntu Server

Updated the package information and installed available updates.

```bash
sudo apt update
sudo apt upgrade -y
```

## 4. Perform Linux Administration

### Check system information

```bash
whoami
hostname
uptime
uname -r
who
```

### Create a project directory and files

```bash
mkdir codomax-project
cd codomax-project
touch README.md
touch linux-commands.txt
```

### Create a Linux user

```bash
sudo adduser intern
```

### Create a Linux group

```bash
sudo groupadd devops
```

### Add the user to the group

```bash
sudo usermod -aG devops intern
```

### Verify group membership

```bash
groups intern
```

### Configure file permissions

```bash
chmod 755 README.md
ls -l README.md
```

## 5. Explore Linux Networking

Used the following commands to inspect network interfaces and connectivity.

### Display IP addresses

```bash
ip addr
```

### Display network interfaces

```bash
ip link
```

### Check hostname

```bash
hostname
```

### Test internet connectivity

```bash
ping -c 4 google.com
```

### Check DNS resolution

```bash
nslookup google.com
```

### Display routing information

```bash
ip route
```

### Check listening ports

```bash
sudo ss -tulnp
```

These commands helped verify the server's network configuration, DNS resolution, routing and listening services.

## 6. Configure the Ubuntu Firewall (UFW)

Checked the firewall status:

```bash
sudo ufw status
```

Allowed SSH connections:

```bash
sudo ufw allow OpenSSH
```

Allowed HTTP traffic:

```bash
sudo ufw allow 80/tcp
```

Enabled the firewall:

```bash
sudo ufw enable
```

Verified the firewall rules:

```bash
sudo ufw status verbose
```

**Configured rules:**
- Port 22 – SSH access.
- Port 80 – HTTP website access.

The default incoming traffic policy denies connections unless explicitly allowed.

## 7. Configure Azure Network Security Group (NSG)

Configured an inbound security rule in Azure to allow external HTTP traffic.

**HTTP inbound rule:**
- Source: Any
- Source Port: `*`
- Destination: Any
- Destination Port: `80`
- Protocol: TCP
- Action: Allow
- Priority: `310`
- Name: `Allow-HTTP`

This allowed external users to access the Nginx web server through the VM's public IP address.

## 8. Install and Configure Nginx

Updated package information:

```bash
sudo apt update
```

Installed Nginx:

```bash
sudo apt install nginx -y
```

Started Nginx and enabled automatic startup:

```bash
sudo systemctl enable --now nginx
```

Checked the Nginx service status:

```bash
sudo systemctl status nginx
```

Verified that Nginx was running successfully.

## 9. Test the Web Server

Tested the web server locally:

```bash
curl -I http://localhost
```

**Expected response:**

```text
HTTP/1.1 200 OK
Server: nginx/1.24.0 (Ubuntu)
```

The successful HTTP response confirmed that Nginx was serving web requests.

## 10. Test External Connectivity

Opened the Azure VM's public IP address using HTTP in a web browser.

Verified that the default **Welcome to nginx!** page was accessible externally.

This confirmed:
- Nginx was running successfully.
- UFW allowed incoming HTTP traffic.
- Azure NSG allowed TCP port 80.
- External website connectivity was working.

## 11. Deployment Outcome

Successfully created and configured an Ubuntu Linux virtual machine using Microsoft Azure.

Configured Linux users, groups, permissions, networking and firewall rules. Installed and started Nginx and successfully accessed the hosted website through the Azure VM's public IP address.

This practical project provided hands-on experience in Linux system administration, networking, security and cloud infrastructure deployment.
