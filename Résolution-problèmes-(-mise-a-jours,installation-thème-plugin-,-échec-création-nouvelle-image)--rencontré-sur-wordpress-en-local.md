En voulant faire les mise a jour, installer des thème ou des plugin depuis l'interface wordpress en local sous apache2 il me demande l'accès à hôte via identifiant FTP 

Solution : http://stackoverflow.com/questions/13120226/wordpress-localhost-ftp

On a changé les droits en donnant l'accée a l'utilisateur apache uniquement : 
sudo chown -R www-data:www-data wordpress sur le dossier wordpress pour donner accée a l'utilisateur apache uniquement
Et sur le fichier de wp-config on ajoute define('FS_METHOD', 'direct');

-----------------------------------------

Si vous rencontré cet Erreur sur la fonctionalité modif (EDIT) des image : Unable to create new image wordpress( recadrer ) Echec lors de la création d'une nouvelle image : 

faut que sur le coté serveur(local ou a distance) on installe la librarie gd image library et redemarer le serveur apache : 
https://www.digitalocean.com/community/questions/how-to-enable-the-gd-image-library-for-wordpress
http://www.cyberciti.biz/faq/ubuntu-linux-install-or-add-php-gd-support-to-apache/

sudo apt-get install php5-gd