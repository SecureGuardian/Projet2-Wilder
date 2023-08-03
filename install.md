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










