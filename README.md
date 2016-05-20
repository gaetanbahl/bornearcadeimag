# Documentation Borne d'arcade de la cafet de l'Ensimag

##WORK IN PROGRESS

Ce dépôt git contient des informations concernant la borne d'arcade
se trouvant dans la cafétéria de l'Ensimag. Elle était là depuis 
longtemps (on m'a dit plus de 10 ans) et nous l'avons remise en état de marche en 2016.

Les informations et fichiers contenus dans ce dépôt peuvent être
utiles dans l'éventualité d'une panne de la borne ou pour des modifications
futures.


## Matériel

Si il faut remplacer du matos, commandez ici : http://joystick-arcade.com

### Borne

La borne date du milieu ou de la fin des années 80, ceci est indiqué par la présence d'un 
cendrier entre les boutons du joueur 1 et du joueur 2, ce qui n'existe plus
depuis le début des années 90, et par le connecteur
interne au standard JAMMA, qui a été créé au milieu des années 80.

Elle comporte une serrure à l'arrière qui a dû être forcée car nous n'avions pas la clef.
Il est possible d'installer un cadenas à l'avant.

### Écran

Le manuel de l'écran et une doc sur son entretien se trouve dans le dossier "ecran".

L'écran est un Hantarex MTC 9000, produit dans les années 80. Le contraste,
la luminosité et la quantité de chaque couleur se règlent avec des 
potentiomètres à l'arrière de la borne.
Il y a une petite carte à droite du pc à l'intérieur de la borne pour régler le
balayage, la position, et la taille de l'image. Ce sont des
résistances variables, ça se règle bien avec un couteau.

L'écran est branché à la carte Jamma par trois fils (RGB) et fonctionne en 15Khz.
Il ne peut donc pas prendre un signal 31Khz classique.

L'écran s'allume avec le petit switch gris situé au dessus de la borne.

### Joysticks et boutons

Les boutons sont classiques, une pin prend la masse, l'autre un +quelquechose, il n'y
a pas de sens.

Les joysticks sont classiques également, ils utilisent un connecteur 5 pins
(une pin noire pour la masse), 4 pins pour les quatres directions). 

Au moment de l'écriture de ce readme, le bouton 6 du joueur 2 n'est pas branché (le câble était trop court, et ce bouton n'était pas utile pour l'émulation de la megadrive).

Il peut arriver qu'un des joysticks se débranche. Pour le rebrancher, il faut faire basculer
le panneau des joysticks. Pour ce faire, ouvrir la porte avant de la borne, passer la main
par en haut, il y a deux loquets (type bouteille de Fisher) à ouvrir, (un à gauche, un
à droite), pour que le panneau bascule. C'est normal de ne pas les voir quand on regarde depuis l'extérieur de la borne. Il faut chercher à l'aveugle ou avec une caméra. 

<img src="/images/loquet.jpg" height=100px \>

### Interface ultimarc JPAC JAMMA

![JPAC](/images/jpac.jpg)

La borne étant au standard Jamma, il y a un conecteur jamma à l'intérieur. Pour l'utiliser,
il est relié à une interface JPAC. L'interface JPAC permet normalement d'utiliser les
joysticks avec un PC, et d'utiliser la sortie vidéo du PC pour l'afficher sur l'écran, mais
la partie joystick de cette JPAC n'est pas fonctionnelle (elle a sans doute grillé suite
à des manipulations hasardeuses). Néanmoins, la partie VGA fonctionne bien et est utile pour
afficher un signal 31Khz sur l'écran 15Khz (ça affiche l'image deux fois, mais au moins
ça l'affiche), pour aller dans le bios du pc, par exemple. Ici, donc, la JPAC n'est utilisée
que pour convertir le signal VGA en ce qui va bien pour l'écran 15Khz.

La documentation concernant la JPAC se trouve là https://www.ultimarc.com/jpac2.html

### Interface joystick usb 


<img src="/images/interface.jpg" height=200px \>

http://www.joystick-arcade.com/fr/adaptateurs-convertisseurs/138-interface-usb-2-joueurs-cosses-28mm-pour-raspberry-pi-pc-ps3.html

Puisque la partie contrôles de la JPAC n'est pas fonctionnelle et qu'une JPAC neuve coûte
cher, nous avons opté pour une petite interface usb de marque Xin-Mo.

http://www.xin-mo.com/dual-players-controller.html

La description des pins est dans le pdf suivant : https://github.com/gaetanbahl/bornearcadeimag/raw/master/Schema_Encodeur_Joystick-boutons_arcade_USB-2j.pdf

Pour savoir quel bouton est relié à quel pin il suffit de suivre les câbles.

Il est important de noter que cette interface usb ne respecte pas entièrement la spécification USB
car elle produit des valeurs trop négatives lorsque l'on utilise les directions hautes et gauche des joysticks.
C'est pourquoi nous avons dû modifier quelques lignes de code du noyau Linux pour accepter
ces valeurs (voir partie Logiciel ci-après).

### Ordinateur

L'ordinateur est à base d'un Pentium 4, ce qui suffit largement pour de l'émulation de systèmes retro.
Il est à noter que c'est un processeur 32 bits.

La carte graphique du PC est très importante car il faut qu'elle soit capable de sortir
un signal 15Khz. Ces cartes n'existent qu'en AGP, c'est pourquoi il faut une vielle carte
mère (et donc un vieux processeur) pour les faire fonctionner. Si cette carte graphique
venait à tomber en panne, il faudrait la remplacer par une autre carte de la série ATI 9000,
de préférence une 9200.

### Clavier

Un clavier est fixé sur l'intérieur de la porte. La touche Échap est positionnée en face
de l'ouverture où l'on devrait normalement mettre les pièces. Elle est utilisée pour quitter
le jeu, c'est donc pratique de l'avoir en face du trou.

## Logiciel

## Pistes d'amélioration

