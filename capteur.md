
# <center>Projet d'ISN </center>

# Présentation 

### Notre projet consiste à créer un programme qui permet de compter le nombre de personnes à l'entrée d'un lieu et de réguler le passage en comptant ceux qui sortent par rapport à ceux qui entrent.

##### Prenons l'exemple d'un self. Ce programme permet d'indiquer aux élèves s'il reste des places disponible dans le self.

<img src="image/schema_self.PNG" alt="shema self" width=50%>

# Programmation sur Jupyter Notebook

#### Ici nous allons créer deux boutons simulant l'entré et et la sortie de la personne 

Suivez ce code et vérifier son fonctionnement en cliquant sur les boutons vert "entrée" et jaune "sortie" !


```python
import ipywidgets as widgets #c'est obligatoire d'importer l'ipywidgets sinon on ne peut pas créer de boutons 
```


```python
from IPython.display import display 

button = widgets.Button(      #ici on définit la variable du bouton "entrée"
    description='entrée',
    disabled=False,           #le bouton prend à l'initial une variable 0
    button_style='success',   #les lignes suivantes définissent le style du bouton 
    tooltip='Click me', 
    icon='check'
)
display(button)

def entre(b):
    print("entré")
    
button.on_click(entre)



button = widgets.Button(      #ici on définit la variable du bouton "sortie"
    description='sortie', 
    disabled=False,           #le bouton prend à l'initial une variable 0
    button_style='warning',   #les lignes suivantes définissent le style du bouton
    tooltip='Click me',
    icon='check'
)
display(button)

def sortie(b):
    print("sortie")
    
button.on_click(sortie)

```


    Button(button_style='success', description='entrée', icon='check', style=ButtonStyle(), tooltip='Click me')



    Button(button_style='warning', description='sortie', icon='check', style=ButtonStyle(), tooltip='Click me')


#### Ici nous allons créer une interface qui va pouvoir indiquer par un symbole programmer au préalable si il reste des places dans le self ou si il est plein


```python
from ipyturtle import Turtle
```


```python
t = Turtle(fixed=False, width=800, height=120) #paramètre de l'interface
```


```python
def yes():#création d'une fontion nommée yes
    for i in range(1):#on repete une fois les ordres suivant
        t.right(135)#tourner de 135° à droite
        t.forward(50)#avancer de 50 
    for i in range(1):#on repete une fois les ordres suivant
        t.left(100)#tourner de 100° à gauche
        t.forward(90)#avancer de 90
    
```


```python
def non():#création d'une fontion nommée non
    for i in range(360):#on repete 360 fois les ordres suivant
        t.forward(1)#avancer de 1
        t.right(1)#tourner de 1° à droite
    for i in range(1):#on repete une fois les ordres suivant
        t.right(90)#tourner de 90° à droite
        t.forward(125)#avancer de 125
```


```python
t.reset()#on reprend à 0 le turtle
```


```python
t #mise en place de la turtle définie au préalable. Suivant la fonction appelée, la commande du dessin s'effectue. 
```


    Turtle()



```python
yes()#on appel la fonction yes() qui correspond à la signification qui reste des places.
```


```python
non()#on appel la fonction non() qui correspond à la signification qui ne reste pas de places.
```


```python
from IPython.display import display 

n=0

button = widgets.Button(      #ici on définit la variable du bouton "entrée"
    description='entrée',
    disabled=False,           #le bouton prend à l'initial une variable 0
    button_style='success',   #les lignes suivantes définissent le style du bouton 
    tooltip='Click me', 
    icon='check'
    
)
display(button)
    
def entre(b):
    n=1
    print("entré")
    print(n)
button.on_click(entre)



button = widgets.Button(      #ici on définit la variable du bouton "sortie"
    description='sortie', 
    disabled=False,           #le bouton prend à l'initial une variable 0
    button_style='warning',   #les lignes suivantes définissent le style du bouton
    tooltip='Click me',
    icon='check'
)
display(button)

def sortie(b):
    n=-1
    print("sortie")
    print(n)

button.on_click(sortie)


```


    Button(button_style='success', description='entrée', icon='check', style=ButtonStyle(), tooltip='Click me')



    Button(button_style='warning', description='sortie', icon='check', style=ButtonStyle(), tooltip='Click me')

codage de la carte microbit son sur MU
'
#Ecrit ton programme ici ;-)
from microbit import *
import music

