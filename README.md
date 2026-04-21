#  HNG DevOps Stage 0 – Linux Server Setup & Nginx Configuration

##  Overview

This project is part of the HNG DevOps Stage 0 task. 
It involves provisioning a Linux server, securing it, configuring Nginx to serve a static webpage and API endpoint, and securing the server using SSL (Let's Encrypt).

## Server Setup

A Linux Ubuntu server was provisioned on a cloud provider.

###  Security Configuration

- Created a non-root user: `hngdevops`
- Granted sudo privileges to `hngdevops`
- Disabled root SSH login
- Disabled password authentication (key-based authentication only)
- Configured UFW firewall to allow only:
  - Port 22 (SSH)
  - Port 80 (HTTP)
  - Port 443 (HTTPS)


##  SSH Configuration

- Added HNG-provided public SSH key to:

/home/hngdevops/.ssh/authorized_keys


- Set correct permissions:
  - `.ssh` → 700
  - `authorized_keys` → 600

##  Nginx Configuration

Nginx was installed and configured to serve two endpoints:

###  Route: `/`

Returns a static HTML page containing:

my-hng-username:pamelaunik


### 📍 Route: `/api`

Returns JSON response:

```json
{
  "message": "HNGI14 Stage 0",
  "track": "DevOps",
  "username": "pamelaunik"
}

SSL Configuration

- SSL certificate issued using Let's Encrypt (Certbot)

- HTTPS enabled for domain

- HTTP automatically redirects to HTTPS using 301 redirect

Domain:

https://chidera-devops.duckdns.org

Technical Requirements Met

 - Linux server provisioned

 - Non-root user created (hngdevops)

 - SSH key authentication enabled

 - Root login disabled

 - Password authentication disabled

 - UFW configured (22, 80, 443 only)

 - Nginx installed and running

 - / serves static HTML with username visible

 - /api returns correct JSON response

 - SSL certificate installed (Let's Encrypt)

 - HTTP → HTTPS redirect (301)

Testing

Tested using:

curl https://chidera-devops.duckdns.org/

curl https://chidera-devops.duckdns.org/api

Author

HNG Username: Pamelaunik

Project: DevOps Stage 0

