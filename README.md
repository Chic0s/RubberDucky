<h2>Matériel(s) nécessaire(s) :</h2>
<ul>
    <li>un PC</li>
    <li>un éditeur de texte (Notepad++, Visual Studio Code, Sublim Text, ... )</li>
    <li>Winrar</li>
    <li>Un raspberry Pi Pico (Env. 4€ : https://www.kubii.fr/cartes-raspberry-pi/3205-raspberry-pi-pico-0728886755172.html)</li>
    <li>Un câble universel pour connecter le PC et le raspberry</li>
</ul>

<h2>Tutoriel​</h2>

<h3>Téléchargement des fichiers nécessaires</h3>
<ul>
    <li>Circuit Python : https://circuitpython.org/board/raspberry_pi_pico/</li>
    <li>AdaFruit hid: https://github.com/adafruit/Adafruit_CircuitPython_Bundle/releases/tag/20211214</li>
    <li>Payload : https://github.com/hak5darren/USB-Rubber-Ducky/wiki/Payloads</li>
    <li>Version du Clavier (FR,US, ...) : https://github.com/Neradoc/Circuitpython_Keyboard_Layouts/releases/tag/20211001</li>
</ul>

<h2>1ère Etape​</h2>

![Etape 1](https://user-images.githubusercontent.com/96829109/188451385-2facd508-9e7d-45c5-a179-5f69637ab1c1.jpg)

<p>
Vous devez télécharger la dernière version de CircuitPython X.X.X (Actuellement 7.0.0) en .UF2.
Puis brancher le Raspberry Pico à votre ordinateur.
</p>

![Etape 2](https://user-images.githubusercontent.com/96829109/188451586-86588756-6698-4cde-8b08-507e2210cbfb.jpg)

<p>
Le Raspberry Pico apparait sous le nom "RPI-RP2". Ensuite, vous devez déplacer le fichier .UF2 dans la racine du Raspberry Pico.
Le Raspberry va disparaître quelques secondes pour ré-apparaître sous le nom "CIRCUITPY".
</p>

![Etape 3](https://user-images.githubusercontent.com/96829109/188451845-d032b51d-cace-4d86-8530-6de39217644b.jpg)

<p>Nous allons passer à l'étape 2, la configuration du raspberry. </p>

<h2>2 ème Etape</h2>
 
<p>Nous irons sur le deuxième lien "AdaFruit" pour télécharger la librairies.</p>

![Etape 4](https://user-images.githubusercontent.com/96829109/188452632-39d90f9b-4518-4ae4-a206-f92546630168.jpg)

<p>
En bas de la page, nous allons pouvoir télécharger les librairies. Le fichier qui nous intéresse est "adafruit-circuitpython-bundle-7.x-mpy-20211214.zip".
Nous allons extraire les dossiers de l'archive Winrar.
Puis cliquez sur le dossier "adafruit-circuitpython-bundle-7.x-mpy-20211214" ensuite "lib".
</p>

![Etape 5](https://user-images.githubusercontent.com/96829109/188452794-2b40362d-ad1a-481e-ab8b-444c6c2d23ac.jpg)

<p>
Recherchez le fichier "adafruit_hid" puis le copier et le coller dans le dossier "lib" du Raspberry Pico.
</p>

<h2> 3ème Etape</h2>

<p>Nous allons passer au code, dans votre Raspberry Pico vous pouvez retrouver un fichier en .py.</p>

![Etape 6](https://user-images.githubusercontent.com/96829109/188452962-5eb510a7-e289-4924-9de1-07dff826f518.jpg)

<p> Nous allons le modifier afin d'utiliser les librairies. <p>

```python



# License : GPLv2.0
# copyright (c) 2021  Dave Bailey
# Author: Dave Bailey (dbisu, @daveisu)

import usb_hid
from adafruit_hid.keyboard import Keyboard

# comment out these lines for non_US keyboards
from adafruit_hid.keyboard_layout_us import KeyboardLayoutUS as KeyboardLayout
from adafruit_hid.keycode import Keycode

# uncomment these lines for non_US keyboards
# replace LANG with appropriate language
#from keyboard_layout_win_LANG import KeyboardLayout
#from keycode_win_LANG import Keycode

import time
import digitalio
from board import *
led = digitalio.DigitalInOut(LED)
led.direction = digitalio.Direction.OUTPUT

duckyCommands = {
    'WINDOWS': Keycode.WINDOWS, 'GUI': Keycode.GUI,
    'APP': Keycode.APPLICATION, 'MENU': Keycode.APPLICATION, 'SHIFT': Keycode.SHIFT,
    'ALT': Keycode.ALT, 'CONTROL': Keycode.CONTROL, 'CTRL': Keycode.CONTROL,
    'DOWNARROW': Keycode.DOWN_ARROW, 'DOWN': Keycode.DOWN_ARROW, 'LEFTARROW': Keycode.LEFT_ARROW,
    'LEFT': Keycode.LEFT_ARROW, 'RIGHTARROW': Keycode.RIGHT_ARROW, 'RIGHT': Keycode.RIGHT_ARROW,
    'UPARROW': Keycode.UP_ARROW, 'UP': Keycode.UP_ARROW, 'BREAK': Keycode.PAUSE,
    'PAUSE': Keycode.PAUSE, 'CAPSLOCK': Keycode.CAPS_LOCK, 'DELETE': Keycode.DELETE,
    'END': Keycode.END, 'ESC': Keycode.ESCAPE, 'ESCAPE': Keycode.ESCAPE, 'HOME': Keycode.HOME,
    'INSERT': Keycode.INSERT, 'NUMLOCK': Keycode.KEYPAD_NUMLOCK, 'PAGEUP': Keycode.PAGE_UP,
    'PAGEDOWN': Keycode.PAGE_DOWN, 'PRINTSCREEN': Keycode.PRINT_SCREEN, 'ENTER': Keycode.ENTER,
    'SCROLLLOCK': Keycode.SCROLL_LOCK, 'SPACE': Keycode.SPACE, 'TAB': Keycode.TAB,
    'BACKSPACE': Keycode.BACKSPACE, 'DELETE': Keycode.DELETE,
    'A': Keycode.A, 'B': Keycode.B, 'C': Keycode.C, 'D': Keycode.D, 'E': Keycode.E,
    'F': Keycode.F, 'G': Keycode.G, 'H': Keycode.H, 'I': Keycode.I, 'J': Keycode.J,
    'K': Keycode.K, 'L': Keycode.L, 'M': Keycode.M, 'N': Keycode.N, 'O': Keycode.O,
    'P': Keycode.P, 'Q': Keycode.Q, 'R': Keycode.R, 'S': Keycode.S, 'T': Keycode.T,
    'U': Keycode.U, 'V': Keycode.V, 'W': Keycode.W, 'X': Keycode.X, 'Y': Keycode.Y,
    'Z': Keycode.Z, 'F1': Keycode.F1, 'F2': Keycode.F2, 'F3': Keycode.F3,
    'F4': Keycode.F4, 'F5': Keycode.F5, 'F6': Keycode.F6, 'F7': Keycode.F7,
    'F8': Keycode.F8, 'F9': Keycode.F9, 'F10': Keycode.F10, 'F11': Keycode.F11,
    'F12': Keycode.F12,

}
def convertLine(line):
    newline = []
    # print(line)
    # loop on each key - the filter removes empty values
    for key in filter(None, line.split(" ")):
        key = key.upper()
        # find the keycode for the command in the list
        command_keycode = duckyCommands.get(key, None)
        if command_keycode is not None:
            # if it exists in the list, use it
            newline.append(command_keycode)
        elif hasattr(Keycode, key):
            # if it's in the Keycode module, use it (allows any valid keycode)
            newline.append(getattr(Keycode, key))
        else:
            # if it's not a known key name, show the error for diagnosis
            print(f"Unknown key: <{key}>")
    # print(newline)
    return newline

def runScriptLine(line):
    for k in line:
        kbd.press(k)
    kbd.release_all()

def sendString(line):
    layout.write(line)

def parseLine(line):
    global defaultDelay
    if(line[0:3] == "REM"):
        # ignore ducky script comments
        pass
    elif(line[0:5] == "DELAY"):
        time.sleep(float(line[6:])/1000)
    elif(line[0:6] == "STRING"):
        sendString(line[7:])
    elif(line[0:5] == "PRINT"):
        print("[SCRIPT]: " + line[6:])
    elif(line[0:6] == "IMPORT"):
        runScript(line[7:])
    elif(line[0:13] == "DEFAULT_DELAY"):
        defaultDelay = int(line[14:]) * 10
    elif(line[0:12] == "DEFAULTDELAY"):
        defaultDelay = int(line[13:]) * 10
    elif(line[0:3] == "LED"):
        if(led.value == True):
            led.value = False
        else:
            led.value = True
    else:
        newScriptLine = convertLine(line)
        runScriptLine(newScriptLine)

kbd = Keyboard(usb_hid.devices)
layout = KeyboardLayout(kbd)

# sleep at the start to allow the device to be recognized by the host computer
time.sleep(.5)

# check GP0 for setup mode
# see setup mode for instructions
progStatus = False
progStatusPin = digitalio.DigitalInOut(GP0)
progStatusPin.switch_to_input(pull=digitalio.Pull.UP)
progStatus = not progStatusPin.value
defaultDelay = 0

def runScript(file):
    global defaultDelay

    duckyScriptPath = file
    f = open(duckyScriptPath,"r",encoding='utf-8')
    previousLine = ""
    duckyScript = f.readlines()
    for line in duckyScript:
        line = line.rstrip()
        if(line[0:6] == "REPEAT"):
            for i in range(int(line[7:])):
                #repeat the last command
                parseLine(previousLine)
                time.sleep(float(defaultDelay)/1000)
        else:
            parseLine(line)
            previousLine = line
        time.sleep(float(defaultDelay)/1000)

if(progStatus == False):
    # not in setup mode, inject the payload
    print("Running payload.dd")
    runScript("payload.dd")

    print("Done")
else:
    print("Update your payload")

```

<p>Il suffit de copier le code et de l'insérer à la place de l'ancien à l'aide d'un éditeur de texte.</p>

<h2>4 ème Etape</h2>

<p>Nous allons mettre le clavier virtuel en Français, pour cela rendez-vous sur le lien Github du "KeyboardLayout".</p>


![Etape 7](https://user-images.githubusercontent.com/96829109/188453711-41a76141-b9b0-45bb-a128-d020af0b2536.jpg)

<p>

Nous allons télécharger le fichier "circuitpython-keyboard-layouts-7.x-mpy-20211001.zip". Dans un second temps, nous allons l'extraire et récupérer les 3 fichiers ci-dessous.

</p>

![Etape 8](https://user-images.githubusercontent.com/96829109/188453784-012742da-30b2-41fe-b01a-e6fe00e687a4.jpg)

<p> 
Copier et coller les trois fichiers dans le dossier lib.

Pour finir nous allons devoir nous rendre dans le code, et changer les lignes 9 et 10 par : </p>

```python
from keyboard_layout_win_fr import KeyboardLayout
from keycode_win_fr import Keycode
```

<h2> 5 ème Etape </h2>

<p> Pour finir, il vous vaudra créer un fichier "Payload.dd" (exemple ci-dessous) et de vous rendre sur le lien Payload.</p>

![Payload](https://user-images.githubusercontent.com/96829109/188454240-226acf7b-bf67-4137-a82b-86a54ddfa65e.jpg)

<p>Il vous suffira de copier-coller un payload qui vous convient ou de créer le votre !

Exemple de Payload :</p>

```
DELAY 3000
GUI r
DELAY 200
STRING https://www.youtube.com/watch?v=dQw4w9WgXcQ
ENTER
DELAY 3000
STRING f
```

<H1>ATTENTION</H1>

<h2> ​
Pour ne pas vous infecter ou faire tourner le script sur votre pc, il suffira de rester appuyer sur le bouton blanc et de brancher le Raspberry Pico en même temps. (Image ci-dessous) </h2>

![images](https://user-images.githubusercontent.com/96829109/188454493-97842ca5-955c-4fe4-924b-1b3775619e33.jpg)

<h3>Je ne suis pas responsable de l'utilisation des fichiers et du tutoriel.</h3>




