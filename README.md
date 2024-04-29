# Mouton-de-panurge

**Groupe : TrioDaynamos**

**Membres :**  *Mariam Ibtihel Narimane*

## Sommaire :
<ul>
<li>Introduction du comportement </li>
<li>Description synthétique du projet </li>
<li>Présentation structurée des résultats </li>
<li>Conclusion</li>
<li>Tableau de bord</li>
<li>Bibliographie</li>
</ul>
    
## Introduction à l'effet mouton : 
Imaginons que nous voulions étudier le phénomène du mouton de Panurge à l'aide d'une simulation informatique. Pour ce faire, nous allons utiliser Python pour créer une simulation où nous aurons une population de moutons qui interagissent entre eux dans un environnement donné.
Tout d'abord, nous allons créer notre population de moutons. Chaque mouton aura une position initiale dans l'environnement et une certaine influence aléatoire qui déterminera son comportement par rapport aux autres moutons. Certains moutons peuvent être des leaders, tandis que d'autres suivront ces leaders ou auront un comportement aléatoire.
Ensuite, nous allons définir l'environnement dans lequel les moutons évolueront. Cet environnement peut contenir des obstacles fixes qui représentent des éléments auxquels les moutons doivent faire attention lorsqu'ils se déplacent.
Maintenant, passons à la simulation du comportement de chaque individu. Chaque mouton devra prendre des décisions en fonction de son environnement. Il devra déterminer s'il suit un leader, s'il suit un mouvement aléatoire ou s'il évite les obstacles et les autres moutons sur son chemin. Ces décisions seront basées sur des règles préétablies qui définissent le comportement des moutons dans différentes situations.
Enfin, nous allons visualiser la simulation pour mieux comprendre le comportement global de la population de moutons. Nous allons afficher la position de chaque mouton ainsi que celle du leader s'il y en a un. Cela nous permettra d'observer comment les moutons interagissent entre eux et avec leur environnement.
En résumé, cette simulation nous permettra de modéliser dynamiquement le phénomène du mouton de Panurge et d'étudier comment les interactions individuelles entre les moutons peuvent conduire à des comportements collectifs émergents.


## Description synthétique du projet

**Problématique :** Comment les interactions individuelles entre les membres d'une population peuvent-elles conduire à des comportements collectifs de type "mouton de Panurge" ?

**Hypothèse principale** La tendance des individus à suivre aveuglément la majorité peut émerger à partir d'interactions simples entre les membres d'une population.

**Hypothèses secondaires**
<ul>
   <li>Les individus sont influencés par le comportement de leurs pairs et tendent à les imiter.</li>
   <li>La présence de leaders au sein de la population peut influencer le comportement des autres membres.</li>
   <li>Les obstacles dans l'environnement peuvent modifier les trajectoires individuelles et collectives des membres de la population.</li>
</ul>

**Objectifs**

<ul>
<li>Modéliser les interactions entre les membres d'une population à l'aide d'une simulation informatique.</li>
<li>Étudier comment les comportements individuels peuvent conduire à des comportements collectifs de type "mouton de Panurge".</li>
<li>Analyser l'impact de différents paramètres, tels que la présence de leaders et d'obstacles, sur les dynamiques de groupe.</li>
<li>Visualiser les résultats de la simulation pour mieux comprendre les phénomènes émergents au sein de la population.</li>
</ul>


**Point historique :** Lors d'un voyage avec son compagnon Pantagruel, Panurge entre en conflit avec un marchand de moutons appelé Dindenault. Pour se venger, Panurge achète un mouton au marchand et le jette à la mer. Les autres moutons, habitués à suivre leur chef de troupeau, sautent également dans la mer.

**Exemples du phénomène dans la vie quotidienne :**

1. **Suivre la foule dans des situations dangereuses :** Lors de bousculades ou d'émeutes, les individus ont tendance à paniquer et à suivre le mouvement sans réfléchir, ce qui peut aggraver la situation.
  
