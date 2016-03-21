![](http://jeromemouly.com/wp-content/uploads/2016/03/svgporn-wordpress-2.png) 

# Tutoriel installation Wordpress En Local

----

## Pré-requis

Avoir une installation de [LAMP](https://doc.ubuntu-fr.org/lamp) sur sa machine.

> Si vous devez faire une installation de LAMP voici quelques liens 

> [Doc Ubuntu](https://doc.ubuntu-fr.org/lamp)

> [Digital Ocean](https://www.digitalocean.com/community/tutorials/how-to-install-linux-apache-mysql-php-lamp-stack-on-ubuntu-14-04)

> [OnlLine.Net](https://documentation.online.net/fr/serveur-dedie/tutoriel/installation-solution-lamp_apache-php-mysql)

----

###1. Télécharger Wordpress

Tout d'abord on va télécharger le dossier Wordpress sur les sites officielles.

[Wordpress en Français](https://fr.wordpress.org/)

[Wordpress en Anglais](https://wordpress.org/)


###2. Positionner le dossier Wordpress

Il faut positionner le dossier Worpdress dans le dossier ou se trouve votre localhost

![](http://jeromemouly.com/wp-content/uploads/2016/03/dossier-wordpress.png) 


----

###3. Méthode pour la visualisation de wordpress

Browser Sync

> browser-sync start --server --files="*.html,css/*.css,js/*.js"


![](http://jeromemouly.com/wp-content/uploads/2016/03/console.png)


###4.  Paramétrage Wordpress

Une fois que vous avez lancer wordpress sur votre localhost il reste encore quelques réglages afin de pouvoir accéder au Tableau de bord.


   * 4.1 Configuration de la Base de Donnée

![](http://jeromemouly.com/wp-content/uploads/2016/03/install-word.png)

Dans cette fenêtre il suffit de rentrer vos identifiants de votre Base de donnée MySqL ou autres (NinjaDB, Maria DB ...) afin de pouvoir vous connecter à Wordpress.

![](http://jeromemouly.com/wp-content/uploads/2016/03/install-Data.png)

__Il est important de changer les 'Préfixes des tables' pour commencer à sécuriser votre site__

Une fois vos paramètres rentrés vous obtiendrez ceci

![](http://jeromemouly.com/wp-content/uploads/2016/03/install-reussi.png)

Qui indique que votre installation de la base de donnée est terminée et que l'on peut passer à l'étape suivante.

   * 4.2 Configuration de Wordpress

Ici vous allez créer vos identifiants pour votre connexion à Wordpress.

![](http://jeromemouly.com/wp-content/uploads/2016/03/config-wordpress.png)

__Il est important de rentrer une adresse mail, c'est celle-ci qui vous permettra de changer votre mot de passe si vous le perdez et également avoir les informations de connexion à wordpress.__

__De plus en cochant 'Visibilité pour les moteurs de recherche' (quand vous installerez wordpress via un hébergeur) vous allez commencez à référencer votre site sur les différents moteur de recherche.__

![](http://jeromemouly.com/wp-content/uploads/2016/03/ident-word.png)

Maintenant il ne reste qu'à vous identifier

![](http://jeromemouly.com/wp-content/uploads/2016/03/connexion-word.png)

 pour accéder au Tableau de bord de Wordpress.

![](http://jeromemouly.com/wp-content/uploads/2016/03/Dashboard.png)

  