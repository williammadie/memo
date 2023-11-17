# Design Patterns

## Table of Contents

- [Creational Design Patterns](#creational-design-patterns)
    - [Singleton](#singleton)
- [Message Construction](#message-construction)
    - [Command Message](#command-message)
    - [Document Message](#document-message)
    - [Event Message](#event-message)
    - [Request Reply](#request-reply)
    - [Correlation Identifier](#correlation-identifier)
    - [Message Sequence](#message-sequence)
    - [Format Indicator](#format-indicator)

## Creational Design Patterns

### Singleton

It is one of the simplest **design pattern**. Its goal is to ensure that a class has **only one instance** while providing a global access point to this instance.

```php
$pdo = null;

function getPDO() {
    if ($pdo == null) {
        ...
    }
    return $pdo;
}
```

## Message Construction

### Event Message

Commentaires du prof: retirer le qualificatif "fiable" parce que dans le cadre du Pub-Sub si on est pas co au topic lorsque le message est envoyé, on ne reçoit rien.

synchrone: RPC (on envoie un truc, le gars traite en direct et on reçoie une réponse. La connexion reste ouverte tant que la demande n'a pas été traitée)

asynchrone: messaging (on envoie un truc, le gars le traite dans le futur, on ne sait pas quand, et nous répond, on ne sait pas quand).

peut s'utiliser avec P2P Channel, Pub-Sub Channel, Observer et Request-Reply

Précise dans le header que l'on attend pas de réponse
```java
?exchangePattern=InOnly
```

### Document Message

Objectif: Transférer des structure de données entre application

La partie importante du pattern c'est **le contenu du message**. Ce contenu, c'est un **objet unique**.

S'utilise avec le Point-to-Point Channel ou le Pub-Sub Channel.

RPC: protocole réseau permettant de faire des appels de procédures sur un ordinateur distant

L'étape la plus importante de ce pattern, c'est **le transfert du document**.

### Command Message

Objectif: donner une instruction à une autre application.

C'est un message contenant une commande destinée à un application distante.

Limites:
- demander à une app distante d'exécuter des commandes en asynchrone, c'est pas terrible parce qu'on ne sait pas quand elle sera exécutée.
- on ne reçoit pas forcément une réponse

### Request Reply

Objectif: Avoir une communication bidirectionnelle (une requête et une réponse)

Classiquement, on a un un seul tuyau pour envoyer un message (unidirectionnel). Ici, on rajoute un tuyau pour recevoir les réponses.

Ce design pattern peut être **synchrone** ou **asynchrone**. On utilise des channels de message pour communiquer (P2P ou Pub-Sub Channels)

La requête peut être un Command Message, un Document Message ou un Event Message

### Return Address

Objectifs: Permettre au destinataire de notre message d'envoyer sa réponse à une autre application.

On spécifie l'addresse de réponse dans **le header** de notre message.

**Méthode n°1**

Préciser l'adresse de retour (côté expéditeur)
```java
requestMessage.setJMSReplyTo("M1.reply-facturation");
```

Obtenir l'addresse de retour (côté destinataire)
```java
reqMess.getJMSReplyTo();
```

**Méthode n°2**

Ici, on a même pas besoin de définir l'adresse de retour !
Le process va attendre la réponse du `.to()`
```java
from("direct:facture")
.to("sjms2:M1.facture")
.process(new Processor() {...});
```

Limites: Il faut vérifier qui écrit l'adresse de retour parce que si on laisse n'importe qui la définir, ça peut être une faille de sécurité.

### Correlation Identifier

Objectif: Identifier uniquement chaque requête de manière à pouvoir répondre à une requête spécifique.

On le met en place en générant un identifiant avec la concaténation de l'horodatage et d'un UUID et on le rajoute dans le header de la requête.

### Message Sequence

Objectif: Découper un message volumineux en plusieurs message légers.

On découpe le message trop lourd en plusieurs messages.

On ajoute un booléen qui sert d'indicateur de fin dans le header. On met cet indicateur à `False` pour tous les messages sauf le dernier. 

### Message Expiration

Objectif: Indiquer à partir de quand un message doit être considéré comme obsolète.

On définit la date d'expiration grâce au TTL (Time To Live). Si le message est expiré, le message est redirigé vers le *Dead Letter Channel*.

Le TTL peut être une valeur **absolue** ou **relatif**:
- absolue: datetime
- relatif: heure d'envoie + durée

Le TTL est infini par défaut en Apache Camel.

**C'est le broker** qui redirige les messages vers le **Invalid Message Channel** et le **Dead Letter Channel**.

On ajoute un paramètre dans notre `.to()`
```java
timeToLive=5000
```

### Format Indicator

Objectif: comment permettre une flexibilité future vis à vis du format de données d'un message

On ajoute un **indicateur de format** dans le header ou dans le body du message: ça peut être:
- un no Version
- une clef étrangère

On l'utilise lorsque notre format de données est susceptible d'évoluer.