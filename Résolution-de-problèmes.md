# Sommaire
* [Composer Install & Github Tokens](#composer-install--github-tokens)
* [ Probleme avec la cle SSH](#probleme-avec-la-cle-ssh)
* [Laravel - Whoops](#laravel-whoops)

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

# Probleme avec la cle SSH
Date: 29/02/16

Auteur: Mehdi

## Probleme

Quand vous essayez de cloné un repo avec SSH et que ça met 

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
