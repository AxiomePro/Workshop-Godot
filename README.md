# Workshop sur Godot

Bienvenue dans ce workshop sur Godot ! Au cours de cette session de 2h30, nous explorerons les bases de Godot, un moteur de jeu open-source et gratuit, afin de vous familiariser avec son fonctionnement et ses fonctionnalités.

## Prérequis
Avant de commencer ce workshop, assurez-vous d'avoir installé Godot sur votre ordinateur. Vous pouvez le télécharger depuis [le site officiel de Godot](https://godotengine.org/download).

### Structure du Workshop
Ce workshop est divisé en plusieurs étapes, chacune couvrant un aspect spécifique de Godot. Chaque étape comprend une brève description suivie d'un exercice pratique. N'hésitez pas à poser des questions tout au long du workshop.

### Étapes

#### 1. Introduction à Godot
- **Description:** Dans cette étape, nous découvrirons l'interface de Godot et apprendrons à créer un nouveau projet.
  - Ouvrez Godot et sélectionnez "Nouveau Projet".
  - Choisissez un emplacement pour votre projet et donnez-lui un nom.
  - Explorez l'interface utilisateur de Godot, y compris les différents panneaux et menus.

#### 2. Création de scènes
- **Description:** Apprenez à créer des scènes, les éléments de base de tout jeu dans Godot.
  - Dans votre nouveau projet, créez une nouvelle scène en cliquant sur "Nouvelle Scène".
  - Ajoutez un nœud Sprite à votre scène pour représenter un personnage ou un objet.
  - Enregistrez votre scène et nommez-la "Player.tscn".

#### 3. Gestion des mouvements
- **Description:** Explorez les concepts de mouvement et de physique dans Godot.
  - Dans votre scène "Player.tscn", ajoutez un nœud "KinematicBody2D" pour gérer les mouvements.
  - Implémentez un script pour contrôler le mouvement du personnage avec les touches du clavier (par exemple, les touches fléchées).
  - Ajoutez des collisions avec les bords de l'écran pour empêcher le personnage de sortir de la zone de jeu.

#### 4. Ajout de mécanismes de jeu
- **Description:** Découvrez comment ajouter des mécanismes de jeu tels que les points de score et les objets collectables.
  - Ajoutez un objet collectable à votre scène en utilisant un nœud Sprite.
  - Implémentez un mécanisme qui incrémente le score du joueur chaque fois qu'il collecte cet objet.
  - Affichez le score à l'écran pour que le joueur puisse le voir pendant le jeu.

#### 5. Création d'un écran de jeu
- **Description:** Apprenez à créer un écran de jeu complet avec un menu principal et un écran de fin de jeu.
  - Créez une nouvelle scène pour l'écran de menu principal et une autre pour l'écran de fin de jeu.
  - Ajoutez des boutons pour démarrer le jeu depuis le menu principal et pour rejouer depuis l'écran de fin de jeu.
  - Implémentez une transition entre les différents écrans en utilisant les signaux et les méthodes de Godot.

### Conclusion
Félicitations pour avoir terminé ce workshop ! Nous espérons que vous avez apprécié cette introduction à Godot et que vous vous sentez plus à l'aise pour explorer davantage ce moteur de jeu puissant. N'hésitez pas à continuer à expérimenter et à créer vos propres jeux !

### Ressources supplémentaires
- Documentation officielle de Godot : [docs.godotengine.org](https://docs.godotengine.org)
- Tutoriels vidéo sur Godot : [YouTube - Godot Engine Official](https://www.youtube.com/user/godotengine)
