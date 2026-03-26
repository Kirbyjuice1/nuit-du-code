import pyxel, random

pyxel.init(128, 128, title="Nuit du c0de")

vaisseau_x = 60
vaisseau_y = 60

tirs_liste = []

ennemis_liste = []

vies = 4

def vaisseau_deplacement(x, y):

    if pyxel.btn(pyxel.KEY_RIGHT):
        if (x < 120) :
            x = x + 1
    if pyxel.btn(pyxel.KEY_LEFT):
        if (x > 0) :
            x = x - 1
    if pyxel.btn(pyxel.KEY_DOWN):
        if (y < 120) :
            y = y + 1
    if pyxel.btn(pyxel.KEY_UP):
        if (y > 0) :
            y = y - 1
    return x, y

def vaisseau_suppression(vies):
    """disparition du vaisseau et d'un ennemi si contact"""

    for ennemi in ennemis_liste:
        if ennemi[0] <= vaisseau_x+8 and ennemi[1] <= vaisseau_y+8 and ennemi[0]+8 >= vaisseau_x and ennemi[1]+8 >= vaisseau_y:
            ennemis_liste.remove(ennemi)
            vies = 0
    return vies

def tirs_creation(x, y, tirs_liste):

    if pyxel.btnr(pyxel.KEY_SPACE):
        tirs_liste.append([x+4, y-4])
    return tirs_liste


def tirs_deplacement(tirs_liste):

    for tir in tirs_liste:
        tir[1] -= 1
        if  tir[1]<-8:
            tirs_liste.remove(tir)
    return tirs_liste


def ennemis_creation(ennemis_liste):

    if (pyxel.frame_count % 30 == 0):
        ennemis_liste.append([random.randint(0, 120), 0])
    return ennemis_liste


def ennemis_deplacement(ennemis_liste):

    for ennemi in ennemis_liste:
        ennemi[1] += 1
        if  ennemi[1]>128:
            ennemis_liste.remove(ennemi)
    return ennemis_liste

def ennemis_suppression():
    """disparition d'un ennemi et d'un tir si contact"""

    for ennemi in ennemis_liste:
        for tir in tirs_liste:
            if ennemi[0] <= tir[0]+1 and ennemi[0]+8 >= tir[0] and ennemi[1]+8 >= tir[1]:
                ennemis_liste.remove(ennemi)
                tirs_liste.remove(tir)

def update():

    global vaisseau_x, vaisseau_y, tirs_liste, ennemis_liste, vies

    vaisseau_x, vaisseau_y = vaisseau_deplacement(vaisseau_x, vaisseau_y)

    tirs_liste = tirs_creation(vaisseau_x, vaisseau_y, tirs_liste)


    tirs_liste = tirs_deplacement(tirs_liste)

    ennemis_liste = ennemis_creation(ennemis_liste)

    ennemis_liste = ennemis_deplacement(ennemis_liste)
    
    # suppression des ennemis et tirs si contact
    ennemis_suppression()

    # suppression du vaisseau et ennemi si contact
    vies = vaisseau_suppression(vies)
    # Effacer l'écran avec la couleur 0 (noir)


def draw():

    pyxel.cls(0)

    if vies > 0:
        pyxel.rect(vaisseau_x, vaisseau_y, 8, 8, 1)

        for tir in tirs_liste:
            pyxel.rect(tir[0], tir[1], 1, 4, 10)

        for ennemi in ennemis_liste:
            pyxel.rect(ennemi[0], ennemi[1], 8, 8, 8)        
    else:
        pyxel.text(50,64, 'GAME OVER', 7)

pyxel.run(update, draw)
