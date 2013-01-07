Les Closures
============

La première chose intéressante à propos des closures en JavaScript est qu'ils ne sont pas différents des fonctions normales.
Toutes les fonctions JavaScript sont des fermetures.

Mais qu'est ce que les closures ?
Simplement, une closure vient du mot anglais "close", qui veut dire "fermer". Donc une closure ferme le contexte d'une fonction.

Cela signifie que le scope de la closure contient automatiquement toutes les informations de ses parents.

Pour comprendre ce que cela signifie, nous devons d'abord parler de le scope des variables.

Regardons un autre language : PHP.

PHP dispose de deux principaux scopes pour les variables : le scope Global et le scope de fonction.

le scope par défaut est toujours le scope de fonction (si on ignore les super globales).

Donc, si nous attribuons une variable de l'intérieur d'une fonction, cette variable sera définie uniquement dans le scope de la fonction.

Si l'on voulait que la variable soit plutôt dans le scope global, nous aurions besoin de déclarer notre intention avec le construit "global".

Donc, en PHP, quand nous déclarons une closure, nous avons besoin d'indiquer explicitement les variables à importer à partir de le scope parente.

Ce qui est important a noter ici est que les variables sont imscopes. Les variables sont en fait copiées dans le scope de la closure.

Par ailleurs, dans PHP, chaque scope est complètement indépendant de n'importe quel autre scope. Le seul moyen de lier deux scopes et d'utiliser les references.

Javascript, Par contre, gere les scopes imbriquées. 
Les scopes s'imbriquent la ou elles sont definies.


Donc, si on definit une closure a l'interieur d'une fonction, le scope de la closure va etre imbriquee dans le scope de la fonction.

Ceci signifie que l'acces a  la variable traverse la chaine des scopes parentes jusqu'a ce qu'il trouve le scope la ou la variable a ete definie.

Et du coup, toutes les fonctions qui ont ete definies dans les scopes des autres fonctions sont toujours des closures, meme si ils ont les noms de functions.
Et en considerant que le scope racine est le scope global, toutes les fonctions sont imbriquees dans le scope global.

Et donc, toutes les fonctions dans Javascript sont automatiquement des closures!


And considering that the root scope is the global scope,
All functions are nested inside the global scope.

Therefore, all functions in JavaScript are automatically closures!


