import pyxel

# Initialisation : largeur=160, hauteur=120, titre="Ma Fenetre"
pyxel.init(128, 128, title="nuit du code")

vaisseau_x = 60
vaisseau_y = 60

tirs_liste = []

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

def tirs_creation(x, y, tirs_liste):
    """création d'un tir avec la barre d'espace"""

    # btnr pour eviter les tirs multiples
    if pyxel.btnr(pyxel.KEY_SPACE):
        tirs_liste.append([x+4, y-4])
    return tirs_liste

def tirs_deplacement(tirs_liste):
    """déplacement des tirs vers le haut et suppression s'ils sortent du cadre"""

    for tir in tirs_liste:
        tir[1] -= 1
        if  tir[1]<-8:
            tirs_liste.remove(tir)
    return tirs_liste

def update():
    global vaisseau_x,vaisseau_y, tirs_liste	
    
    vaisseau_x, vaisseau_y = vaisseau_deplacement(vaisseau_x, vaisseau_y)
    
    tirs_liste = tirs_creation(vaisseau_x, vaisseau_y, tirs_liste)
    
    tirs_liste = tirs_deplacement(tirs_liste)

def draw():
    # Effacer l'écran avec la couleur 0 (noir)
    pyxel.cls(0)
    
    pyxel.rect(vaisseau_x , vaisseau_y , 8 , 8, 1)
        # tirs
    for tir in tirs_liste:
        pyxel.rect(tir[0], tir[1], 1, 4, 10)

# Lancement du jeu
pyxel.run(update, draw)
