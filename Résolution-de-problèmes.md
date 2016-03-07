
# Sommaire
* [Composer Install & Github Tokens]#composer-install--github-tokens)
* [ Probleme avec la cle SSH](#probleme-avec-la-cle-ssh)
* [Laravel - Whoops](#laravel---whoops)
* [Laravel - Page blanche](#laravel---page-blanche)
* [Réactiver connection WIFI caché]

----------

# Réactionner réseau WIFI caché
Date : 07.03.2016 
Auteur : Karine 

## Probleme pour réactiver la connection caché "SimplonMIP"
D'abord, "edit connection" ds la recherche WIFI, puis sélectionner celui utilisé d'habitude: ex SIMPLON MIP
EDIT
MODE : paramétrer avec "infrastructure"
SAVE
et relancer dans le choix des reseaux pr qui l'icone réapparaisse en "WIFI"
> screen shot correspondant : 
https://cloud.githubusercontent.com/assets/16001498/13570884/6c4e5814-e471-11e5-8062-c7e1e01e33c7.png

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
