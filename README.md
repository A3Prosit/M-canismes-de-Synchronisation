

# PROSIT ALLER

## Mots Clés

-   Socket * : combi ip+port, endpoint d'une connexion entre 2 programmes sur un réseau
    
-   Accès concurrent
    
-   IPC
    
-   Client
    
-   IHM
    
-   Logs
    
-   Synchroniser
    
-   Base64 * : code de l'info en 64 char choisi pour être dispo sur la majorité des OS. Ce processus de codage consiste à coder chaque groupe de 24 bits successifs de données par une chaîne de 4 caractères. On concatène 3 octets pour créer un bloc de 24 bits et on le sépare en 4 groupes de 6 bits
    
-   Chat instantané
    
-   UML
    
-   Cypher *: 2 sens: clé de chiffrement ou méthode de chiffrement: algo d'encryption/décryption (cryptage/décyptage, l'autre c'est pas français *derp*)
    
-   TCP
    
-   SocketServeur * CLASSE JAVA
     
-   Pool (thread) * ensemble de thread pret à etre exécutés et libérés pour etre remplacés. Utilie pour ne pas avoir à créer/suppr trop de thread pour les tâches courtes
    
-   IRC * : internet relay chat, protocole de communication textuelle sur internet Il sert à la communication instantanée principalement sous la forme de discussions en groupe par l’intermédiaire de canaux de discussion, mais peut aussi être utilisé pour de la communication de un à un. Il peut par ailleurs être utilisé pour faire du transfert de fichier. concu en 1988
    
-   Logwriter *: objet java.io.Writer, **ch.javasoft.util.logging.LogWriter**
    

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

##   Étudier
### Gestion des threads pool (Java)

`ExecutorService executor = Executors.newFixedThreadPool(5);`
`executor.execute(myWorker);`

on peut implémenter notre propre RejectedExecutionHandler pour gérer les jobs n'ayant pas pu entre dans la queue

```java
RejectedExecutionHandlerImpl rejectionHandler = new  RejectedExecutionHandlerImpl();
//Get the ThreadFactory implementation to use
ThreadFactory threadFactory = Executors.defaultThreadFactory();
//creating the ThreadPoolExecutor
ThreadPoolExecutor executorPool = new ThreadPoolExecutor(2, 4, 10, TimeUnit.SECONDS,new  ArrayBlockingQueue<Runnable>(2), threadFactory, rejectionHandler);`
```


### Socket

combinaison IP+port , endpoint d'une communication à double sens sur un réseau. Permet à la couche TCP d'identifier l'application à laquelle les données sont destinées. On peut identifier une communication TCP de façon unique avec ses 2 endpoints (sockets)


java.net.Socket  qui fournis une implé indépendante de la platefrome
et java.net.ServerSocket qui implé un socket qu'un serveur utilse pour écouter et accepter les connections aux clients 
pour le web on a java.net.URL, URLConnection et URLEncoder

côté serveur:
```java
try ( 
    ServerSocket serverSocket = new ServerSocket(portNumber);
    Socket clientSocket = serverSocket.accept();
    PrintWriter out =
        new PrintWriter(clientSocket.getOutputStream(), true);
    BufferedReader in = new BufferedReader(
        new InputStreamReader(clientSocket.getInputStream()));
) {
```
si on met le port 0 un port libre sera utilisé
on peut aussi utiliser `ServerSocket socketserver = new ServerSocket(numer_port,nbr_max);` pour spécifier le nb maxde connexions simultanées
et `ServerSocket socketserver = new ServerSocket(numer_port,nbr_max,adresse_locale);`


serverSocket fournis une implémentation indépendante du système des sockets côtés serv et client. Il retourne une exception si il ne peut pas écouter un port spécifique 
la méthode accept() attends que le lcient démarre et fasse une requête sur le port serveur et retourne un socket lié au port du serv avec l'adresse et le port client. on peut set un timeout pour ne pas être bloqué à l'infini avec _setSoTimeout_ qui lèvera une InteruptedIOException sans invalider le socket

côté client:

quand le programme client démarre le serv devrait déjà être en train d'écouter, la première chose à faire est donc d'ouvrir un socket connecté au serv

```java
String hostName = args[0];
int portNumber = Integer.parseInt(args[1]);

try (
    **Socket kkSocket = new Socket(hostName, portNumber);**
    PrintWriter out = new PrintWriter(kkSocket.getOutputStream(), true);
    BufferedReader in = new BufferedReader(
        new InputStreamReader(kkSocket.getInputStream()));
)
```
récup les ip: java.net.Inetaddress
-   _getLocalHost()_  : elle retourne un objet qui contient l'adresse IP de la machine locale.
    
-   _getByName(String nom_de_l_machine)_  : elle retourne un objet qui contient l'adresse IP de la machine dont le nom est passé en paramètre.
    
-   _getAllByName(String nom_de_l_machine)_  : elle retourne un tableau d'objets qui contient l'ensemble d'adresses IP de la machine qui correspond au nom passé en paramètre.

peut lever une_UnknownHostException_

-   _BufferedReader_  : cette classe permet de lire des caractères à partir d'un flux tamponné, afin de faire des lectures plus rapides ;
    
-   _InputStreamReader_  : convertit un flux binaire en flux de caractères : elle convertit un objet de type  _InputStream_  en objet de type  _Reader_  ;
    
-   _PrintWriter_ : la classe PrintWriter ajoute à un flux la possibilité de faire des écritures sous forme de texte des types primitifs Java, et des chaînes de caractères.

## Réalisations
### Classer les IPC dans un tableau
### Compléter UML
### Workshop
