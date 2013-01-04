References en PHP
=================

Pour explorer comment les références fonctionnent en PHP, dous devons d'abord prendre un peu de recul et jeter un oeil à la façon dont les variables fonctionnent en PHP.
Typiquement, on nous apprend à visualiser une variable un récipient pour une valeur nommée. Mais nous nous trouvons souvent dans une situation où nous avons besoin de copier une variable.

Les copies peuvent être aussi simples comme affecter une variable à l'autre. Mais les copies peuvent également se produire dans d'autres situations, tels que lors du passage d'une variable à une fonction,lors du retour d'une variable à partir d'une fonction
Ou lors de l'itération sur un tableau.

Alors, quand on copie une variable, on copie la valeur contenue aussi bien. Et cela fait sens. Si nous avons deux variables différentes avec des noms différents, nous nous attendons a avoir des conteneurs  différents.

Donc, si nous éditons un conteneur, nous nous attendons que l'autre reste le même. Mais cela a des problèmes aussi, chaque fois que nous copions une variable, nous avons besoin de dupliquer la valeur contenue.

Cela peut conduire à une duplication grave de zones mémoire, ce qui peut entraîner des problèmes de performances.
PHP résout ce problème en séparant la variable du conteneur valeur. Les variables deviennent alors  des pointeurs vers une valeur. Quand on copie une variable, nous copions tout simplement ce pointeur.
Cela introduit un nouveau problème: lorsque nous supprimons une variable, Comment pouvons-nous savoir si nous pouvons supprimer la valeur?

La façon dont PHP résout ce problème est de maintenir un comptage du nombre de références à une valeur. Ainsi, le conteneur valeur, dispose désormais de deux champs:  La valeur elle-même,et un compteur de référence, aussi connu comme un "refcount". Chaque fois que nous copier une variable, nous augmentons le refcount, et chaque fois que nous supprimons une variable, nous diminuons le refcount. Si le refcount arrive a 0, on peut sans risque supprimer la valeur. 
Mais nous avons aussi un autre problème. Si nous modifions la copie d'une variable, nous faisons aussi éditer l'original puisqu'ils utilisent le conteneur même valeur.

Heureusement, nous avons déjà une façon de régler ce problème. Le "refcount"  peut nous indiquer quand nous pouvons modifier ou quand nous avons besoin de copier la valeur.

Ainsi, lorsque nous éditons une valeur, si le refcount est 1, nous pouvons modifier directement la valeur.

Si le refcount est supérieur à 1, nous avons besoin de copier la première valeur, et puis, nous pouvons modifier la copie.

Ceci est également connu sous le nom "copy on write". 

Jusqu'ici tout va bien.

Maintenant, qu'est-ce qui se passe lorsque nous voulons deux variables pour pouvoir les éditer ensemble en même temps?
En PHP, nous allons utiliser l'opérateur de référence eperluette.

Mais qu'est ce qui est fait que sous le capot?
Eh bien, pour mettre en œuvre cette fonctionnalité, tout ce que nous devons faire est de désactiver la copie-sur-écriture.
Mais nous ne voulons le désactiver que pour les valeurs référencées.

La façon pour atteindre ce but est d'ajouter un champ supplémentaire dans le récipient valeur. Il s'agit d'une valeur booléenne simple, que nous appellerons "is_ref".

Si is_ref est vrai alors que nous éditons un varible, nous ne copions pas la première valeur.

Mais maintenant qu'est ce qui se passe si nous essayons de faire une copie normale d'une valeur de référence?
Nous ne pouvons pas augmenter le refcount, car alors nous ferions une référence à la place.

Nous avons donc besoin de faire une copie complète de la valeur. Par conséquent, à chaque fois que nous utilisons des références,
Nous perdons tous les avantages que copy-on-write nous donne.
En PHP4, c'est ainsi que toutes les variables sont gerees. 

A partir de PHP5, les objets sont traités d'une manière légèrement différente. Au lieu de stocker l'objet sur la meme valeur,
il ya une deuxième couche d'abstraction. Les objets sont stockés dans leur propre conteneur et pointés par la valeur.
Qu'est-ce que cela signifie pour nous, c'est que même si on copie une variable objet, tous les contrôles vont encore à la même place.
Donc, nous n'avons pas besoin d'utiliser des références variables du tout lorsqu'il s'agit d'objets.
Si nous voulons faire une copie d'une valeur de l'objet, nous avons besoin d'utiliser le "clone" de l'opérateur.

Lors de l'écriture moderne du code PHP, il ne faut donc pas essayer de déjouer le système.
L'utilisation de références pour tenter de sauver la mémoire finira en général par vous coûter plus de mémoire.
Laissez PHP manipuler des variables pour vous, Il est plus intelligent que vous le pensez.