2. **Les chasses aux sorcières au 17ème siècle :** Durant cette période, des femmes innocentes ont été persécutées et tuées sur la base de rumeurs plutôt que de preuves tangibles, illustrant ainsi l'effet mouton à grande échelle.


**Formules mathématiques :**  Nous allons utiliser les expressions suivantes pour ajuster les mouvements des moutons dans la simulation,

  <ul>
      <li><img width="170" alt="dx" src=https://github.com/are-dynamic-2024-g3/Mouton-de-panurge-/blob/main/dx.PNG> : 
      Pour l'ajustement de la vitesse horizontale, </li>
      <li><img width="170" alt="dy" src=https://github.com/are-dynamic-2024-g3/Mouton-de-panurge-/blob/main/dy.PNG> : 
      Pour l'ajustement de la vitesse verticale, </li>
      <li><img width="200" alt="v" src=https://github.com/are-dynamic-2024-g3/Mouton-de-panurge-/blob/main/v.PNG> : 
      Pour calculer la vitesse totale. </li>
     <li><img width="500" alt="distance" src=  https://github.com/are-dynamic-2024-g3/Mouton-de-panurge-/blob/main/distance.png> : formule de la distance </li>
  </ul>

  
## Présentation structurée des résultats
  
**Simulation de l'effet mouton avec Python**

**Importation des bibliothèque :** 
```py 
import numpy as np
import matplotlib.pyplot as plt
import random 
```
Pour la modalisation du comportement du mouton de Panurge nous aurons besoin de c’est bibliothèque python afin d’utiliser certaines de ces fonctions


**Définir la classe Mouton :**
```py 
class Mouton:
    def __init__(self, x, y):
        self.x = x
        self.y = y
        self.vx = 0
        self.vy = 0
        self.influence = random.random() #valeur entre 0 et 1
```
Cette initialisation d’objet ou individu va nous permettre de crée des moutons afin dvaoir une population sur laquelle observer le comportement que nous modélisons. 
Pour cela on a un point x et y pour la position du mouton une vitesse vx et vy pour la direction du mouton et une influence qui nous sera très utile par la suite qui nous permettra de définie un leader parmi les moutons qui influencera les autres.

Dans cette même classe on définit la méthode suivante : 

```py 
 def leader (self,moutons):
        # Trouver le leader parmi les autres moutons
        leader = None
        max_influence = -1  # Initialisation avec une valeur très basse

        for mouton in moutons:
            if mouton.influence > max_influence:
                max_influence = mouton.influence
                leader = mouton
        
        return leader
```

Cette méthode nous permet de choisir parmi la population de mouton celui qui a le plus d’influence pour que les autres moutons le suive. Comme dans la vie réelle on observe que les personnes suivent celui ou celle qui paraît plus fort(e), plus confiant(e), plus sûr(e) de son choix, plus intelligent(e)… Donc finalement, on suit selon des critères, l’influence.

Pour continuer, il faut maintenant que les moutons suivent le leader et evitent les obstacles qu'ils peuvent rencontrer sur leur chemin, pour cela on implémente la méthode ```update```.        
Décorticon chaque partie pour mieux comprendre son fonctionnement.
Elle est constituée de **4 partie**.

**1ere partie :  LE LEADER**

```py 
        # 'leader_mouton' contient le mouton avec la plus grande influence
        leader_mouton = self.leader(moutons)        
                
        #on définit de façon random comment le leader va se déplacer par rapport aux moutons
        leader_mouton.vx = random.uniform(-nb,nb)
        leader_mouton.vy = random.uniform(-nb,nb)
```

On choisi un leader puis on defini sa direction de façon aléatoire.

**2eme partie : LE SUIVI**

```py 
# RÈGLE DE SUIVI DU LEADER 
        
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
        else:
            # Sinon, arrêter le mouton
            self.vx = 0
            self.vy = 0
            # et aussi le leader
            leader_mouton.vx=0
            leader_mouton.vy=0
 ```
   
