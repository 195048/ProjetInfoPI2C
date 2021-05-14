# ProjetInfoPI2C
Projet d'informatique ayant pour but de créer une IA pour le jeu abalone.

Le but principal de cet IA est de déterminer le coup le plus intéréssant à jour dans le but de gagner la partie.

## Bibliothèques utilisées : 

Voici une liste des bibliothèques utiliseés dans le cadre du projet et une brève déscription de celle-ci : 
1) 'socket' :
2) 'threading' :
3) 'sys' : 
4) 'copy' :
5) 'time' :
6) 'sqrt' de 'math' : 
7) 'defaultdict' de 'collections' : 
8) 'json' : 
9) 'random' : 

## Subdivision du code : 

1) Game.py :  
2) JsonNetwork : 
3) IA : 
4) Client : 


## Démarrage de l'IA : 
Tapez la ligne de commande dans un terminal : 

python .\clientfinal.py port -name=nom_désiré

Le port par défaut est le 3100 et le nom par défaut est "195048,195178"

## Listes des requêtes / réponse : 

### Inscription : 

Afin de pouvoir jouer, le client doit s'inscrire sur celui-ci. Pour cela, il doit envoyer un message sous format Json au serveur contenant ses données, en communiquant au serveur qui se trouve sur le port 3000.

Contenu du message : 

```json
{
"request": "subscribe",
"port": port,
"name": name,
"matricules": ["195048", "195178"]
}
```

Par défaut, les variables port et name sont réspectivement : 3100 et "195048,195178".

Si tout se passe corrèctement, le serveur répond : 

```json
{
   "response": "ok"
}
```


### Verification de la présence : 


 Afin de vérifier si le client est toujours connecté, le serveur envoit régulièrement des requète "ping" sur le port mentionné lors de l'inscription, auquelle nous devons répondre "pong"

Requète ping : 

```json
{
   "request": "ping"
}
```
Réponse : 

```json
{
   "response": "pong"
}
```

### Requête de coup : 



Lorsque c'est au tour du joueur de donner son coup, le serveur envoit une requête play au client qu idevra renvoyer son coup dans les 3 secondes suivantes.


Requête play du serveur : 

```json
{
   "request": "play",
   "lives": 3,
   "errors": list_of_errors,
   "state": state_of_the_game
}
```

La variable lives donne le nombre de vies restantes du joueur, chaque joueur a 3 vies par match et en perd une à chaque mauvais mouvement effectué. Si le nombre de vies tombe à 0, le joueur perd.

La variable errors liste les raisons pour lesquelles les coups joués étaient mauvais.

La variable state donne l'état du je, elle contient différentes infos nécéssaire au client afin qu'il puisse décider comment jouer. 

Contenu de state : 

```json
{
   "players": ["LUR", "LRG"],
   "current": 0,
   "board": [
      ["W", "W", "W", "W", "W", "X", "X", "X", "X"],
      ["W", "W", "W", "W", "W", "W", "X", "X", "X"],
      ["E", "E", "W", "W", "W", "E", "E", "X", "X"],
      ["E", "E", "E", "E", "E", "E", "E", "E", "X"],
      ["E", "E", "E", "E", "E", "E", "E", "E", "E"],
      ["X", "E", "E", "E", "E", "E", "E", "E", "E"],
      ["X", "X", "E", "E", "B", "B", "B", "E", "E"],
      ["X", "X", "X", "B", "B", "B", "B", "B", "B"],
      ["X", "X", "X", "X", "B", "B", "B", "B", "B"]
   ]
}
```

La variable Players donne les noms des joueurs inscris au match, le premier joueur représente celui qui joueura en premier avec les pions noirs. 

Current représente l'indice dans la liste Players du joueur devant jouer.

Board représente le tableau de jeu. 


### Réponse move

Le client répond par le coup souihaité : 

Exemple de coup : 

```json
{
   "marbles": [[1, 1], [2, 2]],
   "direction": "SE"
}
```

Marbles liste les marbres que l'on souhaite bouger, ils sont donné sous la forme d'une liste de liste. Les sous-listes représentent un marbre, ils sont donnés sous forme [ligne,colonne]. La liste principale liste tout les marbres que l'on souhaite déplacer. 

Direction donne la direction dans laquelle les marbres doivent se déplacer.




## Stratégie pour la génération des coups :

Afin de génerer le meilleur coup, l'IA 





