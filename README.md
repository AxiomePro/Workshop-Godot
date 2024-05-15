# Workshop sur Godot

Bienvenue dans ce workshop sur Godot ! Au cours de cette session de 2h30, nous explorerons les bases de Godot, un moteur de jeu open-source et gratuit, afin de vous familiariser avec son fonctionnement et ses fonctionnalités.


## Prérequis
Avant de commencer ce workshop, assurez-vous d'avoir installé Godot sur votre ordinateur.
> [!NOTE]
> Vous pouvez le télécharger depuis le [site officiel de Godot](https://godotengine.org/download)


## Structure du Workshop
Ce workshop est divisé en plusieurs étapes, chacune couvrant un aspect spécifique de Godot. Chaque étape comprend une description suivie d'un exercice pratique.
> [!TIP]
> Une documentation est présente (ci-dessous)

> [!IMPORTANT]
> N'hésitez pas à poser des questions


## Étapes

### 1. Introduction à Godot
**Description:** Dans cette étape, nous découvrirons l'interface de Godot et apprendrons à créer un nouveau projet.
  - [ ] Ouvrez Godot et sélectionnez "Nouveau Projet".
  - [ ] Choisissez un emplacement pour votre projet et donnez-lui un nom.
  - [ ] Explorez l'interface utilisateur de Godot, y compris les différents panneaux et menus.


### 2. Création d'une scène
**Description:** Apprenez à créer des scènes, les éléments de base de tout jeu dans Godot.
  - [ ] Dans votre nouveau projet, créez une nouvelle scène en cliquant sur "Nouvelle Scène".
  - [ ] Enregistrez votre scène et nommez-la "Player.tscn".


### 3. Gestion des mouvements d'un player
**Description:** Explorez les concepts de mouvement et de physique dans Godot.

#### Mise en place de l'environnement
  - [ ] Ajoutez un nœud "StaticBody3D" nomé "floor" pour créer un sol.
  - [ ] Dans votre "floor", ajoutez un nœud "MeshInstance3D" nomé "mesh" et sélectionnez la forme "BoxMesh" puis agrandissez le pour faire une platforme suffisament grande.
  - [ ] Dans votre "mesh", séléctionez "Maillage" puis "Créer une collision sœur convexe simplifiée".

#### Mise en place du player
  - [ ] Ajoutez un nœud "CharacterBody3D" nomé "player" pour gérer les mouvements.
  - [ ] Dans votre "player", ajoutez un nœud "MeshInstance3D" nomé "mesh" et sélectionnez la forme "CapsuleMesh" pour lui donner une forme.
  - [ ] Dans votre "mesh", séléctinez "Maillage" puis "Créer une collision sœur convexe simplifiée".
  - [ ] Dans votre "player", ajoutez un nœud "Node3D" nomé "head" pour créer une tête qui pourras tourner sur elle même. Placez-la à hauteur de tête sur votre "player".
  - [ ] Dans votre "head", ajoutez un nœud "Caméra3D" nomé "camera" pour ajouter une pov.

#### Ajout d'un script pour le déplacement du player
> [!WARNING]
> Si une fonction évoquée n'existe pas, créez la avec la syntaxe ```func <nom de fonction>(<parametres>):```
  - [ ] Attachez un script dans votre "player" et nommez-le comme proposé, "player.gd".
  - [ ] Dans la function ```_ready():``` écrivez ```Input.set_mouse_mode(Input.MOUSE_MODE_CAPTURED)``` pour cacher votre curseur.
  - [ ] Au début du script écrivez ```const SPEED = 10.0``` pour définir la vitesse de votre player.
  - [ ] Dans la function ```_physics_process(delta):``` écrivez ```var input_dir = Input.get_vector("ui_left", "ui_right", "ui_up", "ui_down")``` pour récupérer votre input.
  - [ ] Au début du script écrivez ```@onready var head = $head``` pour créer un lien avec votre "head".
  - [ ] Dans la function ```_physics_process(delta):``` écrivez ```var direction = (head.transform.basis * Vector3(input_dir.x, 0, input_dir.y)).normalized()``` pour transformer votre input en vecteur.
  - [ ] Dans la fonction ```_physics_process(delta):``` écrivez
```
if direction:
  velocity.x = direction.x * SPEED
  velocity.z = direction.z * SPEED
else:
  velocity.x = 0.0
  velocity.z = 0.0
```
  pour incrémenter la vitesse de votre player.

```
### 4. Déplacements avancés du player
**Description:**
  - [ ] Implémentez un script pour contrôler le mouvement du personnage avec les touches du clavier (par exemple, les touches fléchées).
  - [ ] Ajoutez des collisions avec les bords de l'écran pour empêcher le personnage de sortir de la zone de jeu.


### 4. Ajout de mécanismes de jeu
**Description:** Découvrez comment ajouter des mécanismes de jeu tels que les points de score et les objets collectables.
  - [ ] Ajoutez un objet collectable à votre scène en utilisant un nœud Sprite.
  - [ ] Implémentez un mécanisme qui incrémente le score du joueur chaque fois qu'il collecte cet objet.
  - [ ] Affichez le score à l'écran pour que le joueur puisse le voir pendant le jeu.


### 5. Création d'un écran de jeu
**Description:** Apprenez à créer un écran de jeu complet avec un menu principal et un écran de fin de jeu.
  - [ ] Créez une nouvelle scène pour l'écran de menu principal et une autre pour l'écran de fin de jeu.
  - [ ] Ajoutez des boutons pour démarrer le jeu depuis le menu principal et pour rejouer depuis l'écran de fin de jeu.
  - [ ] Implémentez une transition entre les différents écrans en utilisant les signaux et les méthodes de Godot.
```

## Conclusion
> Félicitations pour avoir terminé ce workshop ! Nous espérons que vous avez apprécié cette introduction à Godot et que vous vous sentez plus à l'aise pour explorer davantage ce moteur de jeu puissant. N'hésitez pas à continuer à expérimenter et à créer vos propres jeux !


## Ressources supplémentaires
  - Documentation officielle de Godot : [Docs Godot Engine](https://docs.godotengine.org)
  - Tutoriels vidéo sur Godot : [YouTube - Godot Engine Official](https://www.youtube.com/user/godotengine)
