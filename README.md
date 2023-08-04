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

### O. WordPress Hardening

## What is the Importance of Security for a WordPress Site?

The security of your site is paramount. In case of hacking, the consequences can be very unfortunate and result in:
- the loss and theft of numerous data, more or less sensitive, especially those of your customers.
- a waste of time, as you will have to clean the hacked site and update everything.
- unforeseen financial expenses, especially if you hire a security expert.
- degradation of your brand image and possible loss of trust from your current users and/or your future customers.
- Keep in mind that this kind of mishap does not only happen to others.

## Statistics and Types of Attacks

A quick visit to the presentation page of iThemes Security Pro may be enough to convince you (if you are the stubborn type). According to the data that the company communicates:
- 50% of cyber-attacks would target very small businesses;
- 45% of site owners would not be sufficiently prepared to undergo a hacking, in the sense that they have not put in place sufficient protection measures.
- As the security expert Patchstack indicates in a report published in 2021, almost all detected vulnerabilities come from themes and especially WordPress plugins (99.42% of total flaws). The attacks can be multiple and varied.
- You can be targeted by:
  - Cross-site scripting (also called XSS).
  - Cross site request forgery (CSRF or XSRF).
  - SQL injections (attacks on your database).
  - PHP vulnerabilities, the language under which WordPress runs.
  - downloads of malicious files, etc.

## Securing WordPress

Some settings to be made in the settings -> ssl tab:
- Prevent the execution of code in the public "Uploads" folder
- Hide the version of Wordpress
- Disable account enumeration
- Block the registration of Internet users when the displayed username and name are identical
- .htaccess 301 redirection method

## iThemes Security

### What is iThemes Security?

iThemes Security is an extension to protect and secure your WordPress site. It offers different features for this, among which:
- two-factor authentication
- protection against brute force attacks
- password strengthening
- IP blocking, etc.

With 900K active installations, iThemes Security is one of the most popular security plugins on the official WordPress directory.

### To Protect Your Installation

To protect your installation as much as possible, the free version of iThemes is notably able to:
- ban the IP addresses of hackers or malicious robots (bots) who wish to access your website.
- backup the database of your WordPress installation.
- detect any unauthorized change made to your files.
- block brute force attacks. In this case, robots (bots) try to discover the username and password of the administrator account of your site by testing different combinations, in order to take control.
- help you implement two-factor authentication to connect to your site.
- impose the implementation of strong passwords for all accounts.
- require connection to your site via SSL, mandatory to implement HTTPS on your site.
- send you email notifications of any suspicious activity on your site.
- change the prefix of your website's database.
- modify the URL of your login page.

However, do not consider iThemes Security as a magic formula to protect you 100%. No security extension can guarantee that, by the way.

### Change the Login URL

Why modify the login URL of your WordPress console?
- The login URL to your administration interface at its value is by default: yoursite.com/wp-admin
- Hackers, pirates, and other Web thugs know very well that the website is under WordPress, how? Here is one of the 3 methods used to know:
  - View the source code of a page on your website to spot multiple references to "WP", i.e. WordPress.
  - look in the footer of the site to see if a WordPress theme is mentioned.
  - simpler, with automatic detection tools of the technology used on a site, like Wappalyzer.

Once the hacker knows that your site is under WordPress, the next step is to find the WordPress administration page.

Then it's intrusion by "Brute Force" to find the password and surely other tricks.

"Brute Force" type attacks are apparently the simplest method to access a website's administration. They consist of running a computer program to try thousands of combinations of username and password, over and over, until they find the right one.

Obviously, this task is greatly facilitated if the hackers know the login URL to your WordPress console.
That's why, it is strongly recommended not to keep the default URL. Thus, you greatly complicate their task.
So, at least, make life difficult for hackers by preventing them from finding your WordPress admin access page too easily!

In iThemes Security, in the advanced menu, the third tab, "Move the login page", allows you to change the login page to the administration of your site. By default, you can easily access it by entering one of the two URLs below in a web browser:
- yoursite.fr/wp-admin
- yoursite.fr/wp-login.php

