
# PROSIT ALLER

## Mots Clés

-   Socket *
    
-   Accès concurrent
    
-   IPC
    
-   Client
    
-   IHM
    
-   Logs
    
-   Synchroniser
    
-   Base64 *
    
-   Chat instantané
    
-   UML
    
-   Cypher *
    
-   TCP
    
-   SocketServeur *
    
-   Pool (thread) *
    
-   IRC *
    
-   Logwriter *
    

\* à définir

## Contexte

Quoi ?

-   1 application de chat instantané

Comment ?

-   Utiliser thread + socket + IPC en les synchronisant

Pourquoi ?

-   Pour répondre à la demande du client

## Contraintes

-   Java
    
-   2 jours

## Problématique

-   Comment synchroniser les processsssssus communicants sur un serveur ?
    
-   Comment manipuler des sockets et comment fonctionne 1 pool de thread ?
    
-   Comment synchroniser les sockets et thread ?

## Généralisation

-   Synchronisation
    
-   Conception
    
-   Design – Modélisation


## Hypothèses

-   Les IPC peuvent nous aider à gérer les threads à travers le réseau.
    
-   Les IPC peuvent nous aider à gérer l’accès aux fichiers
    
-   Il existe déjà des implémentations qui permettent au thread d’un thread pool de communiquer.
    
-   Il y a un buffer sur le socket et il est utilisé pour tout traiter d’un coup.
    
-   On peut utiliser une pool de port (socket) avec un système de synchonisation

## Plan d’Action

-   Étudier
-   Gestion des threads pool (Java)
-   Socket
-   Réalisations
-   Classer les IPC dans un tableau
-   Compléter UML
-   Workshop
