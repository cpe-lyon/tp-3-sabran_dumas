# TP3 Gestion des paquets

## Exercice 1. Commandes de base

### Question 1

On utilise la commande ```dpkg -l``` et on trouve que les 5 derniers paquets installés sont : 
xkb-data /  xxd / xz-utils / zerofree / zlib1g:amd64.

### Question 2
On utilise les commandes ```dpkg -l``` et ```apt list --installed | wc --lines``` pour compter le nombre de paquets installés. **dpkg** affiche tout seul le nombre de paquets (553) alors que **apt**  ne le fait pas, c'est donc pour cela que l'on passe par un pipe (qui nous affiche 549).
On trouve donc que ```dpkg -l``` nous affiche 4 paquets de plus. Cette différence est due au fait que **dpkg** nous informe des éventuelles dépendances à installer alors que **apt** 

### Question 3
On utilise la commande ```apt list --ugradeable ``` et on trouve que tous les paquets sont à jour.

### Question 4
On rentre dans le fichier .bashrc grâce à ```nano .bashrc``` et on créé un alias qu'on nomme "maj" avec la commande ```alias maj= 'sudo apt upgrade' ```.

### Question 5
Le paquet  **fortunes** affiche des citations aléatoires.
On installe le paquet à l'aide de la commande ```sudo apt install fortunes ```  

### Question 6
Le paquet **sudoku** permet de jouer au Sudoku.
On installe le paquet à l'aide de la commande ```sudo apt install sudoku ```

### Question 7
Il faut aller regarder dans le fichier **/var/log/apt/history.log** et on voit que les 2 dernier paquets installé par ```apt install ``` sont **fortunes** et **sudoku**.

## Exercice 2.
Grâce à ```which ls``` on trouve où est stocké la commande ls et ensuite on fait ```dpkg -S /bin/ls ``` pour trouver le paquet est installée la commande. Ce paquet s'appelle **coreutils**.

La commande ```dpkg -S $(wich -a nom_de_la_commande | tail -i) ``` permet en une seule ligne d'afficher dans quel paquet est installée la commande.

On crée le script via la commande ```nano origine_commande ```. Puis on fait ```chmod u+x origine_commande``` pour que le changement se fasse sur le propriétaire (nous) et qu'il puisse s'éxécuter. 

Le script : 
![origine_commande](https://user-images.githubusercontent.com/60732798/76021867-53f23680-5f26-11ea-9f46-00955dec5f5c.png)

Le résultat : 
![result](https://user-images.githubusercontent.com/60732798/76022548-ab44d680-5f27-11ea-8671-62c3809c81b9.png)

## Exercice 3.
On utilise les mêmes commandes pour créer le script et pour changer les permissions.

Le script : 
![install](https://user-images.githubusercontent.com/60732798/76022444-75075700-5f27-11ea-9812-f35693394112.png)

Le résultat : 
![test_install](https://user-images.githubusercontent.com/60732798/76022510-9405e900-5f27-11ea-87ff-c7c58314692d.png)

## Exercice 4.

On utilise la commande ```dpkg -L coreutils``` qui nous affiche tous les programmes livrés avec coreutils.
La commande **[** permet de réaliser des tests, par exemple ```[ "a" = "a" ]``` teste si la chaine de caractère "a" es la même que "a". Pour afficher ce qu'elle retourne il faut utiliser la commande ```echo $?```.

## Exercice 5.

Pour installer le paquet ``emacs`` via l'interface graphique aptitude on saisi la commande ``` sudo aptitude ```. Ensuite on cherche le paquets ``emacs`` puis on l'installe avec la touche ``g``.

## Exercice 6.

Pour installer Oracle on fait : 
```sudo add-apt-repository ppa:linuxuprising/java ``` 
```sudo apt update ``` 
```sudo apt install oracle-java11-installer```

Un nouveau fichier a bien été créé dans/etc/apt/sources.list.d Il contient l'adresse de dépot du répertoire virtuel permettant d'acceder aux différents éléments du répertoire.

## Exercice 7.