By modifying it, you make the job of bots that want to connect to your site more complex. The settings allow you to:
- Change the login slug, i.e., the last part of your URL. Enter the value of your choice (e.g., xc78ygvk).
- Prefer a combination that is difficult to guess and remember to note your new URL in several places (in your note app, in your browser's favorites, etc.).
- Specify a redirect URL (e.g., https://yoursite.fr/404), to which unconnected bots or hackers wishing to access your login page will be sent. Check the associated box if you want to take advantage of this option.

### Hide the WordPress Version

WordPress by default inserts a meta tag containing the WordPress version number. This meta-element identifies the version of WordPress you are currently using and is used for tracking purposes.

Unbeknownst to you, the WordPress version number reveals additional information about your website. WordPress tracks changes in detailed reports every time it publishes updates or fixes issues. This means that everyone knows which versions are affected by which security flaws. Specifically, this implies that hackers know the best type of attack to deploy on your site. For this reason, it is crucial to hide your version number. By merely looking at your website's source code in any web browser, any hacker can discover the WordPress version you are using.

How does a hacker search for your WordPress version?
- Observing the source of your website's page.
- By obtaining your RSS feed.
- By browsing your readme file.

### Hide the WP Version Using a Plugin

The WP Security Safe plugin will be used to demonstrate the method for hiding your WordPress version. With this plugin, you can hide your WordPress version number without any coding. This is especially useful if you do not know how to access your website's theme files or if you want to avoid accidental mistakes.

Follow these steps to hide your WordPress version:
1. Install and activate the WP Security Safe plugin from the WordPress repository.
2. In your WordPress dashboard, go to Security -> WP Security Safe.
3. In the WP Security Safe settings, click on the tab labeled “WordPress.”
4. Check the box next to "Remove WP Version."
5. Click “Save Changes.”

Now, your WordPress version number should be removed from all locations, including the head section, RSS feeds, and the readme file.

This method is much more straightforward than manually editing your theme's files, and it's reversible. If you want to display your WordPress version number again, simply uncheck the box and save your changes.

## Disable XML-RPC

In recent years, XML-RPC has become an increasingly significant target for brute force attacks. One of the hidden features of XML-RPC is that you can use the system.multicall method to execute multiple methods within a single request. This is very useful because it allows the application to pass multiple commands within an HTTP request. But what also happens is that it is used for malicious purposes.

### Plugins and Tools

There are a few WordPress plugins like Jetpack that rely on XML-RPC, but most people won't need it, and it may be beneficial simply to disable access. Don't know if XML-RPC is currently working on your website? Danilo Ercoli from the Automattic team wrote a small tool called XML-RPC Validator. You can run your WordPress site through this to see if XML-RPC is enabled. If not, you will see a failure message.

### How to Disable XML-RPC

To completely disable this function, you can install the free Disable XML-RPC-API extension. Or you can disable it with the premium perfmatters extension, which also contains web performance improvements.

The installation of an extension to disable xmlrpc.php is the simplest way to proceed. The Disable XML-RPC extension will disable it completely.

Once installed, You have nothing else to do: activating the extension will result in the deactivation of XML-RPC.

## WPS Limit Login

WPS Limit Login allows you to limit login attempts to your WordPress administration.

It consists of 4 blocks:
- Configuration
- Whitelist: Define a list of IP addresses that will have no attempt limit and will never be blocked. Be careful; you must put trusted IP addresses (e.g., your home IP address); you must never put the IP address of a public network (Cyber cafe or other).
- Blacklist: Define a list of IP addresses for which you want to completely block access to the login page.
- Blocking log

### Connection and Display Names Must Be Different for WordPress

Login or user names can be the same as your display name on the front-end, such as the author of a blog post. Or available in an RSS feed, etc. This creates instant vulnerability because your login name is available to everyone.

#### Edit Your Display Name

You can change the full names, but the options are limited because they are based on the first entries when creating the user. Go to the accounts tab and change the name to be displayed publicly.

### Regularly Update Your Site and Your Plugins

Another vital way to strengthen your WordPress security is to always keep it up to date. This includes the WordPress core, plugins, and themes (those in the WordPress repository and those that are Premium). These are updated for a reason, and they often include security improvements and bug fixes.

### Generate an SSL Certificate

An SSL certificate (Secure Socket Layer) is a means of securing communications between a browser and a web server. It allows for the encryption of sensitive data transmitted between the two, such as the information...

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
## III. Ubuntu Hardening
## Summary

1. [General principles of security and hardening](#general-principles-of-security-and-hardening)
2. [The sudo command](#the-sudo-command)
3. [Openssh](#openssh)
4. [Iptables](#iptables)
5. [Nfables](#nfables)
6. [Fail2Ban](#fail2Ban)
7. [Certificate SSL/TLS](#certificate-ssl-/-tls)
8. [Anti-virus](#anti-virus)
9. [Lynis Audit on Ubuntu - Remediation](#lynis-audit-on-ubuntu-remediation)

### General principles of security and hardening

**Principle of minimization** 
This principle states that systems designed and installed should avoid unnecessary complexity as much as possible in order to:
- reduce the attack surface to a strict minimum;
- allow efficient updating and monitoring of systems;
- make the system monitoring activity more accessible, insofar as the number of components to be monitored is reduced. The implementation of this principle is sometimes tricky because it can quickly find itself in contradiction with other equally important ones. Only a case study with the help of system and security expertise will make it possible to make reasonable choices. The following chapters will give recommendations targeted according to the considered parts of the system.

**Principle of least privilege** 
This principle defines that any object or entity managed by a system has only the rights strictly necessary for its execution, and nothing more. The objective is both a gain in safety and security:
- the consequences of malfunctions or vulnerabilities are limited to the privileges granted;
- the alteration or compromise of the system requires an escalation of privileges, less trivial and discreet to achieve in cases where several layers of protection are put in place.

**Principle of defense in depth** 
This principle requires the design of several independent and complementary security layers in order to delay an attacker whose objective is to compromise the system. Each layer of security is therefore an additional point of resistance that the attacker must overcome. The failure of a layer is accompanied by signals, alarms or logged events making it possible to detect suspicious activity and to be able to react to it. The remediation step is also facilitated thanks to the additional aggregated information on the context of the compromise. This principle therefore has a real advantage: detection, ease of remediation, and improved security. Under Unix operating systems and derivatives, defense in depth must be based on a combination of barriers that must be kept independent of each other.

### The sudo command
The sudo (Super User DO) command in Linux is usually used as a prefix for certain commands that only superusers are allowed to run. If you prefix a command with "sudo" it will run that command with elevated privileges or, in other words, allow a user with the appropriate permissions to run a command as another user, such as superuser (root). This is the equivalent of the "run as administrator" option in Windows. The sudo option allows us to have multiple administrators. Those users who can use the sudo command must have an entry in the sudoers file located in "/etc/sudoers". Remember that to modify or view the sudoers file, you must use the sudo command. To edit the sudoers file, it is recommended to use the "visudo" command. By default, sudo requires users to authenticate with a password which is the user's password, not the root password itself. As an initial action in installing, configuring and securing the Linux machine, we introduced a line for each user with privileges identical to the privileges of the superuser (root). Extract from /etc/sudoers file:

**leslie	ALL=(ALL:ALL) ALL**
**arakifi	ALL=(ALL:ALL) ALL**
**CDavid	ALL=(ALL:ALL) ALL**

If we write the following command we can see the syntax, options and operation:
```bash
root@wild-groupe-02:~$ sudo -h 
```

**create home directories for existing users:**
```bash
root@wild-groupe-02:~$ sudo usermod -m -d /home/leslie leslie
root@wild-groupe-02:~$ sudo usermod -m -d /home/CDavid CDavid
root@wild-groupe-02:~$ sudo usermod -m -d /home/arakifi arakifi
```

**Sources:** 
[sudo command in Linux with Examples](https://www.geeksforgeeks.org/sudo-command-in-linux-with-examples/)

### Openssh
OpenSSH is the first connectivity tool for remote login with the SSH protocol. It encrypts all traffic to eliminate eavesdropping, connection hijacking, and other attacks. Additionally, OpenSSH provides a wide range of secure tunneling features, multiple authentication methods, and sophisticated configuration options. The SSH protocol was designed with the objective of replacing the various unencrypted protocols like rlogin, telnet, rcp and rsh.

**Installation**

Installing OpenSSH client and server applications is simple. To install OpenSSH client applications on your Ubuntu system, type this command in a terminal:

```bash
root@wild-groupe-02:~$ sudo apt install openssh-client
```

To install the OpenSSH server and necessary files, use this command in a terminal:
```bash
root@wild-groupe-02:~$ sudo apt install openssh-server
```

**Configuration**

You can configure the default behavior of the OpenSSH server, sshd, by modifying the file **/etc/ssh/sshd_config.**
We changed the parameters:
 
- Port 2022
- AllowUsers CDavid, leslie, arakifi

**Sources:** 
[OpenSSH](https://www.openssh.com/)
[OpenSSH Wiki](https://fr.wikipedia.org/wiki/OpenSSH)
[Arch Linux OpenSSH(Français)](https://wiki.archlinux.org/title/OpenSSH_(Fran%C3%A7ais))

### Iptables
The Iptables Linux firewall is used to monitor incoming and outgoing traffic to a server and filter it based on user-defined rules, to prevent anyone from gaining access to the system. Using Iptables, you can set rules that will only allow selected traffic on your server.

**Installation**
To avoid conflict with other existing firewalls, before installing iptables you must uninstall the existing firewall, in my case "ufw" with the command:

```bash
root@wild-groupe-02:~$ sudo apt purge ufw
```

Check if iptables is already installed:
```bash
root@wild-groupe-02:~$ sudo iptables -L -v
```

If iptable is installed we will see the table:
```bash
Chain INPUT (policy ACCEPT 0 packets, 0 bytes)
pkts bytes target     prot opt in     out     source             destination         
 
Chain FORWARD (policy ACCEPT 0 packets, 0 bytes)
pkts bytes target     prot opt in     out     source             destination         
 
Chain OUTPUT (policy ACCEPT 0 packets, 0 bytes)
pkts bytes target     prot opt in     out     source             destination
```

Otherwise you can install iptables with the commands:
```bash
root@wild-groupe-02:~$ sudo apt-get update
root@wild-groupe-02:~$ sudo apt-get install iptables
```

**Configuration**
Defining a rule means adding it to the chain. Here is the iptables command formatted with regular options. We have created a configuration file to install the iptables rules - File **firewall.sh**

```bash
#! /bin/bash

#flush
iptables -F

#loopback
iptables -A INPUT -i lo -j ACCEPT
iptables -A OUTPUT -o lo -j ACCEPT

#ssh

iptables -A INPUT  -p tcp --dport 22 -j ACCEPT
iptables -A OUTPUT -j ACCEPT


iptables -A INPUT -s 93.5.163.229 -d  167.71.39.182  -p tcp --dport 2022 -j ACCEPT
iptables -A OUTPUT -j ACCEPT

iptables -A INPUT -s 88.180.114.84 -d 167.71.39.182  -p tcp --dport 2022 -j ACCEPT
iptables -A OUTPUT -j ACCEPT

iptables -A INPUT -s 176.150.94.8 -d  167.71.39.182  -p tcp --dport 2022 -j ACCEPT
iptables -A OUTPUT -j ACCEPT


#http
iptables -A INPUT -p tcp -d  167.71.39.182  --dport 80 -j ACCEPT
iptables -A OUTPUT -j ACCEPT

#https

iptables -A INPUT -p tcp -d  167.71.39.182  --dport 443 -j ACCEPT
iptables -A OUTPUT -j ACCEPT


#forward
iptables -A  FORWARD  -j ACCEPT


#block
iptables -P INPUT DROP
iptables -P FORWARD ACCEPT
iptables -P OUTPUT DROP

```
### Nftables
Nftables is a tool that allows you to do network filtering and take control of the incoming / outgoing flow on our machine. Available since Linux kernel 3.13, nftables is gradually replacing the aging {ip,ip6,arp,eb}tables- It has several significant advantages over iptables. Here are some of the major improvements:
- Less code duplication / Better written / Fully 64-bit compatible
- Better performance
- A single tool to manage all network layers
- Better handling of dynamic rule reloading
- Faster packet classification
- Several actions possible per rule (Impossible for iptables to block a packet and to log in a single rule)

**Installation**
At the time of writing this report, nftables is in version 1.01. Version 1.0.0 (first stable version) was released in August 2021. If you are using a version of RedHat/CentOS greater than version 8 and a version of Debian greater than or equal to version 10 (Buster) or ubuntu: Good news ! nftables is already installed and is the default solution offered to manage the firewall rules applied by NetFilter. Otherwise you can consult the official site: [nftables](https://git.netfilter.org/nftables/)

**Configuration**

**Tables**

**syntax:** nft [action] table [familly] [table_name] 

**nft:** Tool name.
**action:** Possible values (add, create, delete, list).
**table:** Type of object on which the action is based.
**familly:** Table familly type (see table below).
**table_name:** table name (variable). 

| nftables family |     iptables utility     |
|-----------------|--------------------------|
| ip              | iptables                 |
| ip6             | ip6tables                |
| inet            | iptables and ip6tables   |
| arp             | arptables                |
| bridge          | ebtables                 |
(see Tables of hooks and table family)

**Chains**

There are two types of chaines:
- **Base chain** – There is no pre-defined chain (INPUT / OUTPUT / FORWARD) as in iptables, so you have to create the chain to which you will attach a hook (place in the flow of a program to be intercepted by a function – in our case the function that manages our chain)
- **Regular chain** – Does not have a hook. By definition is not traversed but it can be used to process packets.

**Base chain**

**(action - add)**
**syntax:** nft add chain [table_familly] [table_name] [chain_name] { [chain_details] }

**nft:** Tool name.
**action:** The action in this case is add
**chain:** The object to add
**table_familly:**  Table familly type
**table_name** Table name.
**chain_name:** Chain name (variable).  

**Chain details**

**syntax:** type [chain_type] hook [chain_hook]  priority  [priority] ; policy [policy] ;

**type:** parameter name(type)
**chain_type:** Type of chaine (filter, nat, route)
**hook:** The hook in which the chain will claw (to be executed)
**chain_hook:** type de hook (input, output, forward)
**priority:* Rules evaluation priority (number: order ASC)
**policy:** The action to be taken when matching (drop, reject, accept)

(voir Tableaux des types de chaines et famille de table)

**(action - delete)**
**syntax:** nft delete chain [table_familly] [table_name] [chain_name]

**nft:**  Tool name.
**action:** The action in this case is delete
**chain:**  The object to delete
**table_familly:** Table familly type
**table_name:** Table name.
**chain_name:** Chain name (variable). 

**Regular chain**
**(action - add)**
**syntax:** nft add chain [table_familly] [table_name] [chain_name] 

**nft:** Tool name.
**action:** The action in this case is add
**chain:**  The object to add
**table_familly:** Table familly type
**table_name:** Table name.
**chain_name:** Chain name (variable). 


**(action - delete)**
**syntax:** nft add chain [table_familly] [table_name] [chain_name] 

**nft:** Tool name.
**action:** The action in this case is delete
**chain:**  The object to delete
**table_familly:** Table familly type
**table_name:** Table name.
**chain_name:** Chain name (variable). 

**Rules**
Determine action on packets based on convergence criteria
**(action - add)**
**syntax:** nft add rule [table_name] [chain_name] [parameters] 

**nft:** Tool name.
**action:** The action in this case is add
**rule:** The object to add
**table_name:** Table name.
**chain_name:** Chain name (variable). 
**parameters:** rule settings 

(see Main rule settings)


**
Tables of hooks and table family**:                            
|   main hooks            |   Table family              |   Role                                 |
|-------------------------|-----------------------------|----------------------------------------|
|   prerouting            | Bridge, ip, ipv6,inet       |  Packets arriving at the machine       |
|   postrouting           | Bridge, ip, ipv6, inet      |  Packets leaving the machine           |
|   forward               | Bridge, ip, ipv6, inet      |  Routed packets                        |
|   input                 | Arp, bridge, ip, ipv6, inet |  Packets destined for the machine      |
|   output                | Arp, bridge, ip, ipv6, inet |  Packets sent by the machine           |


**Tables of chain types and table family**:                            
|   Main types            |   Table family              |   Role                                 |
|-------------------------|-----------------------------|----------------------------------------|
|   prerouting            | Bridge, ip, ipv6,inet       |  Packet filtering                      |
|   postrouting           | Bridge, ip, ipv6, inet      |  Packages leaving the machine          |
|   forward               | Bridge, ip, ipv6, inet      |  Routed packets                        |
|   input                 | Arp, bridge, ip, ipv6, inet |  Packets destined for the machine      |
|   output                | Arp, bridge, ip, ipv6, inet |  Packets sent by the machine           |


**Main rule settings**:    
|           Setting                         |         Value                                      |
|-------------------------------------------|----------------------------------------------------|
|        Ip /tcp /udp/ icmp                 |         Protocol IP, TCP, UDP ou ICMP              |
|        iif                                |         Input interface name                       |
|        saddr                              |         Source address                             |
|        sport                              |         Source port                                |
|        snat                               |         Source adress translation                  |
|        oif                                |         Output interface name                      |
|        daddr                              |         Destination address                        |
|        dport                              |         Destination port                           |
|        dnat                               |         Destination adress translation             |
|        drop ou accept                     |         Block or Allow                             |
|        masquerade                         |         Automatic replacement of the source address by the data output address |



The nftables configuration file **(/etc/nftables.conf)**: 
```bash
#!/usr/sbin/nft -f

#flush ruleset

#table inet filter {
#       chain input {
#               type filter hook input priority 0;
#       }
#       chain forward {
#               type filter hook forward priority 0;
#       }
#       chain output {
#               type filter hook output priority 0;
#       }
#}

flush ruleset

add table inet firewall

add chain inet firewall input_chain {
        type filter hook input  priority 0 ; policy drop ;

}
add chain inet firewall forward_chain {
        type filter hook forward  priority 0 ; policy accept ;

}
add chain inet firewall output_chain {
        type filter hook output priority 0 ; policy accept ;

}


add rule inet firewall input_chain iif lo accept



add rule inet firewall input_chain tcp dport 2022 ip saddr 93.5.163.229 ip daddr 167.71.39.182 accept

add rule inet firewall input_chain tcp dport 2022 ip saddr 88.180.114.84 ip daddr 167.71.39.182 accept

add rule inet firewall input_chain tcp dport 2022 ip saddr 176.150.94.8 ip daddr 167.71.39.182 accept

add rule inet firewall input_chain udp dport 53  accept

add rule inet firewall input_chain tcp dport 53 accept

add rule inet firewall input_chain tcp dport 80  accept

add rule inet firewall input_chain tcp dport 443  accept

add rule inet firewall input_chain icmp type echo-reply accept

```

**Sources:** 
[Nftables basics](https://www.cyrilaudras.fr/index.php/informatique/services-reseau/110-les-bases-de-nftables)
[Nftables tutorial](https://www.youtube.com/watch?v=lHLPZlZLWgs)

### Fail2Ban
Fail2ban is an application that analyzes the logs of various services (SSH, Apache, FTP, etc.) by looking for matches between patterns defined in its filters and the log entries. When a match is found one or more actions are executed. Typically, fail2ban looks for repeated failed login attempts in the log files and performs a ban by adding a rule to the iptables or nftables firewall to ban the source IP address.

**Installation**

```bash
root@wild-groupe-02:~$ sudo apt-get install fail2ban
``` 

**Configuration**
After installation, the configuration will be made in the directory **/etc/fail2ban/**
We have different configuration files but what interests us the most is the **“jail.conf”** file. This file allows us to describe how our different “prisons" will behave. It is always crashed when we do a fail2ban update, so we are going to make a backup called **“jail.local”**
```bash
root@wild-groupe-02:~$ cp jail.conf jail.local
```

Edit the jail.local file:
```bash
ignoreip = 127.0.0.1/8 ::1
bantime  = 60m
findtime  = 10m
maxretry = 7
destemail = davidcohen11@hotmail.com
action = %(action_mw)s

…

[sshd]

# To use more aggressive sshd modes set filter parameter "mode" in jail.local:
# normal (default), ddos, extra or aggressive (combines all).
# See "tests/files/logs/sshd" or "filter.d/sshd.conf" for usage example and det>
#mode   = normal

port    = 2022
logpath = %(sshd_log)s
backend = %(sshd_backend)s
maxretry = 5
```

redemarrer:
```bash
root@wild-groupe-02:~$ sudo service fail2ban restart
```

voir l'etat:
```bash
root@wild-groupe-02:~$ sudo fail2ban-client status [jail]
```

example:
```bash
root@wild-groupe-02:~$ sudo fail2ban-client status sshd
```

unbanish:
```bash
root@wild-groupe-02:~$ sudo fail2ban-client set [jail] unbanip [ipaddr]
```

example:
```bash
root@wild-groupe-02:~$ sudo fail2ban-client set sshd unbanip 192.168.1.80
```
### Certificat SSL/TLS
For the certificate we used Certbot. Certbot is a free, open-source software tool for automatically using Let's Encrypt certificates on manually administered websites to enable HTTPS. Certbot is created by the Electronic Frontier Foundation (EFF), a 501(c) non-profit organization 3 based in San Francisco, Calif., which champions digital privacy, freedom of expression and innovation.

**Installation**
1) SSH into the server. SSH into the server running your HTTP website as a user with sudo privileges.

2) Install snapd - You will need to install snapd and be sure to follow the instructions to enable classic snapd support.
(in our distribution, snap is pre-installed)

3) Remove certbot-auto and all Certbot OS packages. If you have Certbot packages installed using an OS package manager like apt, dnf, or yum, you should remove them before installing the Certbot snap-in to ensure that when you run the certbot command, the snap-in is used rather than installing from your operating system package. director. The exact command to do this depends on your operating system, but common examples are sudo apt-get remove certbot, sudo dnf remove certbot, or sudo yum remove certbot.

4) Install Certbot
Run this command on the command line on the machine to install Certbot.
    ```bash
    root@wild-groupe-02:~$ sudo snap install --classic certbot
    ```

5) Prepare the Certbot order
Run the following statement on the command line on the machine to ensure that the certbot command can be run.
    ```bash
    root@wild-groupe-02:~$ sudo ln -s /snap/bin/certbot /usr/bin/certbot
    ```

6) Choose how you want to run Certbot
Either get and install your certificates... Run this command to get a certificate and have Certbot automatically modify your apache config to serve it, enabling HTTPS access in one step.
    ```bash
    root@wild-groupe-02:~$ sudo certbot -- apache
    ```
    Or, just get a certificate

    If you feel more conservative and want to make the changes to your apache config by hand, run this command.
    ```bash	
    root@wild-groupe-02:~$ sudo certbot certonly –apache
    ```
7) Test auto-renewal. Your system's Certbot packages come with a cron job or systemd timer that will automatically renew your certificates before they expire. You won't need to run Certbot again unless you change your configuration. You can test the automatic renewal of your certificates by running this command:
    ```bash
    root@wild-groupe-02:~$ sudo certbot renouveler --dry-run
    ```

    The certbot renewal command is installed in one of the following locations:
    
    /etc/crontab/
    /etc/cron.*/*
    timers de liste systemctl

8) Confirm that Certbot worked. To confirm that your site is set up correctly, visit "https://yourwebsite.com/" in your browser and look for the lock icon in the URL bar.

**Sources:**
[Certbot](https://certbot.eff.org/instructions?ws=apache&os=ubuntufocal)

### Anti-virus
ClamAV (“Clam AntiVirus”), is anti-virus software for UNIX systems. It is generally used with email servers to filter emails. ClamAV is one of the few antiviruses available under GNU/Linux and MacOS. The targeted viruses are mainly viruses attacking the Microsoft Windows operating system, and not the systems on which ClamAV is installed. The antivirus engine is the libclamav library, written in C, C++.

**Installation**
```bash
root@wild-groupe-02:~$ sudo apt install clamav
 ```
 
**Utilisation**
ActionCommandUpdate anti-virus definitions
```bash
root@wild-groupe-02:~$ freshclam
```
Scan files from home folder
```bash
root@wild-groupe-02:~$ clamscan
```
Scan all files in home folder (with -r "Scan subdirectories recursively")
```bash
root@wild-groupe-02:~$ clamscan -r /home/utilisateur
```
Scan the entire hard drive
```bash
root@wild-groupe-02:~$ clamscan -r /
```
Scan a Windows partition (Fat 32), mounted in "/mnt/D". Audible signal and display if virus found and writing to virus.log
```bash
root@wild-groupe-02:~$ clamscan --bell -r -i --log=/home/utilisateur/virus.log /mnt/D/
```

# IV. Lynis Audit on Ubuntu - Remediation

**Command for lauching Lynis:**
```bash 
	root@wild-groupe-02:~$ sudo lynis audit system
```

```bash
 -[ Lynis 3.0.7 Results ]-

  Warnings (2):
  ----------------------------
  ! Found some information disclosure in SMTP banner (OS or software name) [MAIL                                                                                                                                                  -8818]
      https://cisofy.com/lynis/controls/MAIL-8818/

  ! iptables module(s) loaded, but no rules active [FIRE-4512]
      https://cisofy.com/lynis/controls/FIRE-4512/

```

**resolutions:**

iptables module(s) loaded, but no rules active [FIRE-4512]

```bash 
root@wild-groupe-02:~$ sudo apt purge iptables

```

