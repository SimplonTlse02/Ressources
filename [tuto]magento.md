-telecharger magento2 community edition 
-le decompresser

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
-creer la base de donnée magento et j'y accede pour linstaller

mysql -u -p
create database magento 
exit


-racine du projet: faire un composer install ,si le terminal le demande installer  les extensions manquantes et relancer un composer install







 
