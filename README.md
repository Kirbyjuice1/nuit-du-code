import pyxel

# Initialisation : largeur=160, hauteur=120, titre="Ma Fenetre"
pyxel.init(128, 128, title="nuit du code")

vaisseau_x = 60
vaisseau_y = 60



def vaisseau_deplacement(x,y) :
    if pyxel.btn(pyxel.KEY_RIGHT):
        if (x < 120) :
            x = x + 1
    if pyxel.btn(pyxel.KEY_LEFT):
        if (x > 0) :
            x = x - 1
    if pyxel.btn(pyxel.KEY_UP):
        if (y > 0) :
            y = y - 1
    if pyxel.btn(pyxel.KEY_DOWN):
        if (y < 120) :
            y = y + 1
    return x,y

def update():
    global vaisseau_x,vaisseau_y
    vaisseau_x, vaisseau_y = vaisseau_deplacement(vaisseau_x, vaisseau_y)
    

def draw():
    # Effacer l'écran avec la couleur 0 (noir)
    pyxel.cls(0)
    
    pyxel.rect(vaisseau_x , vaisseau_y , 8 , 8, 1)

# Lancement du jeu
pyxel.run(update, draw)