while True:
    if button_a.is_pressed():
        for freq in range(880, 1760, 16):
            music.play(music.POWER_UP)
    if button_b.is_pressed():
        for freq in range(1760, 880, -16):
            music.play(music.JUMP_DOWN)
'
# Programmation BBC Micro:bit avec l'éditeur Mu

Au moyen du câble fourni, raccordez la carte BBC micro:bit sur un port USB de l'ordinateur. Le PC doit reconnaitre la carte comme un nouveau lecteur nommé : MICROBIT (E:)

Ouvrez le logiciel Mu et essayer différents codes. Puis il faut cliquer sur le bouton “Flash” qui permet en quelques secondes de téléverser votre code dans la mémoire flash du µC du BBC micro:bit en effaçant et en remplaçant le programme précédent.

## Boutons poussoirs

<img src="image/buttons.png" alt="Boutons A et B" width=40%>

### Opérateurs Booléens :
Avec les deux entrées TOR (Tout Ou Rien), le bouton A, le bouton B, qui ne peuvent prendre chacun que deux valeurs booléennes `False = 0` `True = 1` nous pouvons programmer et tester des fonctions de logique booléenne.


```python
from microbit import *

while True:
   
    if button_a.is_pressed() and button_b.is_pressed():
        display.scroll("0")    #la microbit affiche la valeur
        break
    
    elif button_a.is_pressed():
        display.scroll("-1")   #la microbit affiche la valeur
    
    elif button_b.is_pressed():
        display.scroll("+1")   #la microbit affiche la valeur
```

On peut également y ajouter une variable qui correspond au nombre de personnes ainsi qu'une image en fonction de l'instruction.


```python
from microbit import *

n = 0 #n = nombre de personnes

while True:
   
    if button_a.is_pressed() and button_b.is_pressed():
        print(n)
        break
    
    elif button_a.is_pressed():
        n=n-1  #n prend la valeur n-1
        sleep(5000)  #la microbit s'endort pendant un certain temps en ms (ici 5s) 
        print(n)
        display.scroll(str(button_a.get_presses()))#la microbit affiche le nombre de fois où le bouton "a" a été pressé en un temps donné
        display.show(Image.SAD)  #un visage triste apparaît
    
    elif button_b.is_pressed():
        n=n+1  #n prend la valeur n+1
        sleep(5000)  #la microbit s'endort pendant un certain temps en ms (ici 5s)
        print(n)
        display.scroll(str(button_b.get_presses()))#la microbit affiche le nombre de fois où le bouton "a" a été pressé en un temps donné
        display.show(Image.HAPPY) #un visage content apparaît
```

## QCM

### En vous aidant du code ci-dessus, compléter le texte avec les élèments suivantes: `sleep()`, `display.scroll()`, `str()`, `get_presses` et `button_a` : (certains peuvent être utilisés plusieurs fois)
<br>

### ♦ La fonction ... fera dormir le microbit pendant un certain nombre de millisecondes si vous voulez une pause dans votre programme.


```python
import ipywidgets as widgets
```


