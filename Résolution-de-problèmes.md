
# Sommaire

* [Réactiver connection WIFI caché](#r%C3%A9-activer-r%C3%A9seau-wifi-cach%C3%A9)
* [Composer Install & Github Tokens](#composer-install--github-tokens)
* [ Probleme avec la cle SSH](#probleme-avec-la-cle-ssh)
* [Laravel - Whoops](#laravel---whoops)
* [Laravel - Page blanche](#laravel---page-blanche)
* [wordpress - problemes mise a jours , installation theme plugin et probleme edit image](#wordpress - problemes mise a jours , installation theme plugin et probleme edit image)

----------

# Ré-Activer réseau WIFI caché
Date : 07.03.2016
 
Auteur : Karine 

## Probleme
Réactiver la connection cachée "SimplonMIP". Si elle a l'icône, d'un ordinateur et non plus celle du Wifi.

## Solution
D'abord, cliquez sur "edit connection" dans la recherche WIFI,
puis sélectionner un de ceux utilisés d'habitude: 
> ex SIMPLON MIP

> EDIT

> MODE : paramétrer avec "infrastructure"

> SAVE

Relancer dans le choix des reseaux pour que l'icône réapparaisse en "WIFI"

![Img](http://i.imgur.com/soskss4.png)

-------------

# Composer Install & Github Tokens
Date : 29.02.2016

Auteur : Sébastien

## Problème
Lors de l'installation avec 
> composer install

> Could not fetch https://api.github.com/repos/symfony/polyfill-mbstring/zipball/XXXXXXXXXXXXXXXXXXXXXXXXXXXX, please create a GitHub OAuth token to go over the API rate limit

> Head to https://github.com/settings/tokens/new?scopes=repo&description=ComposerXXXXXXXXXXXXX

> to retrieve a token. It will be stored in "/home/vagrant/.composer/auth.json" for future use by Composer.

> Token (hidden): 

## Solution
Créer un token Github et l'ajouter au composer.json

ou copier coller le lien donnée par la console (attention, à faire immédiatement : ne pas attendre. Le token généré a une durée de vie limitée).

## Ressources
* http://latcoding.com/2015/09/07/composer-problem-token-hidden-on-github/
* https://github.com/settings/tokens

----------

# Probleme avec la cle SSH
Date: 29/02/16

Auteur: Mehdi

## Probleme

Quand vous essayez de cloner un repo avec SSH et que ça met 

> Agent admitted failure to sign using the key

## Solution
dans la console mettre 

> eval "$(ssh-agent -s)"

Ensuite toujours dans la console

> ssh-add

Normalement votre git clone marche

## Ressouces

*https://help.github.com/articles/error-agent-admitted-failure-to-sign/

----------
# Laravel - Whoops
Date: 02/03/2016

Auteur: Maxime

## Problème
Erreur avec Laravel avec un message du genre 
> Whoops... Looks like something went wrong ....

## Solution
Voir les logs de Laravel {PROJET}/storage/logs/laravel.log


----------
# Laravel - Page blanche
Date: 02/03/2016

Auteur: Maxime

## Problème
Si avec laravel, la page reste blanche, le problème ne vient pas de Laravel mais de apache.


## Solution
Voir les logs d'Apache /var/logs/apache2/error.log

-----------
# wordpress - problemes mise a jours , installation theme plugin et probleme edit image 

Date: 29/03/2016

Auteur: anis

## Problèmes
1.En voulant faire les mise a jour, installer des thème ou des plugin depuis l'interface wordpress en local sous apache2 il me demande l'accès à hôte via identifiant FTP

2.Si vous rencontré cet Erreur sur la fonctionalité modif (EDIT) des image : Unable to create new image wordpress( recadrer ) Echec lors de la création d'une nouvelle image 

## Solutions
1.On a changé les droits en donnant l'accée a l'utilisateur apache uniquement : sudo chown -R www-data:www-data wordpress sur le dossier wordpress pour donner accée a l'utilisateur apache uniquement Et sur le fichier de wp-config on ajoute define('FS_METHOD', 'direct');
trouvé ici http://stackoverflow.com/questions/13120226/wordpress-localhost-ftp

2.faut que sur le coté serveur(local ou a distance) on installe la librarie gd image library et redemarer le serveur apache : https://www.digitalocean.com/community/questions/how-to-enable-the-gd-image-library-for-wordpress http://www.cyberciti.biz/faq/ubuntu-linux-install-or-add-php-gd-support-to-apache/

sudo apt-get install php5-gd