On calcule la distance entre le leader et chaque mouton puis si cette distance est supérieur a 3 on continue d'avancer en modifiant les vitesse vx et vy afin d’avancer vers la direction du leader si cette condition n’est pas respecter c'est a dire que les moutons ont une distance inférieur ou égale a 3 tout le monde s'arrête.

**3eme partie :  ÉVITEMENT D’OBSTACLES**

```py 
 # Règle d'évitement des obstacles
        for obstacle in environnement.obstacles:
            dx = obstacle.x - self.x
            dy = obstacle.y - self.y
            distance_obstacle = np.sqrt(dx**2 + dy**2)
            if distance_obstacle < 5:
              self.vx -= 0.1 * dx / distance_obstacle
              self.vy -= 0.1 * dy / distance_obstacle
 ```

Pour eviter les obstacles on utilise la même logique que le suivi des mouton vers le leader mais au lieu d’additionner on soustrait cela permet au mouton de « reculer » face à l’obstacle pour l’éviter. L’évitement se fait que lorsque le mouton est a une distance de l’obstacle strictement inférieure à 5.

**4eme partie :  LE LEADER**

```py 
        # Règle d'évitement des murs pour les moutons et le leader
        x_min, x_max, y_min, y_max = environnement.murs()

        # Vérifier si la nouvelle position dépasse les limites de l'environnement
        #pour les moutons
        new_x = self.x + self.vx * dt
        new_y = self.y + self.vy * dt

        if new_x <= x_min:
            self.vx = 0  # Arrêter le mouvement horizontal vers la gauche
            new_x = x_min
        elif new_x >= x_max:
            self.vx = 0  # Arrêter le mouvement horizontal vers la droite
            new_x = x_max

        if new_y <= y_min:
            self.vy = 0  # Arrêter le mouvement vertical vers le bas
            new_y = y_min
        elif new_y >= y_max:
            self.vy = 0  # Arrêter le mouvement vertical vers le haut
            new_y = y_max

        # Mettre à jour la position
        self.x = new_x
        self.y = new_y        
       

        # Mise à jour de la position pour le leader
        new_leader_x = leader_mouton.x + leader_mouton.vx * dt
        new_leader_y = leader_mouton.y + leader_mouton.vy * dt

        if new_leader_x <= x_min:
            leader_mouton.vx = 0
            new_leader_x = x_min
        elif new_leader_x >= x_max:
            leader_mouton.vx = 0
            new_leader_x = x_max

        if new_leader_y <= y_min:
            leader_mouton.vy = 0
            new_leader_y = y_min
        elif new_leader_y >= y_max:
            leader_mouton.vy = 0
            new_leader_y = y_max

        leader_mouton.x = new_leader_x
        leader_mouton.y = new_leader_y
 ```

Dans cette parti nous utilisons une méthode de la classe environnement que nous detaillerons plus tard. On vérifie que la position de chaque membre de la population de depassent pas les limites de l'environnement, puis on met à jour la position de chaque individu de constituant la population.

Pour plus de clareter nous definissons une méthode qui va nous permettre de distinguer par les differentes couleurs le leader et les moutons :

```py 
  def draw(self, is_leader=False):
        if is_leader:
            plt.plot(self.x, self.y, 'go')  # Dessiner en vert pour le leader
        else:
            plt.plot(self.x, self.y, 'bo')  # Dessiner en bleu pour les autres moutons
```


**Définir la classe obstacle :**

```py 
class Obstacle:
    def __init__(self, x, y):
        self.x = x
        self.y = y
```

La classe obstacles est seulement constituer de l’initialisation de la position de l’obstacle par les points x et y. 


**Créer un environnement :**

```py 
class Environnement:
    def __init__(self, largeur, hauteur):
        self.largeur = largeur
        self.hauteur = hauteur
        self.obstacles = []
```

