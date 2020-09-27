<div align="center">
  <img src="https://raw.githubusercontent.com/alivx/ansible-cis-nginx-hardening/master/files/nginx.png">
</div>

Ansible CIS Nginx Hardening [![Build Status](https://travis-ci.org/alivx/ansible-cis-nginx-hardening.svg?branch=master)](https://travis-ci.org/alivx/ansible-cis-nginx-hardening)  (still under Testing Phase)
=========

Based on CIS NGINX Benchmark v1.0.0 - 02-28-2019

Nginx is arguably one of the most widely used free and opensource web server used in hosting high-traffic websites. It is well known for its stability, stellar-performance, low resource consumption, and lean configuration.
The default configurations are not secure and extra tweaks are required to fortify the web server and give it the much-needed security to prevent attacks and breaches, So this role establish secure configuration posture for NGINX running on Ubuntu


### Scoring Information
* A scoring status indicates whether compliance with the given recommendation impacts the assessed target's benchmark score. The following scoring statuses are used in this benchmark:
### Scored (implemented in this role)
* Failure to comply with "Scored" recommendations will decrease the final benchmark score. Compliance with "Scored" recommendations will increase the final benchmark score.
### Not Scored (not implements in this role)
* Failure to comply with "Not Scored" recommendations will not decrease the final benchmark score. Compliance with "Not Scored" recommendations will not increase the final benchmark score.

---
### The main benefits of using NGINX packages from your vendor are:
* Ease of installation
* Dependency resolution
* Increased effectiveness of maintenance and security patches
* Q&A procedures carried out by your vendor
---

Requirements
------------

Since this role will install the latest Nginx package from the OS repository, make sure to run this role in fresh nginx server, this will handle the installation process.

It may work if you already install nginx in your server.

---
Role Variables
--------------

config as following
```Yaml
large_client_header_buffers: "2 1k"
client_max_body_size: "100K"
client_body_timeout: 10
client_header_timeout: 10
strict_transport_security_max_age: 15768000 #max-age directive with 15768000 seconds (six months) or longer
nginx_site_config_dir: /etc/nginx/sites-available/
#Or ALL:!EXP:!NULL:!ADH:!LOW:!SSLv2:!SSLv3:!MD5:!RC4;
ssl_ciphers: ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-RSA-CHACHA20-POLY1305:DHE-RSA-AES128-GCM-SHA256:DHE-RSA-AES256-GCM-SHA384


nginx_key: /etc/ssl/private/nginx-selfsigned.key
nginx_cert: /etc/ssl/certs/nginx-selfsigned.crt

backendserver: http://localhost:3000
backendserver_ssl: True

access_log: /var/log/nginx/alivx.com.access.log
error_log: /var/log/nginx/alivx.com.error.log warn

domainName: 172.16.186.129
```

----
Dependencies
------------


-

---
Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```Yaml
---
- hosts: host1
  become: yes
  remote_user: root
  gather_facts: no
  roles:
    - { role: "ansible-cis-nginx-hardening" }

```

---
### Benchmarks

* 1 Initial Setup
* 1.1 Installation
* 1.1.1 Ensure NGINX is installed (Scored)
* 1.2 Configure Software Updates
* 2 Basic Configuration
* 2.1 Minimize NGINX Modules
* 2.1.2 Ensure HTTP WebDAV module is not installed (Scored)
* 2.1.3 Ensure modules with gzip functionality is disabled (Scored)
* 2.1.4 Ensure the autoindex module is disabled (Scored)
* 2.2 Account Security
* 2.2.2 Ensure the NGINX service account is locked (Scored)
* 2.2.3 Ensure the NGINX service account has an invalid shell (Scored)
* 2.3 Permissions and Ownership
* 2.3.1 Ensure NGINX directories and files are owned by root (Scored)
* 2.3.2 Ensure access to NGINX directories and files is restricted (Scored)
* 2.3.3 Ensure the NGINX process ID (PID) file is secured (Scored)
* 2.4 Network Configuration
* 2.4.1 Ensure NGINX only listens for network connections on authorized ports (NotScored)
* 2.4.3 Ensure keepalive_timeout is 10 seconds or less, but not 0 (Scored)
* 2.4.4 Ensure send_timeout is set to 10 seconds or less, but not 0 (Scored)
* 2.5 Information Disclosure
* 2.5.1 Ensure server_tokens directive is set to `off` (Scored)
* 2.5.2 Ensure default error and index.html pages do not reference NGINX (Scored)
* 2.5.4 Ensure the NGINX reverse proxy does not enable information disclosure (Scored)
* 3 Logging
* 3.2 Ensure access logging is enabled (Scored)
* 3.3 Ensure error logging is enabled and set to the info logging level (Scored)
* 3.4 Ensure log files are rotated (Scored)
* 3.7 Ensure proxies pass source IP information (Scored)
* 4 Encryption
* 4.1 TLS / SSL Configuration
* 4.1.1 Ensure HTTP is redirected to HTTPS (Scored)
* 4.1.3 Ensure private key permissions are restricted (Scored)
* 4.1.4 Ensure only modern TLS protocols are used (Scored)
* 4.1.5 Disable weak ciphers (Scored)
* 4.1.6 Ensure custom Diffie-Hellman parameters are used (Scored)
* 4.1.7 Ensure Online Certificate Status Protocol (OCSP) stapling is enabled (Scored)
* 4.1.8 Ensure HTTP Strict Transport Security (HSTS) is enabled (Scored)
* 4.1.10 Ensure upstream server traffic is authenticated with a client certificate (Scored)
* 4.1.13 Ensure session resumption is disabled to enable perfect forward security (Scored)
* 5 Request Filtering and Restrictions
* 5.1 Access Control
* 5.2 Request Limits
* 5.2.1 Ensure timeout values for reading the client header and body are set correctly (Scored)
* 5.2.2 Ensure the maximum request body size is set correctly (Scored)
* 5.2.3 Ensure the maximum buffer size for URIs is defined (Scored)
* 5.3 Browser Security
* 5.3.1 Ensure X-Frame-Options header is configured and enabled (Scored)
* 5.3.2 Ensure X-Content-Type-Options header is configured and enabled (Scored)
* 5.3.3 Ensure the X-XSS-Protection Header is enabled and configured properly (Scored)

---

License
-------

GNU GENERAL PUBLIC LICENSE

Author Information
------------------

The role was originally developed by [Ali Saleh Baker](https://www.linkedin.com/in/alivx/).

When contributing to this repository, please first discuss the change you wish to make via a GitHub issue,  email, or via other channels with me :)