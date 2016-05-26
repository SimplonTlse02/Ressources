* Pour accéder à l'interface d'administration de Magento, il est nécessaire de procéder à l'installation du setup de Magento.
  Dans l'url de votre site, ajoutez `/setup` et commencez le checking.
  La base de données va se mettre à jour automatiquement.
* Vous pouvez ensuite vous rendre sur l'interface d'admin en ajoutant `/admin` à la fin de l'url et entrer vos identifiants.

Dans un premier temps, nous allons paramétrer l'interface afin de pouvoir gérer plusieurs sites marchants séparés mais la méthode est la même s'agissant d'un site unique.

* Rendez vous dans l'onglet, `/Products/Categories` puis cliquez sur `Add Root Category` et ajoutez autant de catégories que de sites prévus.
Si vous souhaitez que vos sites soient entièrement séparés, veillez à créer différentes routes category, une par site.

* Allez ensuite dans l'onglet `Stores` et créez un site (`Create Website`). 
 Dans les informations du site, veillez à remplir la case `code` avec celui que vous avez renseigné lors de la configuration des noms de domaine sur votre serveur. Dans notre cas, le code est 'geantducintre' et notre url 'cintre.agps.smp.ovh'.
Cliquez ensuite sur le bouton `Create Store` et utilisez la Root Category que vous avez créé précédemment.
Cliquez sur `Store View` et remplissez les informations demandées.

* Retournez dans `/Products/Category` et créez ensuite les sous dossiers pour chaque site en cliquant sur `Add Subcategory`. 
Puis, allez dans `/Products/Catalog`, cliquez sur `Add Product` et ajoutez les informations nécessaires. Dans le sous-menu `Websites`, vous pouvez choisir sur lequel de vos sites le produits apparaîtra.

*

 
