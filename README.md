# Pritunl VPN Server Installation on Ubuntu

This guide walks you through the steps to install the Pritunl VPN server on an Ubuntu machine.

## Prerequisites

- A fresh Ubuntu server
- Root (or sudo) access to the machine

## Server Details
- **Pritunl Server Port:** 17057
- **Pritunl Server Password:** 12345
- **User Password:** 12345678

---

## Steps to Install Pritunl Server on Ubuntu

### 1. Update the System

Start by updating the package list and upgrading the system packages:

```bash
sudo apt update && sudo apt upgrade -y

# Add the Pritunl Repository

sudo tee /etc/apt/sources.list.d/pritunl.list << EOF
deb http://repo.pritunl.com/stable/apt jammy main
EOF

# Import the Pritunl Signing Key
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com --recv 7568D9BB55FF9E5287D586017AE645C0CF8E292A

# Add the MongoDB 6.0 Repository

sudo tee /etc/apt/sources.list.d/mongodb-org-6.0.list << EOF
deb https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/6.0 multiverse
EOF

# Import the MongoDB Public Key
wget -qO - https://www.mongodb.org/static/pgp/server-6.0.asc | sudo apt-key add -

# Update Package Lists
sudo apt update
sudo apt --assume-yes upgrade

# Disable UFW Firewall
sudo ufw disable

# Install Pritunl and MongoDB

sudo apt -y install pritunl mongodb-org

# Enable Services to Start at Boot

sudo systemctl enable mongod pritunl

# Start the Services Immediately

sudo systemctl start mongod pritunl
sudo systemctl status mongod pritunl
```

To download the Pritunl VPN client for your system, visit:
https://client.pritunl.com/


![View](./Image/Screenshot%202025-10-15%20003240.png)
![View](./Image/Screenshot%202025-10-15%20003342.png)
![View](./Image/Screenshot%202025-10-15%20003750.png)