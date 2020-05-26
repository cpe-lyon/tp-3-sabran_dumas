# TP3 Gestion des paquets

## Exercice 1. Commandes de base

### Question 1 : 
Quels sont les 5 derniers paquets installés sur votre machine ?

On utilise la commande ```dpkg -l``` et on trouve que les 5 derniers paquets installés sont :  
```
xkb-data  
xxd  
xz-utils  
zerofree  
zlib1g:amd64.  
```

### Question 2 : 
Utiliser dpkg et apt pour compter le nombre de paquets installés (ne pas hésiter à consulter le manuel !).
Comment explique-t-on la (petite) différence de comptage ?

On utilise les commandes ```dpkg -l``` et ```apt list --installed | wc --lines``` pour compter le nombre de paquets installés. **dpkg** affiche tout seul le nombre de paquets (553) alors que **apt**  ne le fait pas, c'est donc pour cela que l'on passe par un pipe (qui nous affiche 549).
On trouve donc que ```dpkg -l``` nous affiche 4 paquets de plus. Cette différence est due au fait que **dpkg** nous informe des éventuelles dépendances à installer alors que **apt** 

### Question 3 : 
Combien de paquets sont disponibles en téléchargement ?

On utilise la commande ```apt list --ugradeable ``` et on trouve que tous les paquets sont à jour.

### Question 4 : 
Créer un alias “maj” qui met à jour le système

On rentre dans le fichier .bashrc grâce à ```nano .bashrc``` et on créé un alias qu'on nomme "maj" avec la commande ```alias maj= 'sudo apt upgrade' ```.

### Question 5: 
A quoi sert le paquet fortunes ? Installez-le

Le paquet  **fortunes** affiche des citations aléatoires.
On installe le paquet à l'aide de la commande ```sudo apt install fortunes ```  

### Question 6 : 
Quels paquets proposent de jouer au sudoku ?

Le paquet **sudoku** permet de jouer au Sudoku.
On installe le paquet à l'aide de la commande ```sudo apt install sudoku ```

### Question 7 : 
Lister les derniers paquets installés explicitement avec la commande apt install

Il faut aller regarder dans le fichier **/var/log/apt/history.log** et on voit que les 2 dernier paquets installé par ```apt install ``` sont **fortunes** et **sudoku**.

## Exercice 2. : 
A partir de quel paquet est installée la commande ls ? Comment obtenir cette information en une seule
commande, pour n’importe quel programme (indice : la réponse est dans le poly de cours 2, dans la liste des
commandes utiles) ? Utilisez la réponse à pour écrire un script appelé origine-commande (sans l’extension
.sh) prenant en argument le nom d’une commande, et indiquant quel paquet l’a installée.

Grâce à ```which ls``` on trouve où est stocké la commande ls et ensuite on fait ```dpkg -S /bin/ls ``` pour trouver le paquet est installée la commande. Ce paquet s'appelle **coreutils**.

La commande ```dpkg -S $(wich -a nom_de_la_commande | tail -i) ``` permet en une seule ligne d'afficher dans quel paquet est installée la commande.

On crée le script via la commande ```nano origine_commande.sh ```. Puis on fait ```chmod u+x origine_commande``` pour que le changement se fasse sur le propriétaire (nous) et qu'il puisse s'éxécuter. 

