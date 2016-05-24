* télecharger magento2 community edition sur le [site de magento](https://magento.com) 
* le décompresser dans le répertoire que vous avez choisi. Nous le mettons dans `/var/www/stage/`.
* installer le serveur nginx grace aux commandes suivantes
     `sudo apt-get update`
     `sudo apt-get install nginx`
* entrer la commande `chown www-data: magento2 -R` sur votre dossier magento pour donner les droits de modification au serveur nginx. 
* installer les extensions suivantes avec apt install (par exemple: sudo apt install php7.0-common).
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

* configurer le virtualhost     

* ajouter cette ligne au fichier /etc/hosts ajouter les noms de domaines au fichier  qui sera le nom de vos magasins
``` 
127.0.0.1  magento.dev ceintre.magento.dev bouton.magento.dev
```
    
* dans sites-avaible, ajouter le code ci-dessous /default copier/coller 
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

-à la racine du dossier magento se situe un fichier `nginx.conf.sample`, y copier/coller les lignes suivantes:

```
# Magento Vars
# set $MAGE_ROOT /path/to/magento/root;
# set $MAGE_MODE default; # or production or developer
#
# Example configuration:
# upstream fastcgi_backend {
#    # use tcp connection
#    # server  127.0.0.1:9000;
#    # or socket
#    server   unix:/var/run/php5-fpm.sock;
# }
# server {
#    listen 80;
#    server_name mage.dev;
#    set $MAGE_ROOT /var/www/magento2;
#    set $MAGE_MODE developer;
#    include /vagrant/magento2/nginx.conf.sample;
# }


root $MAGE_ROOT/pub;

index index.php;
autoindex off;
charset off;

add_header 'X-Content-Type-Options' 'nosniff';
add_header 'X-XSS-Protection' '1; mode=block';

location /setup {
    root $MAGE_ROOT;
    location ~ ^/setup/index.php {
        fastcgi_pass   fastcgi_backend;
        fastcgi_index  index.php;
        fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
        include        fastcgi_params;
    }

    location ~ ^/setup/(?!pub/). {
        deny all;
    }

    location ~ ^/setup/pub/ {
        add_header X-Frame-Options "SAMEORIGIN";
    }
}

location /update {
    root $MAGE_ROOT;

    location ~ ^/update/index.php {
        fastcgi_split_path_info ^(/update/index.php)(/.+)$;
        fastcgi_pass   fastcgi_backend;
        fastcgi_index  index.php;
        fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
        fastcgi_param  PATH_INFO        $fastcgi_path_info;
        include        fastcgi_params;
    }

    # deny everything but index.php
    location ~ ^/update/(?!pub/). {
        deny all;
    }

    location ~ ^/update/pub/ {
        add_header X-Frame-Options "SAMEORIGIN";
    }
}

location / {
    try_files $uri $uri/ /index.php?$args;
}

location /pub {
    location ~ ^/pub/media/(downloadable|customer|import|theme_customization/.*\.xml) {
        deny all;
    }
    alias $MAGE_ROOT/pub;
    add_header X-Frame-Options "SAMEORIGIN";
}

location /static/ {
    if ($MAGE_MODE = "production") {
        expires max;
    }
    location ~* \.(ico|jpg|jpeg|png|gif|svg|js|css|swf|eot|ttf|otf|woff|woff2)$ {
        add_header Cache-Control "public";
        add_header X-Frame-Options "SAMEORIGIN";
        expires +1y;

        if (!-f $request_filename) {
            rewrite ^/static/(version\d*/)?(.*)$ /static.php?resource=$2 last;
        }
    }
    location ~* \.(zip|gz|gzip|bz2|csv|xml)$ {
        add_header Cache-Control "no-store";
        add_header X-Frame-Options "SAMEORIGIN";
        expires    off;

        if (!-f $request_filename) {
           rewrite ^/static/(version\d*/)?(.*)$ /static.php?resource=$2 last;
        }
    }
    if (!-f $request_filename) {
        rewrite ^/static/(version\d*/)?(.*)$ /static.php?resource=$2 last;
    }
    add_header X-Frame-Options "SAMEORIGIN";
}

location /media/ {
    try_files $uri $uri/ /get.php?$args;

    location ~ ^/media/theme_customization/.*\.xml {
        deny all;
    }

    location ~* \.(ico|jpg|jpeg|png|gif|svg|js|css|swf|eot|ttf|otf|woff|woff2)$ {
        add_header Cache-Control "public";
        add_header X-Frame-Options "SAMEORIGIN";
        expires +1y;
        try_files $uri $uri/ /get.php?$args;
    }
    location ~* \.(zip|gz|gzip|bz2|csv|xml)$ {
        add_header Cache-Control "no-store";
        add_header X-Frame-Options "SAMEORIGIN";
        expires    off;
        try_files $uri $uri/ /get.php?$args;
    }
    add_header X-Frame-Options "SAMEORIGIN";
}

location /media/customer/ {
    deny all;
}

location /media/downloadable/ {
    deny all;
}

location /media/import/ {
    deny all;
}

location ~ cron\.php {
    deny all;
}

location ~ (index|get|static|report|404|503)\.php$ {
    try_files $uri =404;
    fastcgi_pass   fastcgi_backend;

    fastcgi_param  PHP_FLAG  "session.auto_start=off \n suhosin.session.cryptua=off";
    fastcgi_param  PHP_VALUE "memory_limit=256M \n max_execution_time=600";
    fastcgi_read_timeout 600s;
    fastcgi_connect_timeout 600s;
    fastcgi_param  MAGE_MODE $MAGE_MODE;
    fastcgi_param  MAGE_RUN_TYPE website;
    fastcgi_param  MAGE_RUN_CODE $MAGE_RUN_CODE;

    fastcgi_index  index.php;
    fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
    include        fastcgi_params;
}
```


* avant de re-demarer nginx faire la commande `nginx -t` pour verifier les syntaxe du fichier et ensuite re-demarrer nginx `service nginx restart`


* créer la base de données magento et y accèder. Entrer la commande suivante 

`mysql -u -p`
create database magento 

* aller à l'url magento.dev
* vous pouvez commencer à configurer votre site Magento 





 
