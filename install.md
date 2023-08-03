# Installation d'Apache2
sudo apt install apache2
sudo systemctl enable apache2

# Activation des modules Apache
sudo a2enmod rewrite
sudo a2enmod ssl
sudo a2enmod deflate
sudo a2enmod headers
sudo systemctl restart apache2

# Configuration du serveur Apache
echo "ServerTokens Prod" | sudo tee -a /etc/apache2/apache2.conf

# Installation de PHP et des extensions nécessaires
sudo apt install php
sudo apt install -y php-pdo php-mysql php-zip php-gd php-mbstring php-curl php-xml php-pear php-bcmath

# Installation de MariaDB
sudo apt install mariadb
sudo mariadb-secure-installation

# Téléchargement et installation de Wordpress
cd /tmp/
wget https://wordpress.org/latest.zip
sudo rm /var/www/html/index.html
sudo apt install zip
sudo unzip latest.zip -d /var/www/html/
sudo mv wordpress/* /var/www/html/
sudo rm wordpress/ -Rf
sudo chown www-data:www-data /var/www/html/ -R

# Création de la base de données pour Wordpress
sudo mariadb -e "create database wp202307_projet1cyber; create user 'adminwp202307_projet1cyber'@localhost IDENTIFIED BY 'Notre-super-m0t-de-passe!'; GRANT ALL PRIVILEGES ON wp202307_projetcyber* TO adminwp202307_projet1cyber@localhost; flush privileges; exit;"