```python
widgets.ToggleButtons(
    options=['sleep()', 'display.scroll()', 'str()', 'get_presses', 'button_a'],
    description='Réponse:',
    disabled=False,
    tooltips=['Tu es sûr de toi ?', 'Tu es sûr de toi ?', 'Tu es sûr de toi ?', 'Tu es sûr de toi ?', 'Tu es sûr de toi ?'],

)
```


    ToggleButtons(description='Réponse:', options=('sleep()', 'display.scroll()', 'str()', 'get_presses', 'button_…


### ♦ Il existe un objet appelé ... et vous pouvez obtenir le nombre de fois où il a été pressé avec la get_presses méthode .


```python
widgets.ToggleButtons(
    options=['sleep()', 'display.scroll()', 'str()', 'get_presses', 'button_a'],
    description='Réponse:',
    disabled=False,
    tooltips=['Tu es sûr de toi ?', 'Tu es sûr de toi ?', 'Tu es sûr de toi ?', 'Tu es sûr de toi ?', 'Tu es sûr de toi ?'],

)
```


    ToggleButtons(description='Réponse:', options=('sleep()', 'display.scroll()', 'str()', 'get_presses', 'button_…


### ♦ Puisque ... donne une valeur numérique et ... n’affiche que des caractères, nous devons convertir la valeur numérique en une chaîne de caractères. Nous faisons cela avec la fonction ... (abréviation de “string” ~ elle convertit les choses en chaînes de caractères).


```python
widgets.ToggleButtons(
    options=['sleep()', 'display.scroll()', 'str()', 'get_presses', 'button_a'],
    description='Réponse:',
    disabled=False,
    tooltips=['Tu es sûr de toi ?', 'Tu es sûr de toi ?', 'Tu es sûr de toi ?', 'Tu es sûr de toi ?', 'Tu es sûr de toi ?'],

)
```


    ToggleButtons(description='Réponse:', options=('sleep()', 'display.scroll()', 'str()', 'get_presses', 'button_…



```python
widgets.ToggleButtons(
    options=['sleep()', 'display.scroll()', 'str()', 'get_presses', 'button_a'],
    description='Réponse:',
    disabled=False,
    tooltips=['Tu es sûr de toi ?', 'Tu es sûr de toi ?', 'Tu es sûr de toi ?', 'Tu es sûr de toi ?', 'Tu es sûr de toi ?'],

)
```


    ToggleButtons(description='Réponse:', options=('sleep()', 'display.scroll()', 'str()', 'get_presses', 'button_…



```python
widgets.ToggleButtons(
    options=['sleep()', 'display.scroll()', 'str()', 'get_presses', 'button_a'],
    description='Réponse:',
    disabled=False,
    tooltips=['Tu es sûr de toi ?', 'Tu es sûr de toi ?', 'Tu es sûr de toi ?', 'Tu es sûr de toi ?', 'Tu es sûr de toi ?'],

)
```


    ToggleButtons(description='Réponse:', options=('sleep()', 'display.scroll()', 'str()', 'get_presses', 'button_…


### ♦ Vous remarquerez que la fonction ... contient la fonction ... qui elle-même contient `button_a.get_presses`. Python tente d’abord de trouver la réponse la plus interne avant de passer à la couche suivante.


```python
widgets.ToggleButtons(
    options=['sleep()', 'display.scroll()', 'str()', 'get_presses', 'button_a'],
    description='Réponse:',
    disabled=False,
    tooltips=['Tu es sûr de toi ?', 'Tu es sûr de toi ?', 'Tu es sûr de toi ?', 'Tu es sûr de toi ?', 'Tu es sûr de toi ?'],

)
```


    ToggleButtons(description='Réponse:', options=('sleep()', 'display.scroll()', 'str()', 'get_presses', 'button_…



```python
widgets.ToggleButtons(
    options=['sleep()', 'display.scroll()', 'str()', 'get_presses', 'button_a'],
    description='Réponse:',
    disabled=False,
    tooltips=['Tu es sûr de toi ?', 'Tu es sûr de toi ?', 'Tu es sûr de toi ?', 'Tu es sûr de toi ?', 'Tu es sûr de toi ?'],

)
```


    ToggleButtons(description='Réponse:', options=('sleep()', 'display.scroll()', 'str()', 'get_presses', 'button_…


## Touches

<img src="image/pins.png" alt="Touches 0,1,2" width=40%>

Les trois grandes broches (pin) repérées 0, 1, 2 sont sensibles à un changement de capacité provoqué au contact d'un doigt. Mais pour plus d'efficacité le plus sûr est de raccorder un bout d'un câble à pince crocodile au `GND` et avec l'autre bout de venir toucher la broche `0`.


```python
from microbit import *

n=0 #n = nombre de personnes

while True:
    
    if pin0.is_touched(): #si on touche le pin0
        n=n-1 #n prend la valeur n-1
        print(n)
        display.show(Image.SAD)  #un visage triste apparaît
    
    if pin2.is_touched():
        n=n+1  #n prend la valeur n+1
        print(n)
        display.show(Image.HAPPY) #un visage content apparaît
```

# Programmation RaspBerry Pi avec Mu



Si vous avez suivis ce bloc note et essayer le code sur les différents support proposés, il est possible de passer sur la RaspBerry Pi 3. Cela permettra, comme avec la MicroBit, d'utiliser de réels capteur.Il est aussi possible d'utiliser plus de matériels HardWare, pour avoir une solution plus réelle.

<img src="image/rb_pi.jpg" width=40%>

<strong>Pour cela il sera utile d'avoir :</strong>
<br> 
- Une RaspBerry Pi 3 équipée de Mu</br>
<br>
- Des capteurs tor ou des boutons </br>
<br> 
- Un écran d'ordinateur</br>

Après avoir branché la carte, et lancé Mu, nous pouvons commencer le code.


```python
from tkinter import *  # on importe toute la biblio tkinter, biblio graphique
from tkMessageBox import *  # on importe toute la biblio des fenetres pop up
import time  # on importe la fonction de temps
from audiere import *  # on importe toute la biblio Pyaudiere
import RPi.GPIO as GPIO # on importe le GPIO, description ci-dessous

# On definit les capteurs sur les pins 3 et 5
capteur_IN = 3
capteurde_IN = 5

# variable du nb de personne et sa variable d'affichage
nbpers = 645
w = 'Il y a ' + str(nbpers) + ' de places prises'

#variables des couleurs
coolheure = "spring green"
g1 = "gray5"
g2 = "grey10"

while True:
    capteur = GPIO.input(capteur_IN)
    capteurde = GPIO.input(capteurde_IN)
    if capteur == 0: #capteur est activé
        nbpers=nbpers+1
        # création d'un son de 900Hz pendant 0.5sec
        son=open_device().create_tone(900).play()
        sleep(500)
        son.stop()
    if capteurde == 0: #capteurde est activé
        nbpers=nbpers-1
        son=open_device().create_tone(500).play()
        sleep(500)
        son.stop()
    if n >= 100 :
        coolheure = "red"
    if n >= 110 :
        coolheure = "red"
        # fenetre pop up d'alerte de seuil, ou il y a plus de 10% de personne en trop.
        showwarning('Attention', "Vous allez depasser le seuil maximal !")
        'ok'
    elif :
        coolheure = "spring green"


# on ouvre une fenetre graphique tkinter
fenetre = Tk()

# on crée un canvas pour l'affichage des données, un cadre gris et la valeur a l'intérieur
canvas = Canvas(fenetre, width=1280, height=720, bg="gray20")
rectde = canvas.create_rectangle(250,150,950,570, fill=coolheure)
trapun = canvas.create_polygon(200,100,250,150,250,570,200,620, fill=g1)
trapde = canvas.create_polygon(200,100,250,150,950,150,1000,100, fill=g2)
traptroa = canvas.create_polygon(1000,100,950,150,950,570,1000,620, fill=g1)
trapkat = canvas.create_polygon(200,620,250,570,950,570,1000,620, fill=g2)

# affichage du texte ainsi que la valeur de la variable
txt = canvas.create_text(600, 350, text=w, font="Arial 40 italic", fill="red")
canvas.pack()

# boucle de mise a jour de la fenetre
fenetre.mainloop() 
```

Tkinter est la bibliothèque graphique permettant l'affichage des données nécessaires pour les personnes voulant entrer et savoir la place dans le lieu.
<img src="http://apprendre-python.com/images/hello-world.png" >
On peut alors y créer un Canvas comme dans p5.js, et y faire ce qu'on veut.<img src="http://apprendre-python.com/images/tkinter-canvas.png" >

Le GPIO permet d'intéragir physiquement avec la carte et donc le programme.
<img src="image/GPIO_pins.png" width=50%>
Il est possible de le relier à une carte comme celle-ci permermettant des branchements plus simple.
<img src="image/rb_schema.png" width=50%>

# QCM Récapitulatif:

pourquoi il est important d'importer au départ ipywidegts:
-car sinon on ne peut pas activer de boutons
-car sinon ça créer des boutons partout
-car sionn ça créer plein de page de dessin turtle


```python
import ipywidgets as widgets
```


```python
widgets.Dropdown(
    options=['étant la fenetre graphique qui peut-etre appelée une seul fois','étant la fenetre graphique qui peut-etre appelée autant de fois demandé', 'étant la fenetre graphique qui permet de dessiner directement dessus'],
    value='étant la fenetre graphique qui peut-etre appelée une seul fois',
    description='t:',
    disabled=False,
)
```


    Dropdown(description='t:', options=('étant la fenetre graphique qui peut-etre appelée une seul fois', 'étant l…



```python
widgets.Dropdown(
    options=['1)ne sert a rien', '2)permet d activer la fenetre turtle' , '3)est indispensable pour la création de systemes interctif'],
    value='1)ne sert a rien',
    description='t:',
    disabled=False,
)
```


    Dropdown(description='t:', options=('1)ne sert a rien', '2)permet d activer la fenetre turtle', '3)est indispe…

