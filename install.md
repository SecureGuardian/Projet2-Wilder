## Installation et Configuration de WordPress avec Apache

### 1. Installation d'Apache2
```bash
sudo apt install apache2  
sudo systemctl enable apache2
```

### 2. Activation des modules Apache
```bash
sudo a2enmod rewrite    
sudo a2enmod ssl  
sudo a2enmod deflate  
sudo a2enmod headers  
sudo systemctl restart apache2  
```
### 3. Configuration du serveur Apache
```bash
echo "ServerTokens Prod" | sudo tee -a /etc/apache2/apache2.conf  
```
### 4. Installation de PHP et des extensions nécessaires
```bash
sudo apt install php php-pdo php-mysql php-zip php-gd php-mbstring php-curl php-xml php-pear php-bcmath    
```
### 5. Installation de MariaDB
```bash
sudo apt install mariadb  
sudo mariadb-secure-installation
```
### 6. Téléchargement et installation de Wordpress
```bash
cd /tmp  
wget https://wordpress.org/latest.zip  
sudo rm /var/www/html/index.html  
sudo apt install zip  
sudo unzip latest.zip -d /var/www/html/  
sudo mv /var/www/html/wordpress/* /var/www/html/  
sudo rm -Rf /var/www/html/wordpress/  
sudo chown -R www-data:www-data /var/www/html/    
```
7. Création de la base de données pour Wordpress
```bash
sudo mariadb -e "create database wp202307_projet1cyber; create user 'adminwp202307_projet1cyber'@localhost IDENTIFIED BY 'Notre-super-m0t-de-passe!'; GRANT ALL PRIVILEGES ON wp202307_projetcyber* TO adminwp202307_projet1cyber@localhost; flush privileges; exit;"  
