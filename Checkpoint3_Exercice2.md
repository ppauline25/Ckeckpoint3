# Exercice 2 : Manipulations pratiques sur VM Linux  

## Partie 1 : Gestion des utilisateurs  
### Q2.1.1  
En se connectant au root, utilisation de la commande adduser pour créer un compte   
![image](CaptureEcran/Exercice%202/Q.2.1.1.png)
### Q2.1.1  
Je préconise l'ajout de cet utilisateur au groupe sudo pour l'élevélation des droits, ainsi pour eviter qu'il se connecte en root  
![image](CaptureEcran/Exercice%202/Q.2.1.2.png)


## Partie 2 : Configuration de SSH  
### Q2.2.1  
modification du fichier de configuration sshd : permitrootloggin no 
![image](CaptureEcran/Exercice%202/Q.2.2.1.png)
### Q2.2.2  
ajout en bas de fichier : AllowUsers pprak  
![image](CaptureEcran/Exercice%202/Q.2.2.2.png)
### Q2.2.3  
modification des lignes : PubKeyAuthentification yes et PasswordAuthentification no   
![image](CaptureEcran/Exercice%202/Q.2.2.3.png)


## Partie 3 : Analyse du stockage  
### Q2.3.1  
fichier perdu cmd : lancement de la commande `lsblk`  
impossible de retrouver car au moment ou j'ai finalisé la redaction de ce md, j'ai déjà fait des modifications sur le systeme  
### Q2.3.2  
udev utilise **devtmpfs**   
tmpfs (sur /run) utilise **tmpfs**  
/dev/mapper/cp3--vg-root utilise **ext4**    
tmpfs (sur /dev/shm) utilise **tmpfs**   
tmpfs (sur /run/lock) utilise **tmpfs**   
/dev/md0p1 utilise **ext2**  
tmpfs (sur /run/users/0) utilise **tmpfs**   
### Q2.3.3  
ajout du volume dans les configurations de virtual box directement + utilisation de commandes pour réparer le volume RAID  
![image](CaptureEcran/Exercice%202/Q.2.3.3.png)
### Q2.3.4  
dans un premier temps on regarde le volume restant avec `vgs` 
ensuite on créer le volume avec lvcreate  
et on le monte dans le directory avec mount    
on cherche son UUID avec blkid   
on modifie le fichier fstab avec l UUID  
![image](CaptureEcran/Exercice%202/Q.2.3.4-1.png)
![image](CaptureEcran/Exercice%202/Q.2.3.4-2.png)
### Q2.3.5  
Il reste **1.79Go** libre  
On peut le voir en faisant vgs de nouveaux, et on peut constater que VFree a diminué  

## Partie 4 : Sauvegarde  
### Q.2.4.1  
**Bareos-dir** orchestre les sauvegardes : il décide ce qui doit être sauvegardé, dans quel répertoire et a quelle fréquence.  
**Bareos-sd** gere le stockage des sauvegardes, il recoit les données des Bareos-fd de chaque client.   
**Bareos -fd** s'exécute sur chaque machine et envoie les fichiers à sauvegarder aux Bareos-sd   

## Partie 5 : Filtrage et analyse réseau  
### Q.2.5.1  
![image](CaptureEcran/Exercice%202/Q.2.5.1.png)

regles appliquées   
- une table nommé **inet_filter_table**  
- une chaine nommée **in_chain**  
- regles appliqué sur le hook **input**  
- priority filter ?????  
- policy drop : tout ce qui ne correspond pas aux regles seront rejetés par défaut  
### Q.2.5.2 type communication autorisé   
**ct state established, related accept** accepter les connexions déjà établis ou déjà liées  
**iifname "lo" accept** accepter toutes les entrées via l'interface "lo"  
**tcp dport 22 accept** accepter toutes les connexion entrantes en TPC sur le port 22   
**ip protocol icmp accept** accepter toutes les connexions avec le protocol ICMP (pour le ping)   
** ip6 nexthdr ipv6-icmp accept** accepte toutes les connexions avec le protocol imcpv6  
### Q.2.5.3 type communication interdis  
**ct state invalid drop** jeter (sans annoncer au destinataire) toutes les connexions invalides  
### Q.2.5.4  
Ajout d'une table, puis d'une chaine puis des regles  
![image](CaptureEcran/Exercice%202/Q.2.5.4-1.png)
![image](CaptureEcran/Exercice%202/Q.2.5.4-2.png)


## Partie 6 : Analyse des logs  
### Q.2.6.1  
utilisation de la commande lastb  
(au préalable j'ai tenté des connexions avec des mauvais comptes et des faux mdp afin d'avoir du contenu pour cette commande)  
![image](CaptureEcran/Exercice%202/Q.2.6.1.png)

