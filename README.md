# Introduction

L'objectif de ce document est de fournir une procédure pour renforcer la sécurité d'un serveur Apache qui héberge WordPress. Cette procédure se base sur les recommandations du Centre for Internet Security (CIS) Apache Benchmark et les résultats de l'outil d'audit Lynis.

## Sommaire
1. [Hardening de WordPress](#hardening-de-wordpress)
2. [Hardening de serveur web Apache](#hardening-de-serveur-web-apache)
3. [Audit Lynis sur Apache - Remédiation](#audit-lynis-sur-apache-remediation)
4. [Hardening de Ubuntu](#hardening-de-ubuntu)
5. [Audit Lynis sur Ubuntu - Remédiation](#audit-lynis-sur-ubuntu-remediation)

## Objectif du document

Ce document a pour objectif d'aider les administrateurs système à renforcer la sécurité de leurs serveurs Apache, en se basant sur les recommandations du CIS Apache Benchmark et les résultats d'un audit Lynis.

## I. Hardening de serveur web Apache

1. Assurez-vous que le module Autoindex est désactivé (Automatisé)
    ```bash
    root@wild-groupe-02:/# apachectl -M | grep autoindex_module
    root@wild-groupe-02:/#
    ```
    - Cette commande vérifie si le module Autoindex est activé.
    - La commande pour désactiver Autoindex est : 
    ```bash
    root@wild-groupe-02:/# a2dismod -f autoindex
    Module autoindex already disabled
    root@wild-groupe-02:/#
    ```
2. Assurez-vous que les modules Proxy sont désactivés
    ```bash
    root@wild-groupe-02:/# apachectl -M | grep proxy_
    root@wild-groupe-02:/#
    ```
    - Cette commande vérifie si les modules Proxy sont activés.
    - La commande pour désactiver Proxy est :
    ```bash
    root@wild-groupe-02:/# a2dismod proxy
    Module proxy already disabled
    root@wild-groupe-02:/#
    ```
3. Assurez-vous que le module des répertoires utilisateur est désactivé (Automatisé)
    ```bash
    root@wild-groupe-02:/# apachectl -M | grep userdir_
    root@wild-groupe-02:/#
    ```
    - Cette commande vérifie si le module Userdir est activé. 
    - La commande pour désactiver Userdir est :
    ```bash
    root@wild-groupe-02:/# a2dismod userdir
    Module userdir already disabled
    root@wild-groupe-02:/#
    ```
4. Assurez-vous que le module Info est désactivé (Automatisé)
    ```bash
    root@wild-groupe-02:/# apachectl -M | grep 'info_module'
    root@wild-groupe-02:/#
    ```
    - Cette commande vérifie si le module Info est activé. 
    - La commande pour désactiver Info est :
    ```bash
    root@wild-groupe-02:/# a2dismod info
    Module info already disabled
    root@wild-groupe-02:/#
    ```
5. Assurez-vous que les modules d'authentification Basic et Digest sont désactivés
    ```bash
    root@wild-groupe-02:/# apachectl -M | grep auth_basic_module
    root@wild-groupe-02:/#
    ```
    - Cette commande vérifie si le module d'authentification Basic est activé.
    - La commande pour désactiver Basic et Digest Authentication Modules est :
    ```bash
    root@wild-groupe-02:/# a2dismod -f auth_basic
    Module auth_basic already disabled
    root@wild-groupe-02:/# a2dismod -f auth_digest
    Module auth_digest already disabled
    root@wild-groupe-02:/#
    ```
6. Assurez-vous que le compte utilisateur Apache a un shell non valide (Automatisé)
    ```bash
    root@wild-groupe-02:~$ useradd apache
    root@wild-groupe-02:~$ chsh -s /sbin/nologin apache
    root@wild-groupe-02:~$ grep apache /etc/passwd
    apache:x:1005:1006::/home/apache:/sbin/nologin
    arafiki@wild-groupe-02:~$
    ```
    - Ces commandes créent un nouvel utilisateur appelé "apache", définissent son shell comme "/sbin/nologin" pour empêcher l'utilisateur de se connecter interactivement, puis vérifient que le shell a été correctement défini.
7. Assurez-vous que le compte utilisateur Apache est verrouillé (Automatisé)
    ```bash
    root@wild-groupe-02:/home/arafiki# passwd -S apache
    apache L 07/27/2023 0 99999 7 -1
    ```
    - La commande passwd -S apache affiche l'état du compte utilisateur Apache.

## II. Audit Lynis sur Apache - Remédiation

L'audit Lynis sur Apache remonté les deux failles suivantes :
  la faille HTTP-6640 - mod_evasive module et la faille HTTP-6643 - mod_security module

1. Corriger la faille HTTP-6640 - mod_evasive module : 
    Installer ou mettre à jour mod_evasive : Vérifiez d'abord si le module mod_evasive est déjà installé :
    ```bash
    root@wild-groupe-02:/# apache2ctl -M | grep evasive
    ```
    Si ce n'est pas installé, installez-le :
    ```bash
    root@wild-groupe-02:/# apt update
    root@wild-groupe-02:/# apt install libapache2-mod-evasive
    ```
    Si le module est déjà installé, mettez-le à jour :
    ```bash
    root@wild-groupe-02:/# apt upgrade libapache2-mod-evasive
    ```
    Redémarrez ensuite Apache pour appliquer les changements :
    ```bash
    root@wild-groupe-02:/# service apache2 restart
    ```
    Configurer le module mod_evasive : Accédez au répertoire de configuration d'Apache pour les modules disponibles :
    ```bash
    root@wild-groupe-02:/# cd /etc/apache2/mods-available/
    ```
    Activez le module mod_evasive :
    ```bash
    root@wild-groupe-02:/# a2enmod evasive
    ```
    Ouvrez le fichier de configuration evasive.conf avec un éditeur de texte :
    ```bash
    root@wild-groupe-02:/# nano evasive.conf
    ```
    Décommenter les configurations par défaut et ajouter les nouvelles valeurs proposées :

    ```
    DOSPageCount   100
    DOSSiteCount   500
    DOSPageInterval   2
    DOSSiteInterval   5
    ```
    Redémarrez Apache pour appliquer les changements de configuration :
    ```bash
    root@wild-groupe-02:/# service apache2 restart
    ```
2. Corriger la faille HTTP-6643 - mod_security module :
    Installation de ModSecurity :
    ```bash
    root@wild-groupe-02:/# apt install libapache2-mod-security2
    ```
    Activation de ModSecurity :
    ```bash
    root@wild-groupe-02:/# a2enmod security2
    root@wild-groupe-02:/# service apache2 restart
    ```
