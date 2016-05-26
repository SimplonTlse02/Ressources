* Nous téléchargeons Magento2 community-edition sur le [site de Magento](https://magento.com). 
* Il faut ensuite décompresser le dossier téléchargé dans le répertoire choisi. Nous avons choisi de le mettre dans `/var/www/stage/`.
* Nous installons ensuite le serveur Nginx grâce aux commandes suivantes:
     `sudo apt-get update`
     `sudo apt-get install nginx`
* Nous donnons les droits d'accès au serveur Nginx en entrant la commande `chown www-data: magento2 -R`. 
* Il nous faut ensuite installer les extensions suivantes avec la commande apt install.
  (sudo apt install php7.0-common)
  -  php7.0-common
  -  php7.0-gd 
  -  php7.0-mysql
  -  php7.0-mcrypt 
  -  php7.0-curl
  -  php7.0-intl 
  -  php7.0-xsl
  -  php7.0-mbstring
  -  php7.0-zip 
  -  php7.0-soap

* Nous configurons ensuite le virtualhost, en nous rendant dans le dossier 'hosts' situé dans '/etc/hosts', nous allons ajouter la ligne suivante:
``` 
127.0.0.1  magento.dev cintre.magento.dev bouton.magento.dev
```     
les noms de domaine correspondront aux noms de vos sites.
    
* Aller dans `/etc/nginx/sites-avaible`, ajouter le code ci-dessous au fichier `default` et l'adapter à votre configuration. 
Attention à noter le code correspondant à votre site et à l'écrire sans espace et sans majuscule ni caractères spéciaux. Par exemple, notre site 'ceintre.magento.dev' a pour code 'geantducintre'. Ce code sera réutilisé dans la configuration du site de l'interface de Magento.
```
upstream fastcgi_backend {
        server  unix:/var/run/php/php7.0-fpm.sock;
}

map $http_host $MAGE_RUN_CODE {
   cintre.magento.dev geantducintre;
   bouton.magento.dev geantdubouton;
}

server {

        listen 80;
        server_name magento.dev;
        set $MAGE_ROOT /var/www/stage/magento2;
        set $MAGE_MODE developer;
        include /var/www/stage/magento2/nginx.conf.sample;
}
server {

        listen 80;
        server_name cintre.magento.dev;
        set $MAGE_ROOT /var/www/stage/magento2;
        set $MAGE_MODE developer;
        include /var/www/stage/magento2/nginx.conf.sample;
}
server {

        listen 80;
        server_name bouton.magento.dev;
        set $MAGE_ROOT /var/www/stage/magento2;
        set $MAGE_MODE developer;
        include /var/www/stage/magento2/nginx.conf.sample;
}


```

-Se rendre à la racine du dossier ou vous avez décompressé Magento, ouvrir le fichier `nginx.conf.sample`, et y rajouter les deux dernières lignes du paragraphe suivant:

```
   {
    fastcgi_param  PHP_FLAG  "session.auto_start=off \n suhosin.session.cryptua=off";
    fastcgi_param  PHP_VALUE "memory_limit=256M \n max_execution_time=600";
    fastcgi_read_timeout 600s;
    fastcgi_connect_timeout 600s;
    fastcgi_param  MAGE_MODE $MAGE_MODE;
    fastcgi_param  MAGE_RUN_TYPE website;
    fastcgi_param  MAGE_RUN_CODE $MAGE_RUN_CODE;

}
```


* Avant de re-demarrer Nginx, entrer la commande `nginx -t` pour vérifier le bon fonctionnement du serveur et ensuite le re-demarrer avec `service nginx restart`.


* Allez sur votre base de donnée, par exemple via l'interface de PhpMyAdmin et créer la table Magento qui de complète automatiquement. Vous pouvez aussi entrer directement la commande suivante dans votre terminal, ce qui produit le même résultat:

`mysql -u -p
create database magento` 

* Se rendre sur l'url de votre site ou de vos magasins.
* Ajoutez '/admin' à la fin de l'url afin d'accéder à l'interface d'administration.
* Vous pouvez commencer à configurer votre site Magento. 





 