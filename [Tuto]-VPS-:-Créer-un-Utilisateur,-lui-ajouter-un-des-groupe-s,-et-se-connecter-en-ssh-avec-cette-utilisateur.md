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