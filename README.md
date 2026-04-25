#  HNG DevOps Stage 0 – Linux Server Setup & Nginx Configuration

##  Overview

This project is part of the HNG DevOps Stage 0 task. 
It involves provisioning a Linux server, securing it, configuring Nginx to serve a static webpage and API endpoint, and securing the server using SSL (Let's Encrypt).

This project focuses on **core DevOps fundamentals** including server hardening, web server configuration, and secure remote access.

## Architecture Diagram

This diagram shows the flow of traffic from the user to the server, including DNS resolution, Nginx routing, and HTTPS handling.

![Architecture Diagram](https://github.com/ChideraA080/hng-devops-stage0/blob/main/Hng_Stage0%20Screenshots/HngStage0%20Architectural%20Diagram.png)

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

  Evidence of Successful UFW Configuration:
  ![Ufw Status](https://github.com/ChideraA080/hng-devops-stage0/blob/main/Hng_Stage0%20Screenshots/IMG_20260415_120227.jpg)


##  SSH Configuration

- Added HNG-provided public SSH key to:

/home/hngdevops/.ssh/authorized_keys


- Set correct permissions:
  - `.ssh` → 700
  - `authorized_keys` → 600
  
Evidence of Successful SSH Verification
  ![Hnggroup Added](https://github.com/ChideraA080/hng-devops-stage0/blob/main/Hng_Stage0%20Screenshots/IMG_20260415_100624.jpg)

##  Nginx Configuration

Nginx was installed and configured to serve two endpoints:

###  Route: `/`

Returns a static HTML page containing:

my-hng-username:pamelaunik

Verification Output
![Domain Displaying Username](https://github.com/ChideraA080/hng-devops-stage0/blob/main/Hng_Stage0%20Screenshots/1000754634.jpg)

###  Route: `/api`

Returns JSON response:

```json
{
  "message": "HNGI14 Stage 0",
  "track": "DevOps",
  "username": "pamelaunik"
}
```
Evidence of Successfull Configuration
![Live Domain](https://github.com/ChideraA080/hng-devops-stage0/blob/main/Hng_Stage0%20Screenshots/HNG%20API.png)

Content-Type: application/json
Status: 200 OK

## SSL Configuration

- SSL certificate issued using Let's Encrypt (Certbot)

- HTTPS enabled for domain

- HTTP automatically redirects to HTTPS using 301 redirect

## Domain:

https://chidera-devops.duckdns.org

## Technical Requirements Met

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

## Tools & Technologies

Linux (Ubuntu)

Nginx

UFW Firewall

OpenSSH

Certbot (Let's Encrypt)

AWS EC2

DuckDNS

### Testing & Validation

Tested using:

curl https://chidera-devops.duckdns.org/

curl https://chidera-devops.duckdns.org/api

## Challenges Faced & Solutions
 1. SSH Access Failure (Permission Denied)

Issue:
Grader could not connect via SSH.

Cause:
Incorrect or missing public key in authorized_keys.

Solution:

- I properly added HNG public key
- I fixed permissions:
```
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
```
- Verified ownership:
```
chown -R hngdevops:hngdevops ~/.ssh
```
2. API Response Failing Validation

Issue:
JSON response did not match expected format.

Cause:
Extra spaces and formatting issues.

Solution:
- I ensured strict JSON format in Nginx:
```
return 200 '{"message":"HNGI14 Stage 0","track":"DevOps","username":"pamelaunik"}';
```
3. UFW Check Failed

Issue:
Grader couldn’t run ufw status.

Cause:
Sudo required password.

Solution:
Configured passwordless sudo:
```
hngdevops ALL=(root) NOPASSWD:/usr/sbin/sshd,/usr/sbin/ufw
```
## Key Learnings

- I learned how critical **SSH key authentication and proper file permissions** are. A small mistake in the `authorized_keys` setup or permissions can completely block server access and cause automation checks to fail.

- I gained hands-on experience in **securing a Linux server**, including disabling root login, turning off password authentication, and restricting access using UFW.

- I understood how to use **Nginx not just for static websites but also for routing API endpoints**, especially configuring `/api` to return the correct JSON response.

- I realized how important **strict formatting is in automation systems** - even minor differences in JSON structure, spacing, or username casing can lead to failed validations.

- I improved my ability to **troubleshoot and debug under pressure**, especially after failed attempts, by carefully identifying issues and fixing them step-by-step.

- Overall, this project helped me move from just learning concepts to actually **applying DevOps practices in a real-world scenario**.

##  Outcome

- I successfully set up a **secure Linux-based web server** from scratch, handling both configuration and security manually.

- I implemented proper **access control** by creating a non-root user and securing SSH with key-based authentication.

- I configured **UFW firewall rules** to expose only the required ports (22, 80, 443), improving the server’s security.

- I built a working **API endpoint (`/api`) using Nginx**, returning the exact JSON format required for validation.

- I secured the application with **HTTPS using Let's Encrypt (Certbot)** and ensured HTTP traffic redirects properly to HTTPS.

- I gained real experience in **debugging and fixing issues in a production-like environment**, especially around SSH access, DNS, and strict validation requirements.

- Overall, I was able to move from just following instructions to actually **understanding and implementing core DevOps practices end-to-end**.

##  Cost Management & Resource Cleanup

To avoid unnecessary cloud charges, the EC2 instance used for this project was **terminated after successful implementation and validation of all requirements**.

This was done after confirming that:

- Nginx was correctly configured and working
- The API endpoint (`/api`) returned the expected JSON response
- HTTPS was properly set up with a valid Let's Encrypt certificate
- SSH access and server configuration were successfully tested

The instance was intentionally shut down to prevent ongoing billing, as this project does not require continuous uptime.

 Note:
The live environment is no longer active. If the domain is accessed, it may not resolve because the EC2 instance has been terminated after successful testing and submission readiness.

## Screenshots:

Launched Instance
![Instance Running](https://github.com/ChideraA080/hng-devops-stage0/blob/main/Hng_Stage0%20Screenshots/HNG%20Nginx.png)

Default Nginx Running On Browser
![Default Nginx Running](https://github.com/ChideraA080/hng-devops-stage0/blob/main/Hng_Stage0%20Screenshots/IMG_20260415_115749.jpg)

Nginx Successfully Configured
![Nginx Success Config](https://github.com/ChideraA080/hng-devops-stage0/blob/main/Hng_Stage0%20Screenshots/1000754172.jpg)

Certificate Encrypt
![Cert Encrypt Success](https://github.com/ChideraA080/hng-devops-stage0/blob/main/Hng_Stage0%20Screenshots/1000754194.jpg)

Domain Testing
![Domain Testing](https://github.com/ChideraA080/hng-devops-stage0/blob/main/Hng_Stage0%20Screenshots/1000754251.jpg)

Author

HNG Username: Pamelaunik

Project: DevOps Stage 0

