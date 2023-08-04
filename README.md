# Introduction

The goal of this document is to provide a procedure to strengthen the security of an Apache server hosting WordPress. This procedure is based on the recommendations of the Centre for Internet Security (CIS) Apache Benchmark and the findings from the Lynis audit tool.

## Table of Contents
1. [Overview](#overview)
2. [Team Members](#team-members)
3. [Technology Stack](#technology-stack)
4. [WordPress Hardening](#wordpress-hardening)
5. [Apache Web Server Hardening](#apache-web-server-hardening)
6. [Lynis Audit on Apache - Remediation](#lynis-audit-on-apache-remediation)
7. [Ubuntu Hardening](#ubuntu-hardening)
8. [Lynis Audit on Ubuntu - Remediation](#lynis-audit-on-ubuntu-remediation)

## Overview

This project focuses on the deployment of WordPress on an Ubuntu server and the securing of various components, including WordPress, Apache, and Ubuntu. The team, consisting of three members, diligently collaborated to achieve the project's goals.

## Team Members

### My Role

As the project manager, my responsibilities included:

- Steering the project and ensuring that goals and timelines were met.
- Securing Apache by implementing appropriate measures to protect against potential vulnerabilities.

### Leslie's Role

Leslie was responsible for:

- Installing WordPress on the server.
- Implementing security measures for WordPress to ensure protection against common threats.

### David's Role

David's responsibilities encompassed:

- Securing Ubuntu, taking necessary precautions to make sure the operating system was safe and resistant to attacks.

## Technology Stack

- **WordPress**: Used for website content management.
- **Apache**: Web server used in conjunction with WordPress.
- **Ubuntu**: The operating system on which both WordPress and Apache were deployed.


## I. Apache Web Server Hardening

1. Ensure that the Autoindex module is disabled (Automated)
    ```bash
    root@wild-groupe-02:/# apachectl -M | grep autoindex_module
    root@wild-groupe-02:/#
    ```
    - This command checks if the Autoindex module is enabled.
    - The command to disable Autoindex is:
    ```bash
    root@wild-groupe-02:/# a2dismod -f autoindex
    Module autoindex already disabled
    root@wild-groupe-02:/#
    ```
2. Ensure that Proxy modules are disabled
    ```bash
    root@wild-groupe-02:/# apachectl -M | grep proxy_
    root@wild-groupe-02:/#
    ```
    - This command checks if the Proxy modules are enabled.
    - The command to disable Proxy is:
    ```bash
    root@wild-groupe-02:/# a2dismod proxy
    Module proxy already disabled
    root@wild-groupe-02:/#
    ```
3. Ensure that the Userdir module is disabled (Automated)
    ```bash
    root@wild-groupe-02:/# apachectl -M | grep userdir_
    root@wild-groupe-02:/#
    ```
    - This command checks if the Userdir module is enabled.
    - The command to disable Userdir is:
    ```bash
    root@wild-groupe-02:/# a2dismod userdir
    Module userdir already disabled
    root@wild-groupe-02:/#
    ```
4. Ensure that the Info module is disabled (Automated)
    ```bash
    root@wild-groupe-02:/# apachectl -M | grep 'info_module'
    root@wild-groupe-02:/#
    ```
    - This command checks if the Info module is enabled.
    - The command to disable Info is:
    ```bash
    root@wild-groupe-02:/# a2dismod info
    Module info already disabled
    root@wild-groupe-02:/#
    ```
5. Ensure that Basic and Digest Authentication Modules are disabled
    ```bash
    root@wild-groupe-02:/# apachectl -M | grep auth_basic_module
    root@wild-groupe-02:/#
    ```
    - This command checks if the Basic Authentication module is enabled.
    - The command to disable Basic and Digest Authentication Modules is:
    ```bash
    root@wild-groupe-02:/# a2dismod -f auth_basic
    Module auth_basic already disabled
    root@wild-groupe-02:/# a2dismod -f auth_digest
    Module auth_digest already disabled
    root@wild-groupe-02:/#
    ```
6. Ensure that the Apache user account has an invalid shell (Automated)
    ```bash
    root@wild-groupe-02:~$ useradd apache
    root@wild-groupe-02:~$ chsh -s /sbin/nologin apache
    root@wild-groupe-02:~$ grep apache /etc/passwd
    apache:x:1005:1006::/home/apache:/sbin/nologin
    arafiki@wild-groupe-02:~$
    ```
    - These commands create a new user called "apache", set its shell to "/sbin/nologin" to prevent the user from logging in interactively, then check that the shell has been properly set.
7. Ensure that the Apache user account is locked (Automated)
    ```bash
    root@wild-groupe-02:/home/arafiki# passwd -S apache
    apache L 07/27/2023 0 99999 7 -1
    ```
    - The passwd -S apache command displays the status of the Apache user account.

## II. Lynis Audit on Apache - Remediation

The Lynis audit on Apache raised the following two vulnerabilities:
  the HTTP-6640 flaw - mod_evasive module, and the HTTP-6643 flaw - mod_security module

1. Fix the HTTP-6640 flaw - mod_evasive module:
    Install or update mod_evasive: First check if the mod_evasive module is already installed:
    ```bash
    root@wild-groupe-02:/# apache2ctl -M | grep evasive
    ```
    If not installed, install it:
    ```bash
    root@wild-groupe-02:/# apt update
    root@wild-groupe-02:/# apt install libapache2-mod-evasive
    ```
    If the module is already installed, update it:
    ```bash
    root@wild-groupe-02:/# apt upgrade libapache2-mod-evasive
    ```
    Then restart Apache to apply the changes:
    ```bash
    root@wild-groupe-02:/# service apache2 restart
    ```
    Configure the mod_evasive module: Navigate to the Apache configuration directory for available modules:
    ```bash
    root@wild-groupe-02:/# cd /etc/apache2/mods-available/
    ```
    Enable the mod_evasive module:
    ```bash
    root@wild-groupe-02:/# a2enmod evasive
    ```
    Open the evasive.conf configuration file with a text editor:
    ```bash
    root@wild-groupe-02:/# nano evasive.conf
    ```
    Uncomment the default configurations and add the proposed new values:

    ```
    DOSPageCount   100
    DOSSiteCount   500
    DOSPageInterval   2
    DOSSiteInterval   5
    ```
    Restart Apache to apply the configuration changes:
    ```bash
    root@wild-groupe-02:/# service apache2 restart
    ```
2. Fix the HTTP-6643 flaw - mod_security module:
    Installation of ModSecurity:
    ```bash
    root@wild-groupe-02:/# apt install libapache2-mod-security2
    ```
    Activation of ModSecurity:
    ```bash
    root@wild-groupe-02:/# a2enmod security2
    root@wild-groupe-02:/# service apache2 restart
    ```
## . Ubuntu Hardening  