On initialise notre environnement en lui donnant une largeur et une hauteur pour lui definir des bords. 
Puis un tableau vide d'obstcales qui contiendra des obstcales definit par leur points par la suite avec une methdode  ```def ajouter_obstacles_aleatoires(self, nb_obstacles)```. 

```py 
def ajouter_obstacles_aleatoires(self, nb_obstacles):
        # Ajouter des obstacles aléatoires à l'environnement
        for _ in range(nb_obstacles):
            self.obstacles.append(Obstacle(np.random.uniform(0, self.largeur), np.random.uniform(0, self.hauteur)))
```

Cette méthode va nous permettre d'ajouter des obstacles dans notre environnement. En fonction du nombre d'obstacle que l’utilisateur entre dans les parametres, la fonction choisira des positions aléatoires dans l'environnement pour placer ces obstacles.

Pour continuer, dans cette classe nous avons une seconde méthode :

```py 
def murs(self):
        x_min = 1
        x_max = self.largeur-1
        y_min = 1
        y_max = self.hauteur-1
        return x_min, x_max, y_min, y_max
```

Nous avons utiliser precedement cette méthode pour délimiter les bords de notre monde. Ici les min sont égales à 1 car les individus de la population sont représentés par des points et si les min seraient égales à 0 on aurait l’impression que les individus ont la moitier de leur « corps » en dehors du monde. Cela évite qu’ils soient « coller » au murs avant de rebondir pour l’éviter. De même pour les max.

Et pour finir, nous avons la méthode suivante :

```py 
  def draw(self):
       for obstacle in self.obstacles:
           plt.plot(obstacle.x, obstacle.y, 'ko')  # Dessiner les obstacles en rouge
```

qui permet de mettre en rouge les obstacles. Cela va permettre de mieux les distiguer lors de la visualisation.


**Visualiser la simulation :**

Pour visualiser, il faut dabors initialiser le comportement:

```py 
# Initialisation
nb_moutons = 10
largeur_environnement = 50
hauteur_environnement = 50
nb=0.1

environnement = Environnement(largeur_environnement, hauteur_environnement)
moutons = [Mouton(np.random.uniform(0, largeur_environnement), np.random.uniform(0, hauteur_environnement)) for i in range(nb_moutons)]

# Ajout d'obstacles aléatoires à l'environnement
nb_obstacles = 7  # Nombre d'obstacles à ajouter
environnement.ajouter_obstacles_aleatoires(nb_obstacles)
```

Puis Simuler le comportement,

```py 
# Simulation
for t in range(50):
    leader = None
    for mouton in moutons:
        mouton.update(t, environnement,nb, moutons)
        if mouton == mouton.leader(moutons):
            leader = mouton
    
            leader.update(t, environnement,nb, moutons)
```

On peut maintenant passer a la visualisation:

```py 
  # Visualisation
    plt.clf() # efface la figure actuelle.
    plt.xlim([0, largeur_environnement])
    plt.ylim([0, hauteur_environnement])
    
    for mouton in moutons:
        mouton.draw(is_leader=(mouton == leader))
    for obstacle in environnement.obstacles:
        plt.plot(obstacle.x, obstacle.y, 'ro')
        
    plt.pause(0.5)

plt.show()
```

Voici une vidéo de ce que cela peut donner. Oui, **« peut donner »** car à chaque execution cela change ce n’est jamais identique.


https://github.com/are-dynamic-2024-g3/Mouton-de-panurge-/assets/160219069/920b9ac5-a3d8-4d62-af8d-067ab35ad18c


Ici, en 16 itérations sur 50 les moutons sont proches du leader, et s’arretent donc.

Mais plus la direction du leader est **aléatoire** plus les moutons n'arrivent **plus à le suivre** et donc le temps de **suivi augmente**.


https://github.com/are-dynamic-2024-g3/Mouton-de-panurge-/assets/160219069/b1fc8345-21cf-4908-ae42-b5fdf3a74a88


Apres avoir atteint les 50 itérations les mouton ne sont pas dutout proche du leader, il n’y a pas la reprsentation dune foule.

