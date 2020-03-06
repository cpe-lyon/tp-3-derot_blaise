# TP3 Gestion des paquets 

## Exercice 1. Commandes de base

Commencez par mettre à jour votre système avec les commandes vues dans le cours.
Donnez les commandes répondant aux questions suivantes :

>jean-baptiste@serveur:~$ sudo apt update



1. Quels sont les 5 derniers paquets installés sur votre machine ?



2. Utiliser dpkg et apt pour compter le nombre de paquets installés (ne pas hésiter à consulter le manuel !).
Comment explique-t-on la (petite) différence de comptage ?


>jean-baptiste@serveur: ~$dpkg -l | wc -l  
>548  
>jean-baptiste@serveur: ~$ apt list -i |wc -l    
>544    
>  
>Cette différence est due au fait que dpkgne gère pas les dépendances.


3. Combien de paquets sont disponibles en téléchargement ?


>jean-baptiste@serveur:~$ apt list | wc -l  
>  
>64118


4. Créer un alias “maj” qui met à jour le système

>Aller dans le fichier .bashrc : jean-baptiste@serveur:~$ nano .bashrc  
>On écrit à la fin : alias maj="sudo apt full-upgrade"  
>La commande source ~/.bashrc permet d'enregistrer


5. A quoi sert le paquet fortunes ? Installez-le.

>sudo apt install fortune

6. Quels paquets proposent de jouer au sudoku ?

>sudo apt install sudoku

7. Lister les derniers paquets installés explicitement avec la commande apt install

>grap 'apt install' /var/log/apt/history.log  
>  
>commandline: apt install fortune   
>commandline: apt install sudoku


## Exercice 2.

**A partir de quel paquet est installée la commande ls ? Comment obtenir cette information en une seule
commande, pour n’importe quel programme (indice : la réponse est dans le poly de cours 2, dans la liste des
commandes utiles) ?**

>serveur@serveur: $ which -a ls | tail -n 1 | xargs dpkg -S   
>coreutils: /bin/ls  

**Utilisez la réponse à pour écrire un script appelé origine-commande (sans l’extension
.sh) prenant en argument le nom d’une commande, et indiquant quel paquet l’a installée.**

>if [ -z "$1" ]; then  
>        echo "no argument, provide a command name."  
>else  
>        which -a "$1" | tail -n 1 | xargs dpkg -S  
>fi  

## Exercice 3.

**Ecrire une commande qui affiche “INSTALLÉ” ou “NON INSTALLÉ” selon le nom et le statut du package
spécifié dans cette commande.**

>!/bin/bash  
>if [ -z "$1" ]; then  
>        echo "Non installé."  
>else  
>        dpkg -S $(which "$1");  
>        echo "Installé";  
>fi  


## Exercice 4.

**Lister les programmes livrés avec coreutils. A quoi sert la commande "[" et comment afficher ce qu’elle retourne ?**

>apt show coreutils  
>
>La commande "[" permet d'écrire des conditions.


## Exercice 5. aptitude

**Installez le paquet emacs à l’aide de la version graphique d’aptitude.**

>On installe aptitude  
>apt install aptitude  
>  
>On utilise la fonction pour checher emacs  
> /  
>  
>On selectionne les paquets avec   
>+    
>  
>On installe avec   
>g  


## Exercice 6. Installation d’un paquet par PPA

**1. Installer la version Oracle de Java (avec l’ajout des PPA)**

>sudo add-apt-repository ppa:linuxuprising/java  
>sudo apt update  
>sudo apt install oracle-java11-installer  


**2. Vérifiez qu’un nouveau fichier a été créé dans /etc/apt/sources.list.d. Que contient-il ?**

>linuxuprising-ubuntu-java-disco.list

