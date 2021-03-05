# Les dernières avancées du Reinforcement Learning

## Qu'est-ce que le Reinforcement Learning ?

Le Reinforcement Learning ou apprentissage par renforcement est une méthode d’apprentissage automatique consistant en un agent placé au sein d’un environnement avec un objectif. A chaque étape de l’exécution, l’agent réalise une action, qui est choisie selon l’environnement et l’état actuel de l’agent, ce qui lui permet d’interagir avec l’environnement, qui lui renvoie son nouvel état, ainsi qu’un reward, qui peut être positif ou négatif (Figure 1). L’agent a donc pour objectif de maximiser la somme des rewards. Pour illustrer cela par un exemple, si on prend la résolution d’un labyrinthe par RL, l’environnement est le labyrinthe, l’agent la personne qui essaye d’en sortir, les actions sont les déplacements de l’agent, et les rewards sont par exemple négatifs à chaque déplacement, et positif lorsque l’agent atteint la sortie. 

Le RL suit donc un système de trial and error, qui est proche de l’apprentissage traditionnel chez les humains.

<p align="center">
<img src="https://www.kdnuggets.com/images/reinforcement-learning-fig1-700.jpg" alt="RL" width="600" > 
</p>

<p align="center">
Figure 1 : Principe du Reinforcement Learning (source image : [www.kdnuggets.com](https://www.kdnuggets.com/2018/03/5-things-reinforcement-learning.html)
</p>

Depuis quelques années, le RL a été très médiatisé, grâce notamment à des performances comme celles d’Alpha Go (Figure 2), réalisé par une filiale de Google, et qui a battu le champion du monde du jeu de Go en 2017, et c’est donc un champ de recherche assez important, où il y a régulièrement des innovations ou des nouvelles applications, et ce site va vous en présenter quelques unes.


<p align="center">
<img src="http://opendeeptech.com/wp-content/uploads/2018/02/d34887ec89_107368_alphago-kejie-678x381.jpg" alt="AlphaGo" width="600" > 
</p>

<p align="center">
Figure 2 : AlphaGo (source image : [opendeeptech.com](http://opendeeptech.com/fr/alphago-lintelligence-artificielle-de-google)
</p>

## Nouvelles innovations du Reinforcement Learning

### Nouveautés "théoriques"

#### Multi-agent Reinforcement Learning

Le principe du Reinforcement Learning présenté au dessus est celui du Reinforcement Learning avec un seul agent qui interagit avec l’environnement. Cela peut être utile dans certaines situations (par exemple, si on veut résoudre un labyrinthe par Reinforcement Learning, on n’a besoin que d’un seul agent), mais dans de nombreux cas, on veut pouvoir apprendre plusieurs agents différents, qui peuvent collaborer ou être en compétition, selon l’application. C’est beaucoup plus compliqué que du Reinforcement Learning à un seul agent, puisque tous les agents interagissent simultanément avec l’environnement, ce qui fait qu’en plus de devoir tenir compte de leur état et de l’environnement, ils doivent aussi pour être efficace en quelque sorte anticiper les actions des autres agents (figure 3).

<p align="center">
<img src="https://miro.medium.com/max/3000/1*PqoJzG3aX9MXAd_cxf2OTQ.png" alt="MARL" width="600" > 
</p>

<p align="center">
Figure 3 : Principe du Multi-Agent Reinforcement Learning (source image : [medium.com](https://medium.com/@RemiStudios/multi-agent-reinforcement-learning-3f00b561f5f0)
</p>

Une autre problématique importante du Multi-agent Reinforcement Learning est la sécurité. Un certain nombre d’applications du Multi-agent Reinforcement Learning sont safety-critical, c’est-à-dire qu’il y a certains états que ne peuvent pas prendre les agents les uns envers les autres sous peine de conséquences graves. Par exemple, dans le cas des voitures autonomes, si on considère chaque voiture comme un agent, il ne faut pas qu’elles se retrouvent au même endroit au même moment, sinon il y aura un accident. C’est donc quelque chose de très important d’être sûr que ces états non sûrs ne seront jamais pris par les agents, dans l’apprentissage comme durant les tests. Les deux publications que j’ai lue sur ce sujet cherchaient donc à résoudre ce problème, de deux manières différentes. Je ne vais pas rentrer dans les détails, mais globalement pour l’une des deux manières, ils rajoutent un bouclier entre les agents et l’environnement, qui vérifie que les actions vérifient bien les critères de sécurité, qui sont précisé à l’avance, et si ce n’est pas le cas, il modifie l’action non safe, et renvoie une récompense négative à l’agent ayant essayé de la réaliser, pour qu’il apprenne à ne plus faire d’action non safe. 

<p align="center">
<img src="https://i.imgur.com/hc8OybM.png" alt="Shielding MARL" width="600" > 
</p>

<p align="center">
Figure 4 : Shielding pour le Multi-Agent Reinforcement Learning (source image : Safe Multi-Agent Reinforcement Learning via Shielding)
</p>


L’autre manière est plus abstraite, je n’ai pas encore vraiment recherché pour l’instant à essayer de la comprendre, mais dans les deux cas, cela permet d’éviter les états non safe dans le Multi-agent Reinforcement Learning, donc cela peut être une belle avancée dans le domaine du Reinforcement Learning, par exemple dans les domaines de la voiture autonome et de la robotique.

#### Meta Learning

Une autre innovation dans le domaine du Reinforcement Learning est le meta-learning d’algorithmes de Reinforcement Learning. La manière classique de réaliser l’apprentissage d’un algorithme de RL, c’est de choisir un type d’algorithme de Reinforcement Learning (par exemple QLearning, DeepQLearning ou Gradient Policy), puis de choisir les hyperparamètres, puis de tester, puis de changer les hyperparamètres pour que cela marche mieux, etc. jusqu’à tomber sur une solution satisfaisante, ce qui peut être long, et ne garantit pas forcément d’obtenir un résultat concluant à la fin.

Des chercheurs de chez Google ont récemment publié un article sur un méta-apprentissage d’algorithmes de Reinforcement Learning, ce qui pourrait éviter ces problèmes. Globalement, on part d’un certain nombre d’algorithmes de Reinforcement Learning, aléatoires ou connus, on les entraîne sur différents environnements d’entraînement, ce qui permet d’obtenir une fonction de perte (qui est généralisée). On réalise ensuite une mutation sur chacun des algorithmes, on les réentraîne, on recalcule la fonction de perte, etc.. Finalement, après n itérations, on sélectionne l’algorithme qui fonctionne le mieux sur l’ensemble des environnements d’apprentissage. Lors de la phase de test, ils ont ensuite testé l’algorithme sur d’autres environnements, et cela a donné des bons résultats, donc l’algorithme trouvé est bien généralisable.

<p align="center">
<img src="https://i.imgur.com/dzAIt7H.png" alt="Metalearning" width="600" > 
</p>

<p align="center">
Figure 4 : Meta Learning (source image : Evolving Reinforcement Learning Algorithms)
</p>


Un problème est évidemment le temps de calcul, vu que cela a duré 72h en utilisant plus de 300 CPUs, donc même si le principe est intéressant et une grosse avancée, il semble pour l’instant compliqué à mettre en œuvre.


### Nouvelles applications

#### Le Reinforcement Learning pour lutter contre les injections SQL

Le Reinforcement Learning peut permettre de lutter contre les injections SQL en les simulant via un algorithme de RL. Commençons par présenter rapidement les injections SQL : il s’agit d’une méthode d’exploitation de failles de sécurité dans un système avec une base de données, qui permet à l’attaquant, via des requêtes SQL non prévues par le système, d’accéder à des données qu’il n’est pas censé pouvoir voir, voire modifier ou supprimer des données.

Voici un exemple simple d’injection SQL, tiré de Wikipédia : dans le cas où, pour un système d’identification, le code fait simplement une requête SQL avec le nom et le mot de passe (haché en MD5) pour vérifier si l’utilisateur a le droit de se connecter ou non :

Nom : Dupont MDP : truc

SELECT uid FROM Users WHERE name = 'Dupont' AND password = '45723a2af3788c4ff17f8d1114760e62';


Il suffit  alorsde rentrer un nom de ce style, avec apostrophe, point-virgule et 2 tirets à la fin, ce qui aura pour effet de commenter la fin de la requête SQL, et donc l’attaquant pourra accéder aux données de l’utilisateur sans avoir son mot de passe. 

Nom : Dupont';-- MDP : peu importe

SELECT uid FROM Users WHERE name = 'Dupont’;-- ' AND password = '45723a2af3788c4ff17f8d1114760e62'; 

SELECT uid FROM Users WHERE name = 'Dupont’; 

Evidemment, ce n’est qu’un exemple simple d’injection SQL, il en existe de beaucoup plus compliqué, et c’est justement là où intervient le RL. L’objectif est de simuler des injections SQL via RL : le problème est modélisé comme un problème de Capture The flag : l’agent envoie des requêtes SQL à l’application (qui sont donc ses actions) avec comme objectif d’obtenir un certain résultat, qui est le drapeau à capturer en quelque sorte. La fonction de reward est donc positive si l’agent réussit son injection SQL, et négative sinon. En utilisant des algorithmes classiques de RL (Qlearning et Deep QLearning), les chercheurs ont réussi à obtenir des résultats concluants lors de leurs tests, avec l’algorithme qui réussit assez rapidement à trouver l’injection SQL pour récupérer la donnée souhaitée.

Ce n’est que le début de leurs recherches sur le sujet, et donc il y a quelques limitations pour l’instant : par exemple, les tests ont été réalisés dans un environnement statique, qui ne réagit pas aux attaques de l’algorithme, ce qui n’est pas forcément le cas pour des applications réelles. De plus, l’algorithme a été utilisé dans un cas où il y avait une vulnérabilité aux injections SQL, et l’algorithme avait donc juste à trouver quelle requête pouvait l’exploiter.
Dans tous les cas, si les chercheurs réussissent à généraliser l’algorithme, ce sera une avancée dans le domaine de la cybersécurité, en plus du domaine du RL.