On peut l’observer sur la courbe ci-dessous :

```py 
# Initialisation
nb_moutons = 10
largeur_environnement = 50
hauteur_environnement = 50
nb_obstacles=7
limite_iterations = 50

moutons = [Mouton(np.random.uniform(0, largeur_environnement), np.random.uniform(0, hauteur_environnement)) for i in range(nb_moutons)]    

def temps_suivi(environnement, moutons, limite_iterations):
    for t in range(limite_iterations):
        leader = None
        for mouton in moutons:
            mouton.update(t, environnement, nb, moutons)
            if mouton == mouton.leader(moutons):
                leader = mouton
                leader.update(t, environnement, nb, moutons)
        
        # Vérifier si tous les moutons ont arrêté de bouger
        tous_arretes = all(mouton.vx == 0 and mouton.vy == 0 for mouton in moutons)
        if tous_arretes:
            return t + 1  # Ajouter 1 pour inclure l'itération actuelle
        
    # Si la limite maximale d'itérations est atteinte
    return limite_iterations

def simuler_temps_suivi(nb_liste):
    temps_suivi_moyen = []
    for nb in nb_liste:
        # Réinitialiser les moutons avec de nouvelles positions aléatoires
        moutons = [Mouton(np.random.uniform(0, largeur_environnement), np.random.uniform(0, hauteur_environnement)) for _ in range(nb_moutons)]
        # Exécuter la simulation et calculer le temps de suivi moyen
        temps_suivi_total = 0
        for _ in range(50):  # Exécuter la simulation 30 fois
            environnement = Environnement(largeur_environnement, hauteur_environnement)
            environnement.ajouter_obstacles_aleatoires(nb_obstacles)
            temps_suivi_total += temps_suivi(environnement, moutons, limite_iterations)
        temps_suivi_moyen.append(temps_suivi_total / 50)  # Calculer la moyenne du temps de suivi
    return temps_suivi_moyen

# Liste des directions aléatoires du leader à tester
liste_nb = [0.1,0.5,1, 5]

# Appel de la fonction pour obtenir les données à tracer
temps_suivi_moyen = simuler_temps_suivi(liste_nb)

# Tracer la courbe
plt.plot(liste_nb, temps_suivi_moyen)
plt.xlabel('Direction aléatoire du leader')
plt.ylabel('Moyenne du temps de suivi des moutons')
plt.title('Temps de suivi des moutons en fonction de la direction aléatoire du leader')
```

<img width="650" alt="1" src= https://github.com/are-dynamic-2024-g3/Mouton-de-panurge-/blob/main/1.png> 

De façon analogique, lorsqu’un groupe de personne décide de suivre une personne ayant une grande influence pour une certaine raison, et que celle ci se déplace de façon imprévisible et rapidement, le groupe d'individu ne peut bien evidement pas suivre le ‘leader’.

Mais il y a un cas où peu importe la vitesse du leader, si les moutons sont déjà proches de lui dès le départ ils reussiront à s'apporcher du leader rapidement. Ce qui paraît finalement assez logique.

Voici une courbe qui permet de constater cela :

<img width="650" alt="2" src=https://github.com/are-dynamic-2024-g3/Mouton-de-panurge-/blob/main/2.png> 

On comprend alors **2** choses :
Premièrement, que la vitesse du leader qui determine sa direction en fonction de sa valeur aleatoire cela va avoir un impacte sur les autres moutons
Deuxiement, que la position de départ des mouton par rapport au leader a un impacte sur le temps de suivi du leader.

**Remarque : à chaque execution du code permettant de réaliser la courbe, la courbe change car se ne sont jamais les mêmes simulations.**

On va maintenant observer l’impacte du nombre d'obstacle sur le temps de suivi des moutons : 

Pour cela,

On fait l’initialisation,

```py 
# Initialisation
nb_moutons = 10
largeur_environnement = 50
hauteur_environnement = 50
nb=0.1

moutons = [Mouton(np.random.uniform(0, largeur_environnement), np.random.uniform(0, hauteur_environnement)) for i in range(nb_moutons)]
```

