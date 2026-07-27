# Phase 1 - Linux Server Administration

## Objective

Prepare the Ubuntu system for DevOps work by performing initial server configuration.

## Tasks Completed

- Updated Ubuntu packages
- Installed essential utilities
- Created users:
  - devops
  - deploy
  - monitor
- Granted sudo access to the devops user
- Generated SSH key pair
- Configured system hostname
- Enabled automatic security updates
- Configured Logrotate
- Verified NTP (time synchronization)

## Commands Used

### Update Ubuntu

#bash
sudo apt update
sudo apt upgrade -y


### Install Packages

#bash

sudo apt install -y git curl wget vim nano tree htop unzip zip jq net-tools #these are the commands which i install


### Create Users

#bash
sudo adduser devops
sudo adduser deploy
sudo adduser monitor


### Grant Sudo Access

#bash

sudo usermod -aG sudo devops


### Generate SSH Key

#bash

ssh-keygen -t ed25519


### Change Hostname

#bash

sudo hostnamectl set-hostname devops-lab


### Enable Automatic Updates

#bash

sudo apt install unattended-upgrades -y

sudo dpkg-reconfigure unattended-upgrades


### Configure Logrotate

#bash

sudo nano /etc/logrotate.d/myapp


### Verify NTP

#bash

timedatectl

## Verification

- Users created successfully
- SSH keys generated
- Hostname updated
- Automatic updates enabled
- Logrotate configured
- NTP synchronized