Le script :  
![origine_commande](https://user-images.githubusercontent.com/60732798/76021867-53f23680-5f26-11ea-9f46-00955dec5f5c.png)

Le résultat :  
![result](https://user-images.githubusercontent.com/60732798/76022548-ab44d680-5f27-11ea-8671-62c3809c81b9.png)

## Exercice 3. : 
Ecrire une commande qui affiche “INSTALLÉ” ou “NON INSTALLÉ” selon le nom et le statut du package
spécifié dans cette commande.

On utilise les mêmes commandes pour créer le script et pour changer les permissions.

Le script :  
![install](https://user-images.githubusercontent.com/60732798/76022444-75075700-5f27-11ea-9812-f35693394112.png)

Le résultat :  
![test_install](https://user-images.githubusercontent.com/60732798/76022510-9405e900-5f27-11ea-87ff-c7c58314692d.png)

## Exercice 4. :
Lister les programmes livrés avec coreutils. A quoi sert la commande ’[’ et comment afficher ce qu’elle
retourne ?

On utilise la commande ```dpkg -L coreutils``` qui nous affiche tous les programmes livrés avec coreutils.
La commande **[** permet de réaliser des tests, par exemple ```[ "a" = "a" ]``` teste si la chaine de caractère "a" es la même que "a". Pour afficher ce qu'elle retourne il faut utiliser la commande ```echo $?```.

## Exercice 5. Aptitude : 
Installez le paquet emacs à l’aide de la version graphique d’aptitude.

Pour installer le paquet **emacs** via l'interface graphique aptitude on saisi la commande ``` sudo aptitude ```. Ensuite on cherche le paquets **emacs** puis on l'installe avec la touche **g**.

## Exercice 6. Installation d’un paquet par PPA : 
Installer la version Oracle de Java (avec l’ajout des PPA)

Pour installer Oracle on fait :  
```sudo add-apt-repository ppa:linuxuprising/java ```  
```sudo apt update ```  
```sudo apt install oracle-java11-installer```  

Vérifiez qu’un nouveau fichier a été créé dans /etc/apt/sources.list.d. Que contient-il ?

Un nouveau fichier a bien été créé dans **/etc/apt/sources.list.d** Il contient l'adresse de dépot du répertoire virtuel permettant d'acceder aux différents éléments du répertoire.

## Exercice 7. Création de dépôt personnalisé

### Création d’un paquet Debian avec dpkg-deb

### Question 1 : 
Dans le dossier scripts créé lors du TP 2, créez un sous-dossier origine-commande où vous créerez un
sous-dossier DEBIAN, ainsi que l’arborescence usr/local/bin où vous placerez le script écrit à l’exercice

On se place déjà dans le dossier script :  
```cd ~/script```  

On crée le sous-dossier **origine-commande** suivi d'un autre sous-dossier **DEBIAN** et on place l'arborescence **usr/local/bin** :  
```mkdir -p origine-commande/DEBIAN```  
```mkdir -p usr/local/bin```  

On copie notre script **origine_commande** que l'on place dans le dossier **origine-commande** :  
```cp ~/origine_commande.sh ./origine-commande```  

### Question 2 :
Dans le dossier DEBIAN, créez un fichier control avec les champs suivants :

On se place dans le bon dossier :  
```cd origine-commande/DEBIAN```
On crée le fichier **control** suivant :  
```
vim control 

Package: origine-commande #nom du paquet
Version: 0.1 #numéro de version
Maintainer: SABRAN DUMAS #votre nom
Architecture: all #les architectures cibles de notre paquet (i386, amd64...)
Description: Cherche l'origine d'une commande
Section: utils #notre programme est un utilitaire
Priority: optional #ce n'est pas un paquet indispendable
```  

### Question 3 :
Revenez dans le dossier parent de origine-commande (normalement, c’est votre $HOME) et tapez la
commande suivante pour construire le paquet :
dpkg-deb --build origine-commande
Félicitations ! Vous avez créé votre propre paquet !

On construit le paquet que nous avons créé :  
```
cd $HOME
dpkg-deb --build origine-commande
```
### Création du dépôt personnel avec reprepro

### Question 1 :
Dans votre dossier personnel, commencez par créer un dossier repo-cpe. Ce sera la racine de votre
dépôt

On crée un dossier **repo-cpe** qui sera la racine de notre dépôt puis on se place dedans :  
```
mkdir repo-cpe
cd repo-cpe 
```

### Question 2 :
Ajoutez-y deux sous-dossiers : conf (qui contiendra la configuration du dépôt) et packages (qui contiendra nos paquets)

On crée 2 sous dossiers **conf ** et **packages ** :  
```
mkdir conf
mkdir packages
```
### Question 3 : 

Dans conf, créez le fichier distributions suivant :
Origin: Un nom, une URL, ou tout texte expliquant la provenance du dépôt
Label: Nom du dépôt
// Suite: stable
Codename: cosmic #le nom de la distribution cible
Architectures: i386 amd64 #(architectures cibles)
Components: universe #(correspond à notre cas)
Description: Une description du dépôt

On crée un fichier **distributions** dans **conf** avec comme paramètres :  
```
cd conf 
vim distributions 

Origin: SABRAN DUMAS
Label: repo-cpe
// Suite: stable 
Codename: cosmic #le nom de la distribution cible 
Architectures: i386 amd64 #(architectures cibles) 
Components: universe #(correspond à notre cas) 
Description: Une description du dépôt 
```

### Question 4 : 
Dans le dossier repo-cpe, générez l’arborescence du dépôt avec la commande
reprepro -b . export

On installe la commande **reprepro** puis on génère l'arborescence du dépôt avec la commande ```reprepro -b . export ```

### Question 5 : 
Copiez le paquet origine-commande.deb créé précédemment dans le dossier packages du dépôt, puis,
à la racine du dépôt, exécutez la commande
reprepro -b . includedeb cosmic origine-commande.deb
afin que votre paquet soit inscrit dans le dépôt.

On copie le paquet **origine-commande.deb** et on le met dans la racine et le dossier **packages** avec la commande :  
```
cp ~/script/origine-commande.deb ./packages
cp ~/script/origine-commande.deb 
```
Puis on éxécute la commande pour mettre notre paquet dans le depot :  
```
reprepro -b . includedeb cosmic origine-commande.deb
```

### Question 6 : 
Il faut à présent indiquer à apt qu’il existe un nouveau dépôt dans lequel il peut trouver des logiciels.
Pour cela, créez (avec sudo) dans le dossier /etc/apt/sources.list.d le fichier repo-cpe.list
contenant :
deb file:/home/VOTRE_NOM/repo-cpe cosmic multiverse
(cette ligne reprend la configuration du dépôt, elle est à adapter au besoin)

On crée un nouveau fichier **repo-cpe.list** dans le fichier **/etc/apt/sources.list.d** :   
``` sudo vim /etc/apt/sources.list.d/repo-cpe.list``` et on ajoute la configuration du dépôt 

### Question 7 :
Lancez la commande sudo apt update.
Féliciations ! Votre dépôt est désormais pris en compte ! ... Enfin, pas tout à fait... Si vous regardez
la sortie d’apt update, il est précidé que le dépôt ne peut être pris en compte car il n’est pas signé.
La signature permet de vérifier qu’un paquet provient bien du bon dépôt. On doit donc signer notre
dépôt.

On lance la commande ``` sudo apt update```. Il faut maintenant signer notre dépôt. 

### Signature du dépôt avec GPG

### Question 1 :
Commencez par créer une nouvelle paire de clés avec la commande
gpg --gen-key
Attention ! N’oubliez pas votre passphrase !!!

On génère une nouvelle paire de clé avec les commandes suivantes : 
``` 
gpg --gen-key
Real name: sabran_dumas`
Email address: maxime.dumas@cpe.fr`
o
passphrase : ckali
```

### Question 2 :
Ajoutez à la configuration du dépôt (fichier distributions la ligne suivante :
SignWith: yes

On ajoute **SignWith: yes** au fichier **distributions** 

### Question 3 :
Ajoutez la clé à votre dépôt :
reprepro --ask-passphrase -b . export
Attention ! Cette méthode n’est pas sécurisée et obsolète ; dans un contexte professionnel, on utiliserait
plutot un gpg-agent.

On ajoute la clé à notre dépôt :  
```reprepro --ask-passphrase -b . export```

### Question 4 :
Ajoutez votre clé publique à votre dépôt avec la commande
gpg --export -a "auteur" > public.key

On ajoute notre clé publique à notre dépôt avec la commande :  
```gpg --export -a "auteur" > public.key```

### Question 5 :
Enfin, ajoutez cette clé à la liste des clés fiables connues de apt :
sudo apt-key add public.key
Félicitations ! La configuration est (enfin) terminée ! Vérifiez que vous pouvez installer votre paquet comme
n’importe quel autre paquet.

On ajoute cette clé à la liste des clés fiables connues de apt :  
```sudo apt-key add public.key```

## Exercice 8. Installation d’un logiciel à partir du code source

### Question 1 :
Commencez par cloner le dépôt git suivant :
git clone https://github.com/jubalh/nudoku
Ceci permet de récupérer en local le code source du logiciel nudoku

On clone le dépôt git suivant :  
```git clone https://github.com/jubalh/nudoku ```
On récupère donc le code source de nudoku en local.

### Question 2 :
Rendez vous dans le dossier nudoku qui vient d’être créé et lancez la commande autoreconf -i (ainsi
que spécifié dans le fichier README.md). A vous d’installer les éventuels paquets manquants (un
peu d’aide : pour résoudre le problème de la macro AM_GNU_GETTEXT manquante, installez le paquet
gettext). Relancez la commande autoreconf -i après chaque paquet installé jusqu’à ce
qu’elle se termine sans erreur.
 Cette phase a pour but de traiter le fichier configure.ac fourni, de manière à générer automatiquement un script appelé configure (vous pouvez essayer de faire un cat sur ce fichier configure pour
comprendre le bénéfice de tels outils).


On éxécute la commande ```autoreconf -i``` dans le dossier **nudoku** autant de fois qu'il y a de paquets manquants (on peut aussi utiliser sudo apt install nudoku).

Exécutez le script configure
Cette phase a pour but de préparer la meilleure compialtion possible par rapport à la plateforme
cible, de faire des choix sur les dossier d’installation du logiciel, et de générer automatiquement les
Makefiles adaptés à votre machine. Un Makefile est un fichier utilisé par l’outil make contenant toutes
les directives de compilation d’un logiciel. Un Makefile définit un certain nombre de règles permettant de
construire des cibles. Les cibles les plus communes étant install (pour la compilation et l’installation
du logiciel) et clean (pour sa suppression).
Normalement, à cette étape on exécute la commande make install, qui procède à la compilation
proprement dite et à l’installation (copie des fichiers compilés dans leur dossier de destination). Mais
dans notre cas, on va demander à checkinstall de s’en charger et de créer un paquet au format .deb :
sudo checkinstall
Le logiciel est à présent installé (exécutez nudoku pour vous en assurer) ; on peut vérifier par exemple
avec aptitude qu’il provient bien du paquet qu’on a créé avec checkinstall.
