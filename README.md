# nuit-du-code
import pyxel

class Jeu:
    def __init__(self):
        # Initialise la fenêtre : 160x120 pixels, titre "Fenêtre Pyxel"
        pyxel.init(160, 120, title="Fenêtre Pyxel")
        # Lance le jeu
        pyxel.run(self.update, self.draw)

    def update(self):
        # Quitte si on appuie sur Echap
        if pyxel.btnp(pyxel.KEY_Q):
            pyxel.quit()

    def draw(self):
        # Efface l'écran avec la couleur 0 (noir)
        pyxel.cls(0)
        # Dessine un rectangle (x, y, w, h, col)
        pyxel.rect(10, 10, 20, 20, 11)

# Démarre l'application
Jeu()




