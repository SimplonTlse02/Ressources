Ce tuto suppose que vous utilisez Ubuntu 16.04

![screen panel ovh](http://i.imgur.com/D4nreWH.png)

0. Liaison entre votre domaine et votre VPS

Commencez par noter l'adresse IP de votre 
![screen ip vps](http://i.imgur.com/YwrUzNq.png)

Ensuite, rendez-vous dans la configuration des DNS de votre domaine
![screen domain](http://i.imgur.com/YwrUzNq.png)

Editer l'entrée correspondant à la racine de votre domaine et **de type A** en entrant l'ip de votre VPS
![screen modif dns](http://i.imgur.com/YwrUzNq.png)

1. Installation d'nginx

Source : [Installer nginx avec les PPA Ubuntu](https://www.nginx.com/resources/wiki/start/topics/tutorials/install/#official-debian-ubuntu-packages)
```
sudo -s
nginx=stable # use nginx=development for latest development version
add-apt-repository ppa:nginx/$nginx
apt-get update
apt-get install nginx
```

2. Installation de PHP 7 fpm
```
apt install php-fpm php-mcrypt php-intl php-gd php-pdo php-mysql php-mbstring php-dom
```

3. Installation de MariaDB
[Installationd e mariadb sur Ubuntu](https://downloads.mariadb.org/mariadb/repositories/#mirror=cnrs&distro=Ubuntu&distro_release=xenial--ubuntu_xenial&version=10.1)
```
sudo apt-get install software-properties-common
sudo apt-key adv --recv-keys --keyserver hkp://keyserver.ubuntu.com:80 0xF1656F24C74CD1D8
sudo add-apt-repository 'deb [arch=amd64,i386] http://ftp.igh.cnrs.fr/pub/mariadb/repo/10.1/ubuntu xenial main'
sudo apt-get update
sudo apt-get install mariadb-server
```

4. Configuration d'un virtualhost

exemple de fichier de  conf

modifiez le `default` avec ces infos :

```
    server_name mon_nom_de_domaine;
    root /mon_dossier;

    index index.php index.html index.htm;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }
```

puis ajoutez pour prendre en compte PHP :

```
    location ~ \.php$ {
        fastcgi_split_path_info ^(.+\.php)(/.+)$;
        fastcgi_pass unix:/var/run/php/php7.0-fpm.sock;
        fastcgi_index index.php;
        # include fastcgi_params;
        include fastcgi.conf;
    }
```

5. Installation de dbninja (ou encore mieux mysql-workbench)

5. Installation et configuration de letsencrypt

# Créer un Utilisateur, lui ajouter un/des groupe/s, et se connecter en ssh avec cette utilisateur
___

## Étape 1 Créer l'utilisateur : 
____

Pour créer un User sur votre VPS rien de plus simple une seul commande à taper :

``` bash
	adduser username
```

> le username sur le tuto et votre nom d'utilisateur !

Donc une fois la commande exécuter, il vous demandera un mot de passe à vous de mettre le votre.

> Je vous conseil de passer pas le logiciel KeepassX qui vous permet de générer des mot de passe complexe pour plus de sécurité.

## Étape 2 Ajouter un groupe à votre utilisateur :
___

Pour cette deuxième étape nous allons ajouter notre user que je vais appeler jean-michel pour garder son anonymat.

Alors jean-michel doit-être dans le groupe des sudoers et www-data pour nginx.

Pour cela on à juste une petite commande sympathique à taper :

``` bash
	usermod -aG nom_du_groupe jean-michel 
```

> la ou j'ai écris le nom du groupe il faudra le changer par `sudo` et `www-data`.

```
usermod -aG sudo jean-michel
usermod -aG www-data jean-michel 
```
Et voila une fois c'est deux groupes sont ajouté c'est beau, c'est magique, c'est magnifique,


## Étape 4 connexion en SSH avec votre utlisateur

___

``` javascript
	if(sshKey === true){
		connexion = true;
	}else{
		create(sshKey);
	}
		
```

Bon pour ceux qui non pas compris on va vérifier si vous avez une clé SSH pour cela il faut allez regarder si dans le dossier `.ssh` il y à un `id_rsa.pub`.

pour cela il faut faire un 

``` bash
	cd .shh && ls
```

Si vous avez ceci des fichiers appelé  `id_rsa.pub` ou `id_rsa`.

It's Epic Win !

- Sinon il faut en créer une, pour cela il faudra taper `ssh-keygen`.

- une fois taper vous suivez les différentes étapes qu'il vous demander.


une fois la clé ssh créer, il faut faudra juste la copier sur votre VPS avec la commande :

``` bash
	ssh-copy-id jean-michel@hostname
```

> hostname correspond à votre nom de domaine ou à l'adresse ip de votre VPS.

Une fois que c'est fait Enjoy ! On pourra de connecter avec l'utilisateur que vous venez de créer juste en faisant

``` bash
	ssh hostname
```

# ENJOY !