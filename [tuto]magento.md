- telecharger magento2 community edition 
- le decompresser dans `/var/www/stage/`
- faire `chown www-data: magento2 -R` pour donner les droits au serveur nginx 
installer les extensions avec apt install
- php7.0-common
-  php7.0-gd 
-  php7.0-mysql
- php7.0-mcrypt 
-  php7.0-curl
-   php7.0-intl 
-  php7.0-xsl
-  php7.0-mbstring
-  php7.0-zip 
- php7.0-soap






-configurer le virtualhost     

-server_name magento.dev 
    
-$path 

- dans sites-avaible /default copier/coller le code ci-dessous
```
upstream fastcgi_backend {
        server  unix:/var/run/php/php7.0-fpm.sock;
}

map $http_host $MAGE_RUN_CODE {
   ceintre.magento.dev geantduceintre;
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
        server_name ceintre.magento.dev;
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
-ajouter cette ligne au fichier /etc/hosts ajouter les noms de domaines au fichier 
``` 
127.0.0.1  magento.dev ceintre.magento.dev bouton.magento.dev
```
avant de re-demarer nginx faire la commande `nginx -t` pour verifier les syntaxe du fichier et ensuite re-demarrer nginx `service nginx restart`


-créer la base de donnée magento et j'y accède pour l installer 

`mysql -u -p`
create database magento 



-aller a l'url magento.dev
-configuration de base sur le site 





 
