# Décodeur

Bienvenue au tutoriel « Décodeur » du Musée des sciences et de la technologie du Canada.

Cette activité nécessite 2 joueurs. Tu vas coder les symboles qui composent le code Morse, un point et un tiret. Tu vas pouvoir utiliser ces symboles pour envoyer des messages codés à ton partenaire. Peux-tu le déchiffrer ?

## Définir le groupe radio
Pour pouvoir envoyer un message, tu dois d'abord régler la fonction radio.
1. Dans l'onglet Radio, fais glisser le bloc ``||radio: définir puissance de transmission (7)||`` et insère-le dans le bloc ``||basic: au démarrage||``. 
2. Choisis ensuite le bloc ``||radio: définir groupe||`` et place-le sous le bloc ``||radio: définir puissance de transmission (7)||``.
3. Clique sur le bouton « Suivant », dans le coin supérieur droit de l'écran, pour passer aux instructions suivantes.

```blocks
radio.setTransmitPower(7)
radio.setGroup(1)
```
## Programmer le point
Maintenant, tu dois programmer le point du code morse que tu enverras à ton coéquipier.
1. Fais glisser le bloc ``||input: lorsque le bouton A est pressé||`` dans ton espace de travail. 
2. Ensuite, fais glisser le bloc ``||basic: montrer LEDs||`` et insère-le dans ``||input: lorsque le bouton A est pressé||``. 
3. Choisis les carrés qui devront s'allumer. Assure-toi qu'ensemble, ils ont la forme d'un point. 
```blocks
input.onButtonPressed(Button.A, function () {
    basic.showLeds(`
        . . . . .
        . # # # .
        . # # # .
        . # # # .
        . . . . .
        `)
```
## Envoyer le point
1. Dans l'onglet Radio, choisis le bloc ``||radio: envoyer le nombre (0) par radio||`` et place-le sous le bloc ``||basic: montrer LEDs||``.
2. Ajoute un bloc ``||basic: pause (ms)||`` à la séquence. 
3. Enfin, ajoute un deuxième ``||basic: montrer LEDs||`` et un autre ``||basic: pause (ms)||`` pour compléter la séquence. Tu n'as pas à choisir de carrés cette fois-ci. Cela correspond à une pause entre tes codes

```blocks
input.onButtonPressed(Button.A, function () {
    basic.showLeds(`
        . . . . .
        . # # # .
        . # # # .
        . # # # .
        . . . . .
        `)
    radio.sendNumber(0)
    basic.pause(100)
    basic.showLeds(`
        . . . . .
        . . . . .
        . . . . .
        . . . . .
        . . . . .
        `)
    basic.pause(100)
})
```
## Programmer le tiret
 
À part quelques petites différences, les étapes de programmation du tiret sont presque les mêmes que celles pour le point. 
 
1. Fais glisser un nouveau bloc ``||input: lorsque le bouton A est pressé||``. Remplace le A par un B. 
2. Ajoute un nouveau bloc ``||basic: pause (ms)||`` à la séquence. Choisis les carrés qui formeront un tiret. Clique sur le bouton d'indice si tu as des doutes. 

```blocks
input.onButtonPressed(Button.B, function () {
    basic.showLeds(`
        . . . . .
        . . . . .
        . # # # .
        . . . . .
        . . . . .
        `)
```
## Envoyer le tiret
1. Ajoute ensuite un bloc ``||radio: envoyer le nombre par radio||``. Remplace le 0 par un 1.
2. Ajoute un bloc ``||basic: pause (ms)||``. 
3. Enfin, ajoute un bloc ``||basic: montrer LEDs||`` vide et un autre ``||basic: pause (ms)||`` pour terminer la séquence. 

```blocks
input.onButtonPressed(Button.B, function () {
    basic.showLeds(`
        . . . . .
        . . . . .
        . # # # .
        . . . . .
        . . . . .
        `)
    radio.sendNumber(1)
    basic.pause(100)
    basic.showLeds(`
        . . . . .
        . . . . .
        . . . . .
        . . . . .
        . . . . .
        `)
    basic.pause(100)
})
```

## Programmer un symbole de fin de message
Pour que ton ou ta partenaire sache que ton message est terminé, nous allons programmer un autre symbole en suivant les mêmes étapes que les deux dernières séquences.
1. Fais glisser un bloc ``||input: lorsque secouer||``. 
2. Ajoute un nouveau bloc ``||basic: montrer LEDs||`` à la séquence. Choisis les carrés qui formeront un X. 

```blocks
input.onGesture(Gesture.Shake, function () {
    basic.showLeds(`
        # . . . #
        . # . # .
        . . # . .
        . # . # .
        # . . . #
        `)
```
## Envoyer symbole de fin de message
1. Ajoute un bloc ``||radio: envoyer le nombre par radio||``. Remplace le 0 par un 2. 
2. Ajoute ensuite un bloc ``||basic: pause (ms)||``. 
3. Enfin, ajoute un bloc ``||basic: montrer LEDs||`` vide et un bloc ``||basic: pause (ms)||`` pour terminer la séquence.