Puis on implémente une fonction pour évaluer le temps de suivi du mouton,

```py 
def temps_suivi(environnement, moutons,nb, limite_iterations):
    for t in range(limite_iterations):
        leader = None
        for mouton in moutons:
            mouton.update(t, environnement, moutons)
            if mouton == mouton.leader(moutons):
                leader = mouton
                leader.update(t, environnement, moutons)
        
        # vérifier si tous les moutons ont arretés de bouger
        tous_arretes = all(mouton.vx == 0 and mouton.vy == 0 for mouton in moutons) #La fonction 'all' est une fonction Python qui prend une séquence en argument et                                                                                      #renvoie True si tous les éléments de cette séquence
                                                                                    #sont évalués comme True, sinon elle renvoie False.
        if tous_arretes:
            return t + 1  # Ajouter 1 pour inclure l'itération actuelle
        
    # Si la limite maximale d'it√©rations est atteinte
    return limite_iterations
```

Ensuite on « créeer » les données,

```py 
nb_obstacles = [60,50,40,30,20,10,0]  # Nombre d'obstacles √† tester

temps_suivi_moyen = []

for nb_obs in range (0,len(nb_obstacles)):
    environnement = Environnement(largeur_environnement, hauteur_environnement)
    environnement.ajouter_obstacles_aleatoires(nb_obstacles[nb_obs])
    temps_suivi_total = 0
    
    # Exécutez plusieurs fois la simulation pour obtenir une moyenne
    for _ in range(30):  # Ex√©cutez la simulation 2 fois
        temps_suivi_total += temps_suivi(environnement, moutons,50)
    
    # Calculez la moyenne du temps de suivi pour ce nombre d'obstacles
    temps_suivi_moyen.append(int(temps_suivi_total / 30)) # Divisez par le nombre de simulations (5)
    nb_obs+=1
```

Et enfin, on trace la courbe,

```py 
plt.plot(nb_obstacles, temps_suivi_moyen)
plt.xlabel('Nombre d\'obstacles')
plt.ylabel('Moyenne du temps de suivi des moutons')
plt.title('Temps de suivi des moutons en fonction du nombre d\'obstacles')
plt.ylim(0, 55)  # D√©finir les limites de l'axe y de 0 √† 100
plt.show()
```

Voici une video de la simulation utilisant ce code :

video 3.mp4

On observe ici que après avoir fait 50 itérations les moutons ne sont toujours pas regroupés vers le leader. Il semble que 50 itérations ne soient pas assez. On remarque une **« hatitude » assez anormale** des moutons ils essayent a la fois de **suivre le leader mais aussi d'éviter les nombreux obstacles**. 

Et au contraire lorqu'il n'y a pas beaucoup d'obstacles, les moutons suivent plus rapidement le leader,

video 4.mp4

Cette simulation a eu besoin de seulement 15 itérations sur 50 pour avoir un regroupement des moutons et du leader. Les moutons ne sont pas gênés par des obstacles qui peuvent contraindre leur déplacement vers le leader.

On peut observer ceci par une courbe. 
La voici,

photo3

On voit sur cette courbe qu'elle a une allure croissante mais elle n’est pas strictement croissent. Ceci s'explique par le fait que si les moutons sont déjà proches du leader, ils n’auront pas besoin de beaucoup de temps pour arriver à celui-ci. On peut l'observer sur cette autre courbe :

photo4

Avant de passer à la suite, voici un tableau avec des données que nous avons collectées. 

```py 
# Initialisation
nb_moutons = 50
largeur_environnement = 50
hauteur_environnement = 50
nb_obstacles=5 #puis avec 15

moutons = [Mouton(np.random.uniform(0, largeur_environnement), np.random.uniform(0, hauteur_environnement)) for i in range(nb_moutons)]
```

Pour cette simulation, nous avons utiliser une boucle allant jusqu'à 100 itérations.

