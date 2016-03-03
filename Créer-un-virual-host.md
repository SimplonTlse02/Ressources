# Création d'un virtual host.
___

Date: 29/02/16

Auteur: Allan Cerveaux

## Probleme

Comment créer un virtual host avec apache 2 pour les projets ?
>**Tuto pour toutes la classe.**

#### Quest-ce que c'est ?

Le Domain Name System (ou DNS, système de noms de domaine) est un service permettant de traduire un nom de domaine en informations de plusieurs types qui y sont associées, notamment en adresses IP de la machine portant ce nom.

>source : [Wikipedia(DNS)](https://fr.wikipedia.org/wiki/Domain_Name_System).

#### Comment ça marche ?

Un DNS permet d'associer des noms en langage courant aux adresses numériques (adresse ip) grâce à un système appelé DNS
>l'adresse ip  vous ai attribué  par votre :
> - Fournisseur d'accés A Internet,
> - Hébergeur de serveur (OVH...)
> - ou même un adresse locale
 
Au lieu 7.58.24.1 où encore 127.0.0.1 vous pourriez avoir ceci **monsupersite.dev** ou si vous achetez via un hébergeur ça pourrait donné ceci **monsupersite.fr**(ou .com etc...).

### **Comment créer un virtual host sous ubuntu avec apache 2 en local.**
_____
> **Note :** Ce tuto par sur la base où vous avez tout ce qui est nécessaire pour créer un virtual host.



1. Création du dossier pour le virtual host: 
 - Pour commencer nous allons créer un dossier de tout ce qu'il y a de plus banal pour le définir en tant virtual host :

 > `mkdir monsupersite`
 > 
 > ![Imgur](http://i.imgur.com/XpnKGJ4.png)
 
 - Puis nous allons un fichier .html et un .css pour avoir une base de site:
 
 > **Note** :  avant d'effectuer cette commande penser à entrer dans le dossier avec :
 > `cd monsupersite.`
 > `touch monsupersite.html`
 > `touch monsupercss.css`
 > Pour être sur que tous c'est passé correctement faire un petit `ls` pour voir si les fichier son bien créer.
 >
 >  ![Imgur](http://i.imgur.com/hHS1bsG.png)
 
 - Voilà nous avons fini pour la création du dossier pour le virtual host.
 
2. SuperUser et en route vers apache2 :
 
- Tous d'abord nous allons aller sur la console.

>`ctrl+alt+t`

- Puis nous allons nous mettre en super utilisateur. (ce qui sera plus simple pour éditer les fichier système).

>`sudo -i` 
>
>![Imgur](http://i.imgur.com/J9viT49.png)

- Une fois en super utilisateur nous allons nous diriger vers le dossier apache2.
> `cd /etc/apache2`
> 
>![Imgur](http://i.imgur.com/8OTHOXu.png)

- Nous voilà dans le dossier que nous cherchions depuis tous ce temps.

3. Configuration de nos petits fichiers :

Si vous faites un `ls` de nombreux fichiers sont apparus logiquement mais n'ayait craintes ce sera plus amusant que vous pensez.

####apache2.conf : 
- Donc pour commencer nous allons ouvrir un nouvel onglet dans le terminal qui nous servira dans quelques minutes : `ctrl+shift+t`

- Nous allons tout d'abord modifier le fichier ```apache2.conf```(comme on est en super utilisateur pas besoin de sudo)

>**Note :** j'utilise gedit peut importe sera votre éditeur de texte ou IDE ça marchera dans tous les cas.
>
>`gedit apache2.conf`
>
>![Imgur](http://i.imgur.com/unePElD.png)

- Après avoir ouvert le fichier ```apache2.conf``` il faudra descendre jusqu'à la ligne où se trouve ce bout de code.
```
#<Directory /srv/>
#   Options Indexes FollowSymLinks
#   AllowOverride None
#   Require all granted
#</Directory>
```
>Il faudra dupliquer ce bout de code en faisant un simple copier/coller, puis enlever les dièse (#) pour enlever le code en mode commentaire

- Plus qu'une dernière étape pour ce fichier il vous restera à partir sur le deuxième onglet que nous avons ouvert sur la console pour connaitre le chemin exact de notre dossier ```monsupersite``` 

>pour cela il faudra taper cette commande dans la console :
> `pwd`
> puis il vous faudra remplacer dans la ligne où il y a le ```<Directory /srv/>``` ,
> la où il y a le /srv/ par le chemin de votre fichier,
> puis remplacer le **None** là où il y a ```AllowOverride None``` par **All** pour donner le droit d'écriture et de lecture
> 
> ![Imgur](http://i.imgur.com/8Xpbxgv.png)

Puis il restera à faire un petit ```ctrl+s``` pour sauvegarde les modifications.

####sites-availlable : 

Maintenant nous allons nous rendre dans ```sites-availlables``` et faite votre petit ```ls``` pour voir ce qui si cache.

- Après avoir inspecter je vous invite à ouvrire encore avec ```gedit``` le fichier ```000-default.conf```

> `gedit 000-default.conf`
> 
>Et comme nous sommes toujours en super utilisateur nous n'avons pas besoin du sudo.
> 


![Imgur](http://i.imgur.com/ZZJpLH0.png)


- Puis allons modifier que deux petites lignes.

La ligne qui contient :
`#ServerName www.example.com` 
Il faudra le remplacer par le DNS de votre choix moi je vais le remplacer par :
>`ServerName monsupersite.dev`
>
>Puis la ligne qui contient :  
>`DocumentRoot /var/www/html`
>Par la route de votre dossier `monsupersite` que vous avez copier au préalable
>`DocumentRoot /home/nutela/monsupersite`
>
>Voilà il vous restera à faire un `ctrl+maj+s` en lui donnant un nom qui corresponde à votre DNS moi je l'appelle `monsupersite.conf`
>
>
>![Imgur](http://i.imgur.com/JQvmt2j.png)

#### Hosts :

On y est presque reste plus que ce fichier quelque manipulation puis c'est fini.

- Pour trouver le fichier hosts il faudra retourné dans le dossier `/etc` car c'est dans celui-ci que vous le trouverez.
> Pour allez plus vite dans la navigation entre vos dossier et si vous êtes toujours dans le dossier `sites-availble` je vous conseille de faire.

> `cd ../../`
> 
>Il vous restera à faire un `gedit hosts` pour accéder au fichier **hosts**.
>  
>  Logiquement vous allez arriver dans un fichier où il y à juste :

    ```127.0.0.1    localhost
    127.0.1.1   nutela-All-Serie
    [#]The following lines are desirable for IPv6 capable hosts
    (il y à juste un diése sur la ligne du dessut)
    ::1     ip6-localhost ip6-loopback
    fe00::0 ip6-localnet
    ff00::0 ip6-mcastprefix
    ff02::1 ip6-allnodes
    ff02::2 ip6-allrouters```

Il faudra rajouter une ligne suplémentaire avec `127.0.0.1` en dessout de ` 127.0.1.1 nutela-All-Serie` puis rajouter votre DNS, après cela comme d'habitude il faudra faire un `ctrl+s` pour sauvegarder les modifications.

![Imgur](http://i.imgur.com/JQvmt2j.png)


 - Et pour finir il faudra relancer le serveur apache2 en faisant `service apache2 restart` afin qu'il prenne les modifications en compte.

 Voilà maintenant vous pouvez sortir du mode super utilisateur pour ne pas faire de bêtise en faisant `exit` puis on passera à la suite.

 4.Activer son sites :

Bien que l'on a mis en place le nom de domaine il faudra quand même activer son site car logiquement si vous tapez votre nom domaine sur l'internet vous allez tomber sur cette page :

![Imgur](http://i.imgur.com/EVLqaRa.png)

Ne vous inquiéter pas ce n'est pas la fin du monde on a juste à taper une commande pour que cela que notre site soit mise en place.

>`sudo a2ensite monsupersite.conf`
> puis il vous restera à redémarrer apache2
> et le tour et joué.

Si vous tapez votre DNS sur l'internet vous allez voir cette page


![Imgur](http://i.imgur.com/iLxjJtn.png)


![Imgur](http://i.imgur.com/U3wUB8N.png)

Voilà vous savez maintenant comment faire un virtual host 

####Enjoy.