# Application Central

App Central is a Docker Compose / Python / Flask / NGINX Service

## Note about Sanitization:
This is a sanitized version of my original project.  Unfortunately, due to sanitization, the project no longer functions as expected.

## Installation

Install via Docker

```bash
docker-compose up --build -d
```

## Architecture

App Central is split across 3 GIT Repos.  These include:
1) Installer - Orchestrates building the full application via docker-compose and multiple GIT repo clones.  It will also build a persistent storage location at ./vault/
2) Main Module - Includes login / logout / XXXX connector / HomePage
3) VLXXX Ports Conversion Applet - Converts VLXXX ports to regular data access.  Also includes HTML Email and Sparkbot notifications.

## Installer

This is composed of:
- docker-compose.yml
- a subdirectory of module specific Dockerfiles.

*Note:* No other files need to be manually installed.  The rest of the application will exist inside docker as images and containers.

Persistent storage files will be automatically built and placed inside the "vault" subdirectory.

## Main Module Docker Container

- The main module leverages Nginx as both a web server and reverse-proxy.
- The web content is a Flask Application hosted on Port XXX.
- Initial SSL certificates are self-signed.  These are located in ./vault/global/ and can be swapped with production certs.  Just use the same filenames.
- Path based routing is configured via default.conf which is copied to /etc/nginx/conf.d/default.conf inside of the docker container.
- Auth credentials are confirmed via ldap.
- XXXX credentials are securely cached at ./vault/global/
- Encryption is provided by Fernet.

## VLXXX Ports Docker Container

- The VLXXX Ports applet leverages Nginx as a web server. 
- The web content is a Flask Application hosted on Port XX.  This is not publicly accessible.
- Redis is also embedded and allows asyncronous processing of automated conversion jobs.
- These jobs are Python3 based.
- Governance is enforced via an XXXX integration.  CRs must be provided and must be in implementation state.
- All changes are logged against the user's XXXX credentials to enforce accountability.
- User credentials are securely passed from the web layer to the Python3 layer with Fernet encryption.
- Full pass / fail outputs are delivered to the user's email address.
- Failures (errors) are also reported by the Automation Bot into any Webex Teams room which it has been added.

## Guide

1) First create an empty directory on your server.
2) Confirm both Docker and Docker-compose are pre-installed.
3) GIT clone this repo.
4) Issue "docker-compose up --build -d"
5) Wait for the install process to complete, then go to: https://your_server.domain.com/
6) Login with your XXXX credentials and supply the password for the "XXXXXXXXXXX" account.
7) Select your desired applet from the homepage.
