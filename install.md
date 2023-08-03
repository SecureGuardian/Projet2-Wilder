# INSTALLATION DE LAMP -> Linux Apache Mariadb et Php
​
----------------------------------------------
​
## Installation d'Apache2
​
Commande installtion apache2 
`sudo apt install apache2`
​
Activer le démarrage automatque d'apache dés le dmarrage de Linux
`sudo systemctl enable apache 2`
​
Regarder si apache est actif ou non 
`sudo systemctl status apache2`
​
Activation de 4 paquets sur le server apache
-> REWRITE `sudo a2enmod rewrite`
Permet la réecriture de l'URL, avoir un lien sur le site qui vont etre constitués de titre de page plûtot que d'avoir un lien avec des id de parametres ou des choses qui n'ont pas trop de sens.
​
->SSL `sudo a2enmod ssl`
Pour avoir un site en HTTPS et gérer les certificats.
​
->DEFLATE `sudo a2enmod deflate`
Pour la partie compression, notamment la partie zip pour pourvoir faire de la mise en cache sur notre site internet et avoir des pages qui se charge plus rapidement et un serveur web qui souffle aussi un peu puisqu'il sera moins sollicité.
​
->HEADERS `sudo a2enmod headers`
Pour permettre d'intéragir avec les en-tetes HTTP.
​
Une fois que tout cela est installé, redemarrer apache
`sudo systemctl restart apache2`
​
----------------------------------------------------
​
### Configuration du serveur Apache
​
Dans le fichier `sudo nano /etc/apache2/apache2.conf` tout à la fin du fichier nous allons ajouter une ligne qui sera `ServerTokens Prod` cette directive va nous permettre de masquer la version d'apache et le nom du sytème, car un attaquant pourrais ce servir de ces informations pour exploiter des vulnérabilités.
​
------------------------------------------------------
​
## Installation PHP
​
Installation php
`sudo apt install php`
Cela va installer un grand nombres de paquets, valider quand il vous demandra.
​
Commande complémentaires `sudo apt install -y php-pdo php-mysql php-zip php-gd php-mbstring php-curl php-xml php-pear php-bcm` qui va permettre de venir installer d'autres modules comme `php mysql` pour permettre à php d'intéragir avec la base de données, `php zip` pour les dossiers compréssés, `php gd` pour tous ce qui est graphique...
​
Pour vérifier que php est bien installé on va c'est créer un fichier à la racine de notre site web `sudo nano /var/www/html/info.php` et dedans nous allons écrire du code en php et simplement exécuter la fonction php info :
```
< ?php
Phpinfo() ;
?)
```
Ensuite dans le navigateur nous allons écrire derrière l'ip `info.php` et là une page d'information s'affiche, premières indications, le php fonctionne. Sur le serveur web il est bien intégré à apache et cette page-là permet d'afficher vraiment toute la configuration de la partie php apache avec les modules donc c'est une page qui ne faut pas laisser accessible à n'importe qui donc il est recommande de mettre en place des restrictions au niveau de la configuration de d'apache.
Une fois cela terminé on peut supprimer le fichier `info.php` -> `sudo rm /var/www/html/info.php` comme nous sommes sûr qu'il n'y est personne qui va accéder à cette page là pour php.
​
-------------------------------------------------------------------
​
## Installation Mariadb
​
Il ne reste plus que la partie base de données Mariadb.
`sudo apt install mariadb`
​
Ensuite nous allons lancer un petit script qui va permettre de venir sécuriser un minimum notre instance mariadb en répondant à quelques questions. Donc on exécute la commande `sudo mariadb-secure-installation`.
​
Premierement il me demande le mot de passe par défaut de l'instance mariadb, comme elle vient d'êtres installé il n'y en à pas, donc on valide sans rien ecrire.
​
Est ce que nous voulons basculer sur l'authentification unix-socket ? n, on valide.
​
Est ce qu'on veux changer le mot de passe root ? yes, on valide.
Ensuite nous definissons le nouveau mot de passe de l'instance mariadb et attention à bien mettre un mot de passe vraiment sécurisé puisque ce compte permet d'acceder totalement à la bese de données.
​
Est ce qu'on souhaite supprimer les accés anonyme ? yes, on valide.
​
Est ce qu'on souhaite empecher root de se connecter à distance sur notre instance mariadb ? y, on valide.
​
Est ce que nous voulons supprimer la base de données de test et l'acces à cette base, yes, on valide.
​
Ensuite on valide, y, pour qu'il recharge les ensembles des privilèges.
​
Voila nous avons fait l'installation et la sécurisation minimaliste de mariadb et pour vérifier que nous avons bien acces à notre base de données nous allons faire `sudo mysql -u root -p` on rentre le mot de passe crée juste avant, on valide, et nous pouvons voir que l'on à bien acces à la console mariadb, nous pouvons également faire `show databases;` et cela nous liste les bases de données apr défaut, et on fait `exit` pour quitter la console.
​
Notre server LAMP est opérationnel et pret à acceuillir notre site internet.
​
# INSTALLATION ET PREMIER PAS AVEC WORDPRESS
​
Maintenant nous allons déployer Wordpress sur notre server LAMP sous Linux.
​
Nous allons nous positionner dans le dossier tmp `cd /tmp/` pour récuperer deja l'archive zip d'installation de Wordpress et faire la commande `wget https://wordpress.org/latest.zip`
et `latest.zip` va toujours récuperer la derniere version de Wordpress.
​
Ensuite il va falloir créer une base de donées dédiée à wordpress pour qu'il puissent stocker les informations sur la configuration, stocker les articles, les pages qui va etre crée, la configuration des extensions... donc on va créer une base dédiée avec son propre utilisateur qui aura uniquement des droits sur cette base de données.
​
On va devoir ce connecter à Mariadb `sudo mariadb -u root -p`, on met le mot de passe, et nous voila connécté.
​
Donc pour créer la base de données `create database wp202307_projet1cyber;` cela sera le nom de la base de données pour le site Wordpress (eviter les noms faciles à deviner, mettre un nom plus personnalisé) et on valide.
​
Si je fait `show databases;` nous pouvons voir que ma base de données est crée.
​
Maintenant nous allons créer un utilisateur `create user 'adminwp202307_projet1cyber'@localhost' IDENTIFIED BY 'Notre-super-m0t-de-passe!';` cela veux dire que nous voulons créer u utilisateur en presisant son nom, qu'il faudra rentrer dans wrodpress pour la connexion @ on autorise les connexions local et IDENTIFIED BY pour le mot de passe et on valide la commande.
​
Là nous avont crée un compte, maintenant je vais lui donner les droits sur ma base de données `GRANT ALL PRIVILEGES ON wp202307_projetcyber* TO adminwp202307_projet1cyber@localhost;` cela veux dire que l'on donne tous les droits sur cette base de donnée.
​
Pour finir nous allons faire `flush privileges;` cela permet d'appliquer, de recharger les droits pour que ce soit vraiment effectif.
​
Faire `exit` pour quitter la console mariadb car nous avons fini de créer la base d'utilisateurs.
​
Maintenant nous allons decompresser l'archive zip que l'on à telechargé à la racine du site c'est à dire dans `var/www/html`.
​
On va supprimer la page d'index d'apache qui est ajouté par défaut `sudo rm /var/www/htmlindex.html`.
​
Nous allons installer le paquet zip `sudo apt install zip` et ensuite `sudo unzip latest.zip -d /var/www/html/` cela veux dire que nous voulons décompresser dans /var/www/html.
​
Si nous regardons le contenu de mon dossier `/var/www/html` -> `sudo ls /var/www/html/` il m'a fait un dossier WordPress alors ça veut dire que pour accéder à mon site WordPress il faudra que je fasse l'adresse ip ou le nom domaine de mon site /wordPress/ puisque c’est un sous dossier de ma racine.
Deux solutions, soit nous modifions la racine du site dans le fichier `00.default.conf` comme on a vu tout à l'heure pour lui dire que la racine du site ce n'est pas `/var/www/html` mais c'est ``/var/www/html/wordpress` soit en laisse comme ça et dans ce cas-là il faut prendre le contenu des dossiers wordpress et remettent à la racine du dossier `html` et c'est ce qu'on va faire.
​
Donc va faire `cd /var/www/html/` et là on va déplacer le contenu donc avec mv `sudo mv worpress/* /var/www/html/` donc on déplace le contenu du dossier wordpress donc s’est pour cela qu’on met `wordpress/*`, on prend bien le contenu dans `/var/www/html` et donc je vais supprimer mon dossier wordpress puisqu'en fait il ne me sert plus rien, il est vide maintenant donc je fais un rm `sudo rm worpress/ -Rf`  pour forcer la suppression puisqu'il s'agit d'un dossier
​
Et enfin on va venir donner les droits à l'utilisateur `www-data:www-data` de manière récursive c'est à dire sur tous les dossiers de Wordpress grâce à la commande `sudo chown www-data:www-data /var/www/html/` et donc www-data:www-data ça correspond à l'utilisateur et aux groupes qui sont créés et associés par défaut à apache2 lorsque l'on met en place un serveur web donc là si je lis un petit peu le contenu de mon dossier de `/var/wwww/html` -> `sudo ls -l /var/www/html` on peut voir que j'ai tous les fichiers de wordpress qui sont là avec les bons droits `www-data:www-data` donc là on est pas mal normalement les droits par défaut qui sont données lorsque l’on décompresse l'archive de wordpress sont bons c'est à dire que c'est 644 sur les fichiers et 755 sur les dossiers, en aucun cas il ne faut mettre 777 ! donc là c'est bien le cas on a bien 644 ici sur tout mes fichiers et 755 sur mes dossier.
Si vous n'avez pas ça vous pensez ou même avoir modifié ses droits là et bien sachez qu'il y a des commandes qui permettent de remettre tout ça, donc là on a créé la base de données, l'utilisateur, on a décompressé les fichiers d'installation wordpress à la racine du serveur web de notre site par défaut donc on est plutôt pas mal on va retourner sur le navigateur à la racine du site on met l'adresse ip on valide et normalement on doit arriver sur la page wordpress donc la page de connexion. 
