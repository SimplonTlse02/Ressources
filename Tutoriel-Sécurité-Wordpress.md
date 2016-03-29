

![](http://jeromemouly.com/wp-content/uploads/2016/03/svgporn-wordpress-2.png)


# Tutoriel Sécurité pour votre Wordpress
---

##Première manipulation

Tout d'abord vous allez bloquer l'accès de certains fichiers en lecture seule.
Ce procéder est accessible via un programme FTP ou en faisant in click droit propriétés puis permissions et vous pouvez changer les accès de lecture.

![](http://jeromemouly.com/wp-content/uploads/2016/03/permission-fichier-wordpress.jpg)


##Ajout de ligne

Tout d'abord vous allez ajouter les lignes suivantes en bas dans le fichiers .htaccess :

Ces lignes de code vont protéger votre fichier wp-config.php.

`<files wp-config.php>
 order allow,deny
 deny from all
 </files>`

Ces lignes de code vont protéger votre fichier .htaccess.

`<files .htaccess>
order allow,deny
deny from all
</files>`

Ces lignes de code vont cacher les répertoires sensibles.

`Options All -Indexes`


Ensuite vous allez modifier en bas le fichier functions.php dans wp-content/themes/votre theme ...


Ces lignes de code vont masquer votre version de Wordpress.

`remove_action("wp_head", "wp_generator");`

Ces lignes de code vont masquer votre version de Wordpress via le flux RSS.

`function wpt_remove_version() {
return ''; }
add_filter('the_generator', 'wpt_remove_version');`

Pour finir supprimer le fichier readme.html qui se trouve à la racine du dossier Wordpress.

De plus toutes ces modifications sont à ajouter au changement des 'Préfixe des tables lors de l'installation de Wordpress 

![](http://jeromemouly.com/wp-content/uploads/2016/03/install-Data.png)

et également en ajoutant des plugins de sécurité supplémentaires.

Vous pouvez suivre [ce tutoriel](https://github.com/SimplonTlse/Ressources/wiki/Tutoriel-Plugin-Wordpress) .

Voici quelques liens sur la sécurité pour son site Wordpress

[15 rappels de Sécurité pour WordPress](http://wpformation.com/11-rappels-securite-wordpress/)

[Sécuriser efficacement son site WordPress](http://www.fabricecourt.com/formation/securiser-efficacement-son-site-wordpress/)

[Sécuriser WordPress – L’installation](http://korben.info/securiser-wordpress-installation.html)

[Comment sécuriser son site Wordpress en quelques minutes ?](http://www.atchik-services.com/blog/webmarketing/securiser-site-blog-wordpress)

[20 astuces pour sécuriser votre site WordPress](http://blog.netapsys.fr/securisation-de-votre-site-wordpress/)
