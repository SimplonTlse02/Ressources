Ce tuto suppose que vous utilisez Ubuntu 16.04

![screen panel ovh](http://imgur.com/D4nreWH)

0. Liaison entre votre domaine et votre VPS

Commencez par noter l'adresse IP de votre 
![screen ip vps](http://imgur.com/YwrUzNq)

Ensuite, rendez-vous dans la configuration des DNS de votre domaine
![screen domain](http://imgur.com/YwrUzNq)

Editer l'entrée correspondant à la racine de votre domaine et **de type A** en entrant l'ip de votre VPS
![screen modif dns](http://imgur.com/YwrUzNq)

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

5. Installation de dbninja

5. Installation et configuration de letsencrypt

