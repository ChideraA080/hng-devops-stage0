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


###  Route: `/api`

Returns JSON response:

```json
{
  "message": "HNGI14 Stage 0",
  "track": "DevOps",
  "username": "pamelaunik"
}
```
### SSL Configuration

- SSL certificate issued using Let's Encrypt (Certbot)

- HTTPS enabled for domain

- HTTP automatically redirects to HTTPS using 301 redirect

### Domain:

https://chidera-devops.duckdns.org

### Technical Requirements Met

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

### Testing

Tested using:

curl https://chidera-devops.duckdns.org/

curl https://chidera-devops.duckdns.org/api

### Screenshots:


Launched Instance
![Instance Running](https://github.com/ChideraA080/hng-devops-stage0/blob/main/Hng_Stage0%20Screenshots/1000754636.jpg)

HngDevops Group Added
![Hnggroup Added](https://github.com/ChideraA080/hng-devops-stage0/blob/main/Hng_Stage0%20Screenshots/IMG_20260415_100624.jpg)

Default Nginx Running On Browser
![Default Nginx Running](https://github.com/ChideraA080/hng-devops-stage0/blob/main/Hng_Stage0%20Screenshots/IMG_20260415_115749.jpg)

Nginx Successfully Configured
![Nginx Success Config](https://github.com/ChideraA080/hng-devops-stage0/blob/main/Hng_Stage0%20Screenshots/1000754172.jpg)

UFW Status
![Ufw Status](https://github.com/ChideraA080/hng-devops-stage0/blob/main/Hng_Stage0%20Screenshots/IMG_20260415_120227.jpg)

Domain Live Displaying username
![Domain Displaying Username](https://github.com/ChideraA080/hng-devops-stage0/blob/main/Hng_Stage0%20Screenshots/1000754634.jpg)

Certificate Encrypt
![Cert Encrypt Success](https://github.com/ChideraA080/hng-devops-stage0/blob/main/Hng_Stage0%20Screenshots/1000754194.jpg)

Domain Testing
![Domain Testing](https://github.com/ChideraA080/hng-devops-stage0/blob/main/Hng_Stage0%20Screenshots/1000754251.jpg)

Live Domain Dispalying Track and Username 
![Live Domain](https://github.com/ChideraA080/hng-devops-stage0/blob/main/Hng_Stage0%20Screenshots/1000754193.jpg)




Author

HNG Username: Pamelaunik

Project: DevOps Stage 0

