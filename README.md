# Workshop Godot

- Bienvenue dans ce workshop sur Godot ! Au cours de cette session de 2h30, nous explorerons les bases de Godot, un moteur de jeu open-source et gratuit, afin de vous familiariser avec son fonctionnement et ses fonctionnalités.


## Prérequis
- Avant de commencer ce workshop, assurez-vous d'avoir installé Godot sur votre ordinateur.
> [!NOTE]
> Vous pouvez le télécharger depuis le [site officiel de Godot](https://godotengine.org/download)


## Structure du Workshop
- Ce workshop est divisé en plusieurs étapes, chacune couvrant un aspect spécifique de Godot. Chaque étape comprend une description suivie d'un exercice pratique.
> [!TIP]
> Une documentation est présente (en bas de page)

> [!NOTE]
> N'hésitez pas à poser des questions


## Étapes
> [!CAUTION]
> Suivez bien les instruction à la lettre pour que tout fonctionne correctement

> [!TIP]
> Testez votre jeu à chaque étape en cliquant sur "Éxecuter la scène actuelle"
### 1. Introduction à Godot
- **Description:** Dans cette étape, nous découvrirons l'interface de Godot et apprendrons à créer un nouveau projet
  - Ouvrez Godot et sélectionnez "Nouveau Projet".
  - Choisissez un emplacement pour votre projet et donnez-lui un nom.
  - Explorez l'interface utilisateur de Godot, y compris les différents panneaux et menus.


### 2. Création d'une scène
- **Description:** Apprenez à créer des scènes, les éléments de base de tout jeu dans Godot
  - Dans votre nouveau projet, créez une nouvelle scène en cliquant sur "Ajouter un nouvelle scène" et sélectionnez "Scène 3D" puis renomez votre "Node3D" en "scène".
  - Enregistrez votre scène et nommez-la "player.tscn".
> [!IMPORTANT]
> Tout ce qui sera fait par la suite sera bien evidement dans la scène "player.tcsn"


### 3. Gestion des mouvements d'un player
- **Description:** Explorez les concepts de mouvement et de physique dans Godot.
> [!TIP]
> Vérifier le placement de vos noeud via l'interface 3D

- #### Mise en place de l'environnement
  - Ajoutez un noeud "StaticBody3D" nomé "floor" pour créer un sol.
  - Dans votre "floor", ajoutez un noeud "MeshInstance3D" nomé "mesh" et sélectionnez la forme "BoxMesh" puis agrandissez le pour faire une platforme suffisament grande.
  - Dans votre "mesh", séléctionez "Maillage" puis "Créer une collision sœur convexe simplifiée".

- #### Mise en place du player
  - Dans votre "scène", ajoutez un noeud "CharacterBody3D" nomé "player" pour gérer les mouvements.
  - Dans votre "player", ajoutez un noeud "MeshInstance3D" nomé "mesh" et sélectionnez la forme "CapsuleMesh" pour lui donner une forme.
  - Dans votre "mesh", séléctinez "Maillage" puis "Créer une collision sœur convexe simplifiée".
  - Dans votre "player", ajoutez un noeud "Node3D" nomé "head" pour créer une tête qui pourras tourner sur elle même. Placez-la à hauteur de tête sur votre "player".
  - Dans votre "head", ajoutez un noeud "Caméra3D" nomé "camera" pour ajouter une pov.

- #### Ajout d'un script pour le déplacement du player
> [!WARNING]
> Si une fonction évoquée n'existe pas, créez la avec la syntaxe ```func <nom de fonction>(<parametres>):```
- - Attachez un script dans votre "player" et nommez-le comme proposé, "player.gd".
  - Dans la function "_ready()" ajoutez le code suivant pour cacher votre curseur.
    ```
    Input.set_mouse_mode(Input.MOUSE_MODE_CAPTURED)
    ```
  - Au début du script ajoutez le code suivant pour définir la vitesse de votre player.
    ```
    const SPEED = 10.0
    ```
  - Dans la function "_physics_process(delta)" ajoutez le code suivant pour récupérer votre input.
    ```
    var input_dir = Input.get_vector("ui_left", "ui_right", "ui_up", "ui_down")
    ```
  - Au début du script ajoutez le code suivant pour créer un lien avec votre "head".
    ```
    @onready var head = $head
    ```
  - Dans la function "_physics_process(delta)" ajoutez le code suivant pour transformer votre input en vecteur directionnel.
    ```
    var direction = (head.transform.basis * Vector3(input_dir.x, 0, input_dir.y)).normalized()
    ```
  - Dans la fonction "_physics_process(delta)" ajoutez le code suivant pour incrémenter la vitesse de votre player.
    ```
    if direction:
      velocity.x = direction.x * SPEED
      velocity.z = direction.z * SPEED
    else:
      velocity.x = 0.0
      velocity.z = 0.0
    ```


### 4. Création d'un ATH (Affichage Tête Haute)
- **Description:** Explorez les concepts d'affichage en 2D sur un jeu 3D
> [!TIP]
> Vérifier le placement de vos noeud via l'interface 2D

- #### Mise en place de l'ATH
  - Dans votre "scène", ajoutez un noeud "CanvasLayer" qui serviras de liens entre un affichage 2D et une interface en 3D.
  - Dans votre "CanvasLayer", ajoutez un noeud "Control" nomé "ATH" qui serviras de support pour le text.
  - Dans votre "ATH", ajoutez un noeud "Label" nomé "speed" pour pouvoir afficher du text.

- #### Ajout d'un script pour afficher le text dynamique
> [!WARNING]
> Si une fonction évoquée n'existe pas, créez la avec la syntaxe ```func <nom de fonction>(<parametres>):```
- - Attachez un script dans votre "speed" et nommez-le comme proposé, "speed.gd".
  - Au début du script ajoutez le code suivant pour créer un lien avec votre "player".
    ```
    @onready var player = $"../../../player"
    ```
  - Dans la fonction "_process(delta)" ajoutez le code suivant pour modofier le text à afficher en continu.
    ```
    text = "speed x:%f y:%f" % [player.velocity.x, player.velocity.y]
    ```


### 4. Rotation de la caméra du player
- **Description:** Approfondissez vos connaissances en gd script
> [!IMPORTANT]
> Cette partie s'éffectuera entierement dans le script "player.gd"

> [!WARNING]
> Si une fonction évoquée n'existe pas, créez la avec la syntaxe ```func <nom de fonction>(<parametres>):```

- - Dans la fonction "_unhandled_input(event)" ajoutez la condition suivante pour ne bouger la caméra qu'en cas de mouvement de la souris
    ```
    if event is InputEventMouseMotion:
    ```
> [!IMPORTANT]
> Le reste du code dans la fonction "_unhandled_input(event)" sera dans le **if** et donc indenté en conséquence
 
- - Au début du script ajoutez le code suivant pour définir la sensibilité de la camera.
    ```
    const SENSITIVITY = 0.001
    ```
  - Dans la fonction "_unhandled_input(event)" ajoutez le code suivant pour tourner la caméra selon l'axe X.
    ```
    head.rotate_y(-event.relative.x * SENSITIVITY)
    ```
  - Au début du script ajoutez le code suivant pour créer un lien avec votre "camera".
    ```
    @onready var camera = $head/camera
    ```
  - Dans la fonction "_unhandled_input(event)" ajoutez le code suivant pour tourner la caméra selon l'axe Y.
    ```
    camera.rotate_x(-event.relative.y * SENSITIVITY)
    ```
  - Au début du script ajoutez le code suivant pour définir l'inclinaison verticale minimale et maximale de votre caméra.
    ```
    const MIN_Y = -60
    const MAX_Y = 40
    ```
  - Dans la fonction "_unhandled_input(event)" ajoutez le code suivant pour bloquer l'inclinaison de la caméra selon les valeurs définies.
    ```
    camera.rotation.x = clamp(camera.rotation.x, deg_to_rad(MIN_Y), deg_to_rad(MAX_Y))
    ```

## Conclusion
- Félicitations pour avoir terminé ce workshop ! Nous espérons que vous avez apprécié cette introduction à Godot et que vous vous sentez plus à l'aise pour explorer davantage ce moteur de jeu puissant. N'hésitez pas à continuer à expérimenter et à créer vos propres jeux !


> ## Ressources supplémentaires
>  - Documentation officielle de Godot : [Docs Godot Engine](https://docs.godotengine.org)
>  - Tutoriels vidéo sur Godot : [YouTube - Godot Engine Official](https://www.youtube.com/user/godotengine)