photo7

On remarque que plus le leader a une direction aléatoire et plus il y a d'obstacles plus le nombre d’iteration représentant le temps de suivi des moutons vers le leader **augmente**. Cette observation semble être proportinelle.
	
Pour finir, même si cela semble intuitif, on va observer quelques courbes sur l’impacte de la taille de l'environnement sur le temps de suivi des moutons.

Le code reste identique seulement le nom des parametres et des variables à l'intereur de la fonction changent :

```py 
def temps_suivi(environnement, moutons, limite_iterations):
    for t in range(limite_iterations):
        leader = None
        for mouton in moutons:
            mouton.update(t, environnement, nb, moutons)
            if mouton == mouton.leader(moutons):
                leader = mouton
                leader.update(t, environnement, nb, moutons)
        
        # Vérifier si tous les moutons ont arrêté de bouger
        tous_arretes = all(mouton.vx == 0 and mouton.vy == 0 for mouton in moutons)
        if tous_arretes:
            return t + 1  # Ajouter 1 pour inclure l'itération actuelle
        
    # Si la limite maximale d'itérations est atteinte
    return limite_iterations

def simuler_temps_suivi(tailles_environnement):
    temps_suivi_moyen = []
    for taille in tailles_environnement:
        # Calculer le temps de suivi moyen pour chaque taille d'environnement
        temps_suivi_total = 0
        for _ in range(30):  # Exécuter la simulation 30 fois
            environnement = Environnement(taille, taille)
            environnement.ajouter_obstacles_aleatoires(nb_obstacles)
            moutons = [Mouton(np.random.uniform(0, taille), np.random.uniform(0, taille)) for _ in range(nb_moutons)]
            temps_suivi_total += temps_suivi(environnement, moutons, limite_iterations)
        temps_suivi_moyen.append(temps_suivi_total / 30)  # Calculer la moyenne du temps de suivi
    return temps_suivi_moyen
```

On « definit » les donnees:

```py 
# Liste des tailles d'environnement à tester
tailles_environnement = [10, 20, 30, 40, 50]

# Appel de la fonction pour obtenir les données à tracer
temps_suivi_moyen = simuler_temps_suivi(tailles_environnement)
```

Et on trace la courbe:

```py 
plt.plot(tailles_environnement, temps_suivi_moyen, color='red')
plt.xlabel('Taille de l\'environnement')
plt.ylabel('Moyenne du temps de suivi des moutons')
plt.title('Temps de suivi des moutons en fonction de la taille de l\'environnement')
plt.show()
```

Voici une première courbe :

photo5

On observe sur celle-ci que plus la taille de l'environnement est grand plus les moutons prennent du temps à arriver vers le leader, ce qui paraît normale et logique.

Mais, voici une seconde courbe qui nous permet d'avoir un temps de reflexion :

photo6

En effet, comme precedement,  cela s'explique par le fait que si les moutons sont déjà proches du leader ils n’auront pas besoin de beaucoup de temps pour arriver à celui-ci et donc, dans se cas là, la taille de l'environnemnt n'a aucun impacte sur le temps de suivi des moutons.


## Conclusion : 
En résumé, cette simulation nous offre un aperçu fascinant du comportement des individus. Elle nous aide à mieux comprendre pourquoi les personnes suivent parfois aveuglément un « leader », même dans des situations complexes.

En observant comment les moutons réagissent à un leader imprévisible et à des obstacles sur leur chemin, nous pouvons mieux saisir pourquoi les gens ont tendance à suivre le mouvement sans réfléchir. Cela nous permet de comprendre comment fonctionnent les comportements de groupe dans différentes situations sociales.

Cette simulation pourrait nous aider à mieux gérer les groupes et les situations où l'influence sociale joue un rôle important, comme dans les organisations ou les foules par exemple.

Pour améliorer cette simulation, nous pourrions envisager plusieurs pistes. Tout d'abord, nous pourrions créer une fonction pour éviter les collisions entre les moutons et entre les moutons et le leader, ce qui rendrait le comportement du groupe encore plus réaliste.

