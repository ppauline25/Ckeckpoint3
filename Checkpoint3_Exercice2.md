# Exercice 2 : Manipulations pratiques sur VM Linux (

## Partie 1 : Gestion des utilisateurs
### Q2.1.1
### Q2.1.1


## Partie 2 : Configuration de SSH
### Q2.2.1
### Q2.2.2
### Q2.2.3


## Partie 3 : Analyse du stockage
### Q2.3.1
### Q2.3.2
udev utilise **devtmpfs**   
tmpfs (sur /run) utilise **tmpfs**
/dev/mapper/cp3--vg-root utilise **ext4**   
tmpfs (sur /dev/shm) utilise **tmpfs**   
tmpfs (sur /run/lock) utilise **tmpfs**   
/dev/md0p1 utilise *ext2**  
tmpfs (sur /run/users/0) utilise **tmpfs**   
### Q2.3.3
### Q2.3.4
### Q2.3.5
Il reste **1.79Go** libre 

## Partie 4 : Sauvegarde
### Q.2.4.1
**Bareos-dir** orchestre les sauvegardes : il décide ce qui doit être sauvegardé, dans quel répertoire et a quelle fréquence. 
**Bareos-sd** gere le stockage des sauvegardes, il recoit les données des Bareos-fd de chaque client.  
**Bareos -fd** s'exécute sur chaque machine et envoie les fichiers à sauvegarder aux Bareos-sd 

## Partie 5 : Filtrage et analyse réseau
### Q.2.5.1 
regles appliquées 
- une table nommé **inet_filter_table**
- une chaine nommée ** in_chain**
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

## Partie 6 : Analyse des logs
### Q.2.6.1
