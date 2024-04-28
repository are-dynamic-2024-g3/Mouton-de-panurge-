```py

import numpy as np
import matplotlib.pyplot as plt
import random 

class Mouton:
    def __init__(self, x, y):
        self.x = x
        self.y = y
        self.vx = 0
        self.vy = 0
        self.influence = random.random() #valeur entre 0 et 1

    def leader (self,moutons):
        # Trouver le leader parmi les autres moutons
        leader = None
        max_influence = -1  # Initialisation avec une valeur très basse

        for mouton in moutons:
            if mouton.influence > max_influence:
                max_influence = mouton.influence
                leader = mouton
        
        return leader
    
                
    def update(self, dt, environnement, moutons):
        
        # 'leader_mouton' contient le mouton avec la plus grande influence
        leader_mouton = self.leader(moutons)        
                
       #on definit de facon random comment le leader va se déplacer par rapport aux moutons
        leader_mouton.vx = random.uniform(-0.01,0.01)
        leader_mouton.vy = random.uniform(-0.01,0.01)
       
    	# REGLE DE SUIVI DU LEADER 
        
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
      
        # Règle d'évitement des obstacles
        for obstacle in environnement.obstacles:
            dx = obstacle.x - self.x
            dy = obstacle.y - self.y
            distance_obstacle = np.sqrt(dx**2 + dy**2)
            if distance_obstacle < 5:
              self.vx -= 0.1 * dx / distance_obstacle
              self.vy -= 0.1 * dy / distance_obstacle
       
        
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
        
    def population_diff(self, nb_leaders, population_moutons):
        les_leaders=[]
        
        #on definit les différents leaders 
        for i in range(nb_leaders):
            les_leaders.append(self.leader(self,population_moutons))
            i+=1
            
        # Calculer les distances entre chaque leader et chaque mouton
        for leader in les_leaders:
            for mouton in population_moutons:
                 distance = np.sqrt((mouton.x - leader.x)**2 + (mouton.y - leader.y)**2)
                 
                 # Comparer avec la distance la plus courte et mettre à jour le leader proche si nécessaire    
    def temps_suivi_leader(self, moutons, dt, max_temps=100):
        distance_initiale = np.sqrt((self.x - self.leader(moutons).x)**2 + (self.y - self.leader(moutons).y)**2)
        temps = 0
        while distance_initiale > 1 and temps < max_temps:    
            self.update(dt, environnement, moutons)
            distance_initiale = np.sqrt((self.x - self.leader(moutons).x)**2 + (self.y - self.leader(moutons).y)**2)
            temps += 1
        return temps
  
    def draw(self, is_leader=False):
        if is_leader:
            plt.plot(self.x, self.y, 'go')  # Dessiner en vert pour le leader
        else:
            plt.plot(self.x, self.y, 'bo')  # Dessiner en bleu pour les autres moutons
            

class Obstacle:
    def __init__(self, x, y):
        self.x = x
        self.y = y

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

        
# Initialisation
nb_moutons = 50
largeur_environnement = 50
hauteur_environnement = 50
temps_suivi=[]
directions_leader= []


environnement = Environnement(largeur_environnement, hauteur_environnement)
moutons = [Mouton(np.random.uniform(0, largeur_environnement), np.random.uniform(0, hauteur_environnement)) for i in range(nb_moutons)]

# Simulation
for t in range(100):
    leader = None
    for mouton in moutons:
        mouton.update(t, environnement, moutons)
        if mouton == mouton.leader(moutons):
            leader = mouton
    
            leader.update(t, environnement, moutons)

for mouton in moutons:
    leader = mouton.leader(moutons)
    leader.vx = random.uniform(-0.01,0.01)
    leader.vy = random.uniform(-0.01,0.01)
    
    temps_suivi_moyen =mouton.temps_suivi_leader(moutons, 0.2)
    directions_leader.append(np.sqrt(leader.vx**2 + leader.vy**2))
    temps_suivi.append( temps_suivi_moyen)
    
    
    


# Tracer la courbe
plt.plot(directions_leader,temps_suivi)
plt.title("Temps de suivi des moutons en fonction de la direction aléatoire du leader")
plt.xlabel("Direction aléatoire du leader")
plt.ylabel("Temps de suivi moyen des moutons")
plt.ylim(0,100)
plt.show()
```