De plus, nous pourrions complexifier le code en ajoutant une méthode permettant de choisir le nombre de leaders et d'avoir des populations différentes. Cela nous permettrait d'explorer davantage les dynamiques de groupe et les interactions sociales dans des contextes variés.


## Tableau de bord :
**Semaine 1:** Durant cette première semaine, nous avons initié notre projet en créant le dossier de travail, en établissant notre site et en rédigeant le README. Nous avons également entamé nos premiers échanges au sein du groupe pour définir les grandes lignes de notre collaboration.

**Semaine 2:** Cette semaine a été marquée par une session de recherche documentaire intensive, où chaque membre s'est plongé dans l'exploration des ressources pertinentes pour notre projet. Nous avons également entamé nos recherches individuelles afin de rassembler un ensemble complet d'informations pour alimenter notre travail.

**Semaine 3:** Le point d'orgue de cette semaine fut la mise en commun de nos recherches. Nous avons consolidé nos découvertes en un ensemble cohérent, explorant notamment des pistes de code et des tutoriels pour la modélisation visuelle. En parallèle, nous avons poursuivi la rédaction du README, testé des premiers morceaux de code et échangé activement au sein du groupe pour affiner notre vision collective.

**Semaine 4:** Au cours de cette semaine, nous avons continué à enrichir le README et à affiner notre approche de modélisation. Nous avons également poursuivi nos expérimentations avec le code et entrepris des recherches plus approfondies pour identifier une bibliothèque de visualisation adaptée à nos besoins spécifiques. Nos échanges réguliers ont permis de maintenir une dynamique collaborative fructueuse au sein du groupe.

**Semaine 5 et 6 (vacances):** Nous avons consacré du temps à revoir et à ajuster notre code en fonction de nos besoins. Nous avons effectué plusieurs simulations et avons observé attentivement les résultats pour tirer des conclusions significatives. Nous avons identifié les points forts et les points faibles de notre modèle, ce qui nous a permis de proposer des améliorations et des ajustements pour le rendre plus précis et plus représentatif de la réalité. Nous avons également examiné les différents paramètres de notre simulation et leur impact sur le comportement des agents, en particulier le leader et les moutons.

**Semeine 7:** Nous avons travaillé sur la représentation visuelle de nos observations en créant des graphiques et des tableaux pour illustrer nos résultats. Ces graphiques nous ont permis de visualiser clairement les tendances et les relations entre les différents paramètres de notre modèle de simulation. En parallèle, nous avons consacré du temps à mettre à jour et à finaliser notre site GitHub, en ajoutant les dernières modifications apportées à notre code. Enfin, nous avons préparé la présentation orale de notre projet en créant des diapositives qui résument nos principales conclusions, nos observations et nos résultats. 


## Bibliographie :

[Tracé de courbes — Cours Python](https://courspython.com/introduction-courbes.html)

[Matplotlib — Visualization with Python](https://matplotlib.org/)

[matplotlib.pyplot.plot — Matplotlib 3.8.4 documentation ](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.plot.html)

[Matplotlib Scatter (w3schools.com) ](https://www.w3schools.com/python/matplotlib_scatter.asp)

[Welcome to Python.org](https://www.python.org/)

[Les moutons de Panurge : définition et origine de l’expression (lalanguefrancaise.com)](https://www.lalanguefrancaise.com/expressions/les-moutons-de-panurge-definition-origine#:~:text=L%E2%80%99expression%20%C2%AB%20mouton%20de%20Panurge%20%C2%BB%2C%20locution%20nominale%2C,la%20majorit%C3%A9%20sans%20trop%20se%20poser%20de%20questions%E2%80%A6)

[« Mouton de panurge » : Que signifie cette expression française ? (orthographiq.com) ](https://www.orthographiq.com/blog/mouton-de-panurge-que-signifie-cette-expression-francaise)



































