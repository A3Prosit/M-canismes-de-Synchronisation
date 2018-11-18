
# PROSIT ALLER

## Mots Clés

-   Socket * : @IP + n° port - Point de fin dans une communication à travers un réseau sur internet.
    
-   Accès concurrent
    
-   IPC
    
-   Client
    
-   IHM
    
-   Logs
    
-   Synchroniser
    
-   Base64 * : encodage binaire vers texte, qui représente la donnée en ASCII, en la traduisant en un base64 (radix64).
    
-   Chat instantané
    
-   UML
    
-   Cypher * : Chiffrement. C'est un langage informatique de requête orienté graphe, utilisé par Neo4j (SGBD open source basé sur les graphes)
    
-   TCP
    
-   SocketServeur * : Point de fin pour recevoir/ envoyer des données avec un noeud côté serveur.
    
-   Pool (thread) * : piscine de thread (vu après)
    
-   IRC * : Internet Relay Chat, couche applicative qui facilite les communications via des échanges textuels. Basé sur un modèle réseau client/serveur. Les clients passent par des serveurs pour transférer leurs messages vers d'autres clients.
    
-   Logwriter * : Ecriture de logs
    

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


## Gestion des threads pool (Java)

Un thread pool est un design pattern logiciel, pour gérer la concurrence d'exécution dans un programme ordinateur. 
- Appelé aussi "replicated workers" ou "Worker-crew-model"

**Fonctionnement**
- Groupe de thread pré-instancié, prêt à exécuter des tâche.
- On passe par eux pour des petites exécutions plutôt création/destruction nouveau thread7
- 
Permet de :
- Augmenter les performances
- Éviter les latences dans l'exécution du aux créations/destructions trop fréquentes pour des petites tâches

Le nombre de threads à l'écoute dépend des ressources de l'ordinateur disponible pour le programme.

**java.util.concurrent.Executors** provide implementation of **java.util.concurrent.Executor** interface to create the thread pool in java.

Principe d'une pool de thread :
- Moyen de créer des threads et de les maintenir dans un état inactif jusqu'à appelé :
	- On les faits attendre à une barrière jusqu'à que la pool effectue ses actions (ex : mutex)
- Un container pour enregistrer les threads crées, pour pouvoir en tirer une quand on le souhaite
- Une interface standard ou classe abstraite pour effectuer les tâches

On ajout la tâche que l'on souhaite exécuter de manière asynchrone dans la task queue

Méthode clasique :
- Planifier grâce à une queue synchronisé (task queue)
- Les threads dans la pool retirent les tâchent qui attendant dans la queue, et les place dans "completed task" après leurs exécutions.
![](https://upload.wikimedia.org/wikipedia/commons/thumb/0/0c/Thread_pool.svg/400px-Thread_pool.svg.png)

## Socket Java

**Fonctions de base**
Une classe IntetAddress permet de manipuler les @IP
- getLocalHost() : retourne un objet contenant l'@IP de la machine locale
- getByName(string nom_machine) : retourne un objet de l'@IP de la machine du nom rentré en paramètre
- getAllByName(string nom_machine) : retourne un tableau d'objets qui contient l'ensemble d'@IP  de la machine qui correspond au nom rentré en param

Après avoir récupéré un objet : 
- getHostName() : retourner le nom de la machine
- getAddress : retourner @IP tableau 4 octets
- toString() : retourner un string qui correspond au nom de la machine et son address


**Connecter deux socket entre elle**
Un socket est un point de terminaison d'une communication "bidirectionnelle" (client & serveur) sur un même réseau. Les deux sont liés par un même numéro de port TCP.

Serveur --> Ecouter client : 
- ServerSocket socketserver = new ServerSocket(numero_port); //Si à 0, créer sur n'importe quel port libre
- ServerSocket socketserver = new ServerSocket(numer_port,nbr_max_connexion simultanée);
- ServerSocket socketserver = new ServerSocket(numer_port,nbr_max,adresse_locale);

Socket client :
- Socket socket = new Socket(identité_client, n°port)
- Socket socket = new Socket(adresse_distante, port_distant, adresse_locale, port_locale)

Accepter une demande client (serveur) 
- Socket socketduserveur = socketserver.accept(); //Méthode accept reste bloquante tant qu'elle n'a pas détecté de connexion, on peut utiliser setSoTimeout() pour définir un timeout
⇒ Si connexion acceptée, socket client et serveur communiquent.

**Echange de message**

- Gestion des flux :
	- getInputStream() : gérer les flux entrant
	- getOutputStream() : gérer les flux sortant
	

	- BufferedReader = Classe permettant de lire des caractères (plus rapide pour lire)
	- InputStreamReader = convertit flux binaire en flux caractère
	- PrintWriter : Classe, ajoutant à un fux la possibilité de faire des écritures sous forme de texte des primitives Java.


![](https://user.oc-static.com/files/192001_193000/192110.png)

## Classer les IPC :




