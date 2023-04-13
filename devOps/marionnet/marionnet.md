# Marionnet

## Sommaire

1. [Les Routeurs Zebra](#routeurs-zebra)

## Les Routeurs Zebra <a name="routeurs-zebra"></a>

### Les différents modes du Routeur

|           MODE           |                     Actions possibles                          |      Prompt           |
|:------------------------:|:--------------------------------------------------------------:|:---------------------:|
|       CONSULTATION       |                     consulter état routeur                     |      MonRouteur>      |
|        PRIVILEGIE        | obtenir l'autorisation de modifier les informations du routeur |      MonRouteur#      |
|       CONFIGURATION      |                         modifier routes                        |  MonRouteur(config)#  |
| CONFIGURATION INTERFACES |               modifier config interfaces routeur               | MonRouteur(configif)# |

### Passer d'un mode à l'autre

Pour passer d'un mode à l'autre, il faut nécessairement passer d'une bulle à l'autre. Il n'est pas possible de passer directement du mode **consultation** au mode **configuration interface**.

![img_1](/networks/marionnet/resources/routeur.jpg)

Le mode **consultation** est le mode par défaut.

- `enable`  passer en mode **privilégié**
- `disable` passer en mode **consultation**
- `configure terminal` passer du mode **privilégié** au mode **configuration**
- `interface nom_interface` passer du mode **configuration** au mode **configuration**

### Configurer un routeur
