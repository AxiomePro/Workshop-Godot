# Workshop Godot
- Bienvenue dans ce workshop sur Godot ! Au cours de cette session de 2h30, nous explorerons les bases de Godot, un moteur de jeu open-source et gratuit, afin de vous familiariser avec son fonctionnement et ses fonctionnalités.


## Prérequis
- Avant de commencer ce workshop, assurez-vous d'avoir installé Godot sur votre ordinateur.
> [!NOTE]
> Vous pouvez le télécharger depuis le [site officiel de Godot](https://godotengine.org/download)

- Si vous pouvez, munisez vous d'une souris pour les manipulations 3D


## Structure du Workshop
- Ce workshop est divisé en plusieurs étapes, chacune couvrant un aspect spécifique de Godot. Chaque étape comprend une description suivie d'un exercice pratique.
> [!TIP]
> Une documentation est présente (en bas de page)

> [!NOTE]
> N'hésitez pas à poser des questions


## Étapes
> [!TIP]
> Toute l'édition de script peut se faire depuis Godot via l'interface d'édition de script
> Testez votre jeu à chaque étape en cliquant sur "Éxecuter la scène actuelle"

> [!CAUTION]
> Suivez les instructions à la lettre pour que tout fonctionne correctement
> Retirez ```pass``` d'une fonction pour l'utiliser

### 1. Introduction à Godot
- **Description:** Découvrez l'interface de Godot et créez un nouveau projet
  - Ouvrez Godot et sélectionnez "Nouveau Projet".
  - Choisissez un emplacement pour votre projet et donnez-lui un nom.
  - Explorez l'interface utilisateur de Godot, y compris les différents panneaux et menus.


### 2. Création d'une scène
- **Description:** Créez une scène, avec des éléments de base de tout jeu
  - Dans votre nouveau projet, créez une nouvelle scène en cliquant sur "Ajouter un nouvelle scène" et sélectionnez "Scène 3D" puis renomez votre **${\textsf{\color{red}Node3D}}$** en "scene".
  - Enregistrez votre scène et nommez-la "player.tscn".
> [!IMPORTANT]
> Tout ce qui sera fait par la suite sera bien evidement dans la scène "scene" (player.tcsn)


### 3. Gestion des mouvements d'un player
- **Description:** Explorez les concepts de mouvement et de physique
> [!TIP]
> Vérifier le placement de vos noeud via l'interface 3D

- #### Mise en place de l'environnement
  - Dans votre "scene", ajoutez un noeud **${\textsf{\color{red}DirectionalLight3D}}$** et inclinez la vers le bas pour eclairer le futur sol.
  - Dans votre "scene", ajoutez un noeud **${\textsf{\color{red}StaticBody3D}}$** nomé "bounds" pour créer un sol.
  - Dans votre "bounds", ajoutez un noeud **${\textsf{\color{red}MeshInstance3D}}$** nomé "mesh" et sélectionnez la forme "BoxMesh" puis agrandissez le pour faire une platforme suffisament grande.
  - Dans votre "mesh", séléctionez "Maillage" puis "Créer une collision sœur convexe simplifiée".
  - Répétez ces deux dernières étapes **4** fois pour placer 4 murs autour de votre platforme.

- #### Mise en place du player
  - Dans votre "scène", ajoutez un noeud **${\textsf{\color{red}CharacterBody3D}}$** nomé "player" pour gérer les mouvements.
  - Dans votre "player", ajoutez un noeud **${\textsf{\color{red}MeshInstance3D}}$** nomé "mesh" et sélectionnez la forme "CapsuleMesh" pour lui donner une forme.
  - Dans votre "mesh", séléctinez "Maillage" puis "Créer une collision sœur convexe simplifiée".
  - Dans votre "player", ajoutez un noeud **${\textsf{\color{red}Node3D}}$** nomé "head" pour créer une tête qui pourras tourner sur elle même. Placez-la à hauteur de tête sur votre "player".
  - Dans votre "head", ajoutez un noeud **${\textsf{\color{red}Caméra3D}}$** nomé "camera" pour ajouter une pov.

- #### Ajout d'un script pour le déplacement du player
> [!WARNING]
> Si une fonction évoquée n'existe pas, créez la avec la syntaxe ```func <nom de fonction>(<parametres>):```

> [!CAUTION]
> Si le code est déjà présent, ne l'écrivez pas en double
- - Attachez un script dans votre "player" et nommez-le comme proposé, "player.gd".
  - Dans la function **_ready()** ajoutez le code suivant pour cacher votre curseur.
    ```gdscript
    Input.set_mouse_mode(Input.MOUSE_MODE_CAPTURED)
    ```
  - Au début du script ajoutez le code suivant pour définir la vitesse de votre player.
    ```gdscript
    const SPEED = 10.0
    ```
  - Dans la function **_physics_process(delta)** ajoutez le code suivant pour récupérer votre input.
    ```gdscript
    var input_dir = Input.get_vector("ui_left", "ui_right", "ui_up", "ui_down")
    ```
  - Au début du script ajoutez le code suivant pour créer un lien avec votre "head".
    ```gdscript
    @onready var head = $head
    ```
  - Dans la function **_physics_process(delta)** ajoutez le code suivant pour transformer votre input en vecteur directionnel.
    ```gdscript
    var direction = (head.transform.basis * Vector3(input_dir.x, 0, input_dir.y)).normalized()
    ```
  - Dans la fonction **_physics_process(delta)** ajoutez le code suivant pour incrémenter la vitesse de votre player.
    ```gdscript
    if direction:
        velocity.x = direction.x * SPEED
        velocity.z = direction.z * SPEED
    else:
        velocity.x = move_toward(velocity.x, 0, SPEED)
        velocity.z = move_toward(velocity.z, 0, SPEED)
    ```


### 4. Création d'un ATH (Affichage Tête Haute)
- **Description:** Découvrez l'affichage en 2D sur un jeu 3D
> [!TIP]
> Vérifier le placement de vos noeud via l'interface 2D

- #### Mise en place de l'ATH
  - Dans votre "scene", ajoutez un noeud **${\textsf{\color{grey}CanvasLayer}}$** qui serviras de liens entre un affichage 2D et une interface en 3D.
  - Dans votre "CanvasLayer", ajoutez un noeud **${\textsf{\color{green}Control}}$** nomé "ATH" qui serviras de support pour le texte.
  - Dans votre "ATH", ajoutez un noeud **${\textsf{\color{green}Label}}$** nomé "speed" pour pouvoir afficher du texte.

- #### Ajout d'un script pour afficher un texte dynamique
> [!WARNING]
> Si une fonction évoquée n'existe pas, créez la avec la syntaxe ```func <nom de fonction>(<parametres>):```
- - Attachez un script dans votre "speed" et nommez-le comme proposé, "speed.gd".
  - Au début du script ajoutez le code suivant pour créer un lien avec votre "player".
    ```gdscript
    @onready var player = $"../../../player"
    ```
  - Dans la fonction **_process(delta)** ajoutez le code suivant pour modifier le texte à afficher en continu.
    ```gdscript
    text = "speed x:%f z:%f" % [player.velocity.x, player.velocity.z]
    ```


### 5. Rotation de la caméra du player
- **Description:** Approfondissez vos connaissances en gd script
> [!IMPORTANT]
> Cette partie s'éffectuera entierement dans le script "player.gd"

> [!WARNING]
> Si une fonction évoquée n'existe pas, créez la avec la syntaxe ```func <nom de fonction>(<parametres>):```

- - Dans la fonction **_unhandled_input(event)** ajoutez la condition suivante pour ne bouger la caméra qu'en cas de mouvement de la souris
    ```gdscript
    if event is InputEventMouseMotion:
    ```
> [!IMPORTANT]
> Le reste du code dans la fonction **_unhandled_input(event)** sera dans le **if** et donc indenté en conséquence
 
- - Au début du script ajoutez le code suivant pour définir la sensibilité de la camera.
    ```gdscript
    const SENSITIVITY = 0.001
    ```
  - Dans la fonction **_unhandled_input(event)** ajoutez le code suivant pour tourner la caméra selon l'axe X.
    ```gdscript
    head.rotate_y(-event.relative.x * SENSITIVITY)
    ```
  - Au début du script ajoutez le code suivant pour faire un liens avec la "camera".
    ```gdscript
    @onready var camera = $head/camera
    ```
  - Dans la fonction **_unhandled_input(event)** ajoutez le code suivant pour tourner la caméra selon l'axe Y.
    ```gdscript
    camera.rotate_x(-event.relative.y * SENSITIVITY)
    ```
  - Au début du script ajoutez le code suivant pour définir l'inclinaison verticale minimale et maximale de votre caméra.
    ```gdscript
    const MIN_Y = -60
    const MAX_Y = 40
    ```
  - Dans la fonction **_unhandled_input(event)** ajoutez le code suivant pour bloquer l'inclinaison de la caméra selon les valeurs définies.
    ```gdscript
    camera.rotation.x = clamp(camera.rotation.x, deg_to_rad(MIN_Y), deg_to_rad(MAX_Y))
    ```


### 6. Mise en place d'un timer
- **Description:** Découvrez le fonctionnement des signaux sur Godot
> [!TIP]
> Vérifier le placement de vos noeud via l'interface 2D

- #### Mise en place du timer
  - Dans votre "CanvasLayer", ajoutez un noeud **${\textsf{\color{grey}Timer}}$** pour créer un timer.
  - Dans votre "ATH", ajoutez un noeud **${\textsf{\color{green}Label}}$** nomé "time" pour afficher le timer.

- #### Code et affichage du timer
> [!WARNING]
> Si une fonction évoquée n'existe pas, créez la avec la syntaxe ```func <nom de fonction>(<parametres>):```

- - Attachez un script dans votre "time" et nommez-le comme proposé, "time.gd".
  - Dans votre "Timer", séléctionnez "Noeud" puis "Connecter...", choisissze "timeout()" puis trouvez et séléctionnez "time" et cliquez sur "Connecter" pour lié le signal "timeout" du timer à votre script "time.gd"
  - Au début du script ajoutez le code suivant pour créer un liens avec le "Timer".
    ```gdscript
    @onready var timer = $"../../Timer"
    ```
  - Dans la function **_ready()** ajoutez le code suivant pour démarrer timer avec la scène.
    ```gdscript
    timer.autostart = true
    ```
  - Dans la function **_ready()** ajoutez le code suivant pour afficher un premier texte avant l'affichage de la première seconde.
    ```gdscript
    text = "Temps écoulé: 0:00"
    ```
  - Au début du script ajoutez le code suivant pour définir les minutes et secondes initiales de votre timer.
    ```gdscript
    var seconds = 0.0
    var minutes = 0.0
    ```
  - Dans la function **_on_timer_timeout()** ajoutez le code suivant pour incrémenter votre timer.
    ```gdscript
    seconds += 1.0
    if seconds == 60.0:
      minutes += 1.0
      seconds = 0.0
    ```
  - Dans la function **_on_timer_timeout()** ajoutez le code suivant pour créer une variable qui serviras à afficher "1m09" au lieu de "1m9".
    ```gdscript
    var zero = ""
    ```
  - Dans la function **_on_timer_timeout()** ajoutez le code suivant pour ajouter le "0" si nécéssaire.
    ```gdscript
    if seconds < 10.0:
      zero = "0"
    ```
  - Dans la fonction **_on_timer_timeout()** ajoutez le code suivant pour afficher votre timer.
    ```gdscript
    text = "Temps écoulé: %d:%s%d" % [minutes, zero, seconds]
    ```


### 7. Amélioration du player
- **Description:** Simulez le déplacement vertical des pas

> [!IMPORTANT]
> Cette partie s'éffectuera entierement dans le script "player.gd"

> [!WARNING]
> Si une fonction évoquée n'existe pas, créez la avec la syntaxe ```func <nom de fonction>(<parametres>):```

- - Au début du script ajoutez le code suivant pour définir la fréquence de variation de hauteur.
    ```gdscript
    const FREQ = 2.0
    ```
  - Au début du script ajoutez le code suivant pour définir l'amplitude de la variation de hauteur.
    ```gdscript
    const AMP = 0.3
    ```
  - Au début du script ajoutez le code suivant pour définir une variable de temps qui va permettre de changer la hauteur au fur et à mesure.
    ```gdscript
    var time = 0.0
    ```
  - Dans la function **_physics_process(delta)** ajoutez le code suivant pour incrémenter votre "time" à chaque passage de boucle.
    ```gdscript
    time += delta * velocity.length() / 2 * float(is_on_floor())
    ```
  - Dans la function **_physics_process(delta)** ajoutez le code suivant pour définir un vecteur 3d.
    ```gdscript
    var pos = Vector3.ZERO
    ```
  - Dans la function **_physics_process(delta)** ajoutez le code suivant pour incrémenter votre position en y selon le "time", la "FREQ" et l'"AMP".
    ```gdscript
    pos.y = sin(time * FREQ) * AMP
    ```
  - Dans la function **_physics_process(delta)** ajoutez le code suivant pour incrémenter votre position en x selon le "time", la "FREQ" et l'"AMP".
    ```gdscript
    pos.x = cos(time * FREQ / 2) * AMP
    ```
  - Dans la function **_physics_process(delta)** ajoutez le code suivant pour associer votre vecteur 3d à votre "CollisionShape3D".
    ```gdscript
    camera.transform.origin = pos
    ```


## Conclusion
- Félicitations pour avoir terminé ce workshop ! Nous espérons que vous avez apprécié cette introduction à Godot et que vous vous sentez plus à l'aise pour explorer davantage ce moteur de jeu puissant. N'hésitez pas à continuer à expérimenter et à créer vos propres jeux !


> ## Ressources supplémentaires
>  - [Documentation Godot](https://docs.godotengine.org) officielle
>  - Exemples vidéos sur [YouTube - Godot Engine Official](https://www.youtube.com/@GodotEngineOfficial)
