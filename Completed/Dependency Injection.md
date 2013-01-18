Dependency Injection
====================

Qu'est ce que l'injection de dependances?
Litéralement, cela veut dire : injecter des des dependances.
Commençons par definir ce qu'est une dependance. Une dependance est en effet un objet que votre classe necessite pour fonctionner.
Si nous avons une classe modele qui recupere des données depuis un objet Database, nous pouvons dire que ce la classe modele a une dependance a l'objet Database.
Maintenant que nous savons ce qu'est une dependance, voyons ce que veut dire d'injecter des dependances.
Injecter des dependances veut juste dire que la dependance est poussée dans la classe depuis l'exterieur.


Tout ce que cela veut dire est que vous ne devez pas instancier vos dependances (avec le construit new) a l'interieur de vos classes, mais plutôt les récupérer comme un paramètre de constructeur ou un setter.


C'est tout ce que c'est par rapport a l'injection de dependances. Vous n'avez pas besoin d'un "container" super cool ou d'une classe pour faire de l'injection de dependances. C'est sur que votre vie sera meilleure si vous les utilisez, mais ils ne sont pas "necessaires".

Mais pourquoi devons nous injecter des dependances ? 

Let's imagine for a minute that you're programming a house building robot.
Imaginons que nous avons comme tache de programmer un robot de construction de maisons. Nous commençons par une pile de briques, et nous devons construire des murs. Nous arrivons par la suite a mettre la porte de notre maison. Que faisons nous dans ce cas? Est ce que nous construisons une porte a partir de matières premieres? ou que nous programmons notre robot pour récupérer une porte deja prete (qu'un autre fournisseur a construite) et nous ne faisons que l'installer?

La solution la plus flexible, évidemment, serait de récupérer la porte depuis un fournisseur externe.
Et c'est exactement ce que l'injection de dependances fait. Elle decouple la construction de vos classes de la construction de ses dependances.

La raison derriere cette importance est le principe d'Inversion de dependances.
Le principe d'inversion de dependances est le fait que le code doit dépendre d'abstractions. En dépendant d'abstractions, nous découplons nos implementations. 
Ce que cela veut dire, c'est qu'en PHP, votre code doit dépendre d'interfaces. Vous pourrez alors substituer les differentes dependances, du moment qu'ils satisfont l'interface requise.
En utilisant l'injection de dependances, nous découplons le code de l'implementation bas-niveau, ce qui rend le code beaucoup plus elegant, plus facile a modifier et a réutiliser.

Maintenant que nous avons adopté l'injection de dependances, nous avons un autre problème. Chacune de nos classes necessite des dependances. Donc, pour construire chaque classe, nous devons trouver quels sont les dependances dont elles ont besoin et trouver un moyen pour récupérer ces derniers dans la ligne qui les instancie.

Heureusement qu'il ya une solution pour résoudre ce problème : Le conteneur d'injection de dependances, ou plus communèment connu sous "Dependency Injection Container".

Au root de votre application, le container n'est rien d'autre qu'une "carte" des dependances que votre classe necessite, avec la logique necessaire pour les creer si elles ne sont pas encore créées.
A chaque fois que vous demandez une interface "DatabaseInterface", la carte des dependances indiquera quelle dependance utiliser, le container vérifie par la suite si l'objet a été instancié auparavant, et le réutilisé si c'est le cas. Sinon, il va creer l'instance Database, la sauvegarde et la fournit a votre classe.
Donc, au lieu de creer la classe par vous meme, vous demander au container de creer l'instance. Il va résoudre les dependances, construire l'objet et le retourner pour vous.

La meilleure partie est que le container peut résoudre des dependances complexes et c'est transparent! Si vous voulez changer la dependance pour une autre, ou par exemple la mocker dans un test unitaire, tout ce que vous avez a faire est de mettre a jour la dependance dans le container, c'est a une seule place.

Ecrivez donc un code plus propre et plus modulaire, utilisez l'injection de dependance.