```blocks
input.onGesture(Gesture.Shake, function () {
    basic.showLeds(`
        # . . . #
        . # . # .
        . . # . .
        . # . # .
        # . . . #
        `)
    radio.sendNumber(2)
    basic.pause(100)
    basic.showLeds(`
        . . . . .
        . . . . .
        . . . . .
        . . . . .
        . . . . .
        `)
    basic.pause(100)
})
```

## Programmer la radio pour recevoir un point
 
Cette dernière séquence te permettra de recevoir des messages de ton ou ta partenaire. Suis les étapes très attentivement, et utilise le bouton d'indice si tu as besoin d'une aide visuelle. 
 
1. Pour commencer, choisis le bloc ``||radio: quand une donnée est reçue par radio (receiveNumber)||`` et dépose-le dans ton espace de travail. 
2. Ensuite, choisis le bloc ``||logic: si vrai alors||``. Insère-le dans le bloc ``||radio: quand une donnée est reçue par radio||``. 
3. Tu dois modifier la variable « vrai » dans la fonction logique. Place un bloc ``||logic: 0=0||`` par-dessus ``||logic: vrai||``. 
4. Tu dois maintenant créer une nouvelle ``||variable||``. Nomme-la « receivedNumber ». Remplace le premier ``||logic: 0||`` de la fonction que tu viens d'ajouter par ``||variable: receivedNumber||``.
5. Dans le bloc ``||logic: si…alors||``, tu dois ajouter un ``||basic: montrer LEDs||`` sous la section « si ». Choisis les DEL qui formeront un point. 
```blocks
radio.onReceivedNumber(function (receivedNumber) {
    let receivedNumber = 0
    if (receivedNumber == 0) {
        basic.showLeds(`
            . . . . .
            . # # # .
            . # # # .
            . # # # .
            . . . . .
            `)
    }
```

## Programmer la radio pour recevoir un tiret
1. Clique sur le + au bas du bloc ``||logic: si...alors||`` afin d'ajouter une autre condition à ta variable.
2. Remplace le ``||logic: vrai||`` par ``||logic: 0=0||``, puis remplace le premier 0 par ``||variable: receivedNumber||``. Remplace le deuxième 0 par un 1. 
3. Ajoute un deuxième ``||basic: montrer LEDs||`` à la séquence. Choisis les carrés qui formeront un tiret. 
4. Clique sur le + encore une fois afin d'ajouter un autre bloc ``||logic: si...alors||``. Ajoute un bloc ``||logic: 0=0||`` et remplace le premier 0 par ``||variable: receivedNumber||``. Remplace le deuxième 0 par un 2.

```blocks
radio.onReceivedNumber(function (receivedNumber) {
    let receivedNumber = 0
    if (receivedNumber == 0) {
        basic.showLeds(`
            . . . . .
            . # # # .
            . # # # .
            . # # # .
            . . . . .
            `)
    }
    if (receivedNumber == 1) {
        basic.showLeds(`
            . . . . .
            . . . . .
            . # # # .
            . . . . .
            . . . . .
            `)
    }
```

## Programmer la radio pour recevoir le symbole pour fin de message
1. Ajoute un bloc ``||basic: montrer LEDs||`` et choisis les carrés qui formeront le symbole X.
2. La toute dernière étape est d'ajouter un bloc ``||basic: pause (ms)||`` puis un bloc ``||basic: montrer LEDs||`` vide. 

```blocks
radio.onReceivedNumber(function (receivedNumber) {
    let receivedNumber = 0
    if (receivedNumber == 0) {
        basic.showLeds(`
            . . . . .
            . # # # .
            . # # # .
            . # # # .
            . . . . .
            `)
    }
    if (receivedNumber == 1) {
        basic.showLeds(`
            . . . . .
            . . . . .
            . # # # .
            . . . . .
            . . . . .
            `)
    }
    if (receivedNumber == 2) {
        basic.showLeds(`
            # . . . #
            . # . # .
            . . # . .
            . # . # .
            # . . . #
            `)
    }
    basic.pause(100)
    basic.showLeds(`
        . . . . .
        . . . . .
        . . . . .
        . . . . .
        . . . . .
        `)
})
```
### Une dernière étape
Félicitations, tu as réussi la programmation de l'activité « Décodeur ». Maintenant il est temps de jouer! 
1. Télécharge ta programmation en la sauvegardant sur un disque local.
2. Fais glisser ton fichier .hex sauvegardé vers ton micro:bit (assure-toi qu'il est relié par connexion USB).
3. Débranchez le micro:bit de l'ordinateur et ajoutez le bloc-piles.
4. Essayez-le contre un autre joueur qui possède également un micro:bit codé dans le même groupe radio.
