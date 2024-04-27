# Mouton-de-panurge

**Groupe : TrioDaynamos**

**Membres :**  *Mariam Ibtihel Narimane*

**Introduction à l'effet mouton :** Nous allons simuler ce phénomène avec Python. En créant notre population et l'environnement dans lequel  les individus vont bouger et intéragire entre eux.Nous allons ensuite simuler le comportement de chaque individu ( déterminer la direction à suivre (leader ou aléatoire),se déplacer dans la direction choisi,gérer les collisions avec les obstacles et les autres moutons...),et enfin Visualiser la simulation (afficher la position des moutons et du leader).Cette simulation est une modélisation dynamique du phénomène du mouton de panurge.

<img width="580" alt="image0" src=https://github.com/are-dynamic-2024-g3/Mouton-de-panurge-/blob/main/image0.jpeg>


<img width="580" alt="i" src=https://github.com/are-dynamic-2024-g3/Mouton-de-panurge-/blob/main/i.jpg>



## Description synthétique du projet

**Problématique :**

Reproduire l'épisode du mouton de panurge.

**Hypothèse principale**

Le mouton de Panurge symbolise la pensée moutonnière et la tendance des individus à suivre aveuglément la majorité.

**Hypothèses secondaires**

La simulation permet aux utilisateurs de comprendre les différentes facettes de Panurge et de soncomportements.

**Objectifs**

<ul>
<li>-Recréer la dynamique de l'épisode.</li>
<li>-explorer les conditions favorisant la contagion.</li>
<li>-étudier l'impact de la manipulation sur le groupe.</li>

</ul>






**Point historique :** Lors d'un voyage avec son compagnon Pantagruel, Panurge entre en conflit avec un marchand de moutons appelé Dindenault. Pour se venger, Panurge achète un mouton au marchand et le jette à la mer. Les autres moutons, habitués à suivre leur chef de troupeau, sautent également dans la mer.

**Exemples du phénomène dans la vie quotidienne :**

1. **Suivre la foule dans des situations dangereuses :** Lors de bousculades ou d'émeutes, les individus ont tendance à paniquer et à suivre le mouvement sans réfléchir, ce qui peut aggraver la situation.
  
2. **Les chasses aux sorcières au 17ème siècle :** Durant cette période, des femmes innocentes ont été persécutées et tuées sur la base de rumeurs plutôt que de preuves tangibles, illustrant ainsi l'effet mouton à grande échelle.
   
## Présentation structurée des résultats
  
**Simulation de l'effet mouton avec Python**

1. **Définir la classe Mouton :** Création d'une classe pour représenter les moutons dans notre simulation,
     ```py
     
      class Mouton:
    def __init__(self, x, y):
        self.x = x
        self.y = y
        self.vx = 0
        self.vy = 0
        self.influence = random.random() #valeur entre 0 et 1
   ```
    - Modélisation de la probabilité de suivi en fonction du nombre de personnes autour.
    - Analyse de la propagation des rumeurs et de leur impact sur le comportement collectif.
    - **Formules mathématiques :**  Nous allons utiliser les expressions suivantes pour ajuster les mouvements des moutons dans la simulation,

  <ul>
      <li><img width="170" alt="dx" src=https://github.com/are-dynamic-2024-g3/Mouton-de-panurge-/blob/main/dx.PNG> : 
      Pour l'ajustement de la vitesse horizontale, </li>
      <li><img width="170" alt="dy" src=https://github.com/are-dynamic-2024-g3/Mouton-de-panurge-/blob/main/dy.PNG> : 
      Pour l'ajustement de la vitesse verticale, </li>
      <li><img width="200" alt="v" src=https://github.com/are-dynamic-2024-g3/Mouton-de-panurge-/blob/main/v.PNG> : 
      Pour calculer la vitesse totale. </li>
  </ul>


  
  ```py
  
       #Regle de suivi du leader
        
        # Définir la distance entre chaque mouton et le leader
        dx = leader_mouton.x - self.x
        dy = leader_mouton.y - self.y
        distance_leader = np.sqrt(dx**2 + dy**2)
        
        # Si la distance entre le mouton et le leader est supérieure à 10
        if distance_leader > 3:
            # Ajuster la vitesse du mouton pour suivre le leader
            #modifier vx et vy permet de définir la direction pour suivre le leader
            self.vx += 0.1 * dx/distance_leader
            self.vy += 0.1 * dy/distance_leader
   ```

Ces expressions contribuent à réguler le mouvement des moutons en fonction de la distance par rapport au leader et à maintenir une vitesse maximale cohérente.    


2. **Créer un environnement :** Mise en place d'un environnement virtuel dans lequel les moutons évolueront.

 ```py

class Environnement:
    def __init__(self, largeur, hauteur):
        self.largeur = largeur
        self.hauteur = hauteur
        self.obstacles = []
        #self.ajouter_murs()
        self.ajouter_obstacles_aleatoires()

  def ajouter_obstacles_aleatoires(self, nb_obstacles=10):
        # Ajouter des obstacles aléatoires à l'environnement
        for _ in range(nb_obstacles):
            self.obstacles.append(Obstacle(np.random.uniform(0, self.largeur), np.random.uniform(0, self.hauteur)))

    def murs(self):
        x_min = 1
        x_max = self.largeur-1
        y_min = 1
        y_max = self.hauteur-1
        return x_min, x_max, y_min, y_max
    

    def draw(self):
       for obstacle in self.obstacles:
           plt.plot(obstacle.x, obstacle.y, 'ko')  # Dessiner les obstacles en noir
```
4. **Initialiser une population de moutons :** Génération d'une population de moutons avec des comportements initiaux aléatoires.

5. **Simuler le comportement :** Développement d'un algorithme pour simuler l'interaction et le mouvement des moutons selon l'effet mouton.

   <img  width="400" alt="image1" src= https://github.com/are-dynamic-2024-g3/Mouton-de-panurge-/blob/main/Capture%20d%E2%80%99%C3%A9cran%20du%202024-03-14%2021-28-14.png>
   
6. **Visualiser la simulation :** Création de graphiques ou d'animations pour représenter visuellement le comportement des moutons dans l'environnement simulé.

**Conclusion :** Cette modélisation offre une simulation intrigante du comportement du mouton de Panurge dans un environnement dynamique parsemé d'obstacles, nous permettant de mieux comprendre les mécanismes sous-jacents de l'effet mouton et ses implications dans divers contextes sociaux.

<img  width="280" alt="image1" src=https://github.com/are-dynamic-2024-g3/Mouton-de-panurge-/blob/main/image1.jpeg>







































