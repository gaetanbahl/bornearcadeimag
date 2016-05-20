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

Le manuel de l'écran et une doc sur son entretien se trouvent dans le dossier "ecran".

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

### Haut-parleurs

Les haut-parleurs sont branchés au PC et se trouvent dans le bas de la borne d'arcade. 
Ce sont les haut-parleurs de mon tout premier PC (1996), prenez-en soin :)

## Logiciel

###Distribution : GroovyArcade

GroovyArcade est une distribution pour borne d'arcade basée sur Archlinux. Le projet
est éparpillé un peu partout sur la toile, donc j'ai mis la dernière iso 32 bit que j'ai
trouvée sur mon drive : https://drive.google.com/open?id=0B1wBYVhSt02eTnh2VndhN2dnLU0

Disons-le tout de suite, il n'est pas possible d'installer d'autres paquets que ceux
qui sont déjà présents dans la distro. Il faudrait déjà connecter le PC de la borne 
à internet, et on serait obligés de mettre à jour pacman et plein de trucs, sauf que
ça casse immédiatement tout parce qu'apparemment pacman a changé de format de base de 
données depuis et on peut pas utiliser l'ancienne et voilà bref c'est pas possible.

Le seul moyen d'installer des logiciels est de les compiler en 32 bits sur autre machine 
(une VM par ex) et de les installer manuellement sur la borne.

###Kernel

Pour que le PC puisse sortir du 15Khz, il faut que le Kernel soit patché pour que le driver
ATI gère ce mode. GroovyArcade est pré-patchée pour le 15Khz.

Nous avons cependant dû modifier et recompiler le kernel nous mêmes pour que les directions
haut et gauche des joysticks soient correctement lues depuis la carte Xin Mo (cf plus haut).
Ce sont quelques lignes à modifier dans la noyau linux avant la compilation pour que celui-ci
borne les valeurs trop négatives ou trop positives dans l'intervalle de la spec au lieu de
les ignorer.

Ce soucis est réglé dans les noyaux récents, mais nous avons utilisé un kernel 3.7.7 car
c'est celui proposé par défaut dans l'iso de groovy et n'avions pas de patch 15Khz pour des 
kernels récents de toutes manière. Le patch pour 3.7.7 est dans le dépôt (dossier patch-3.7
dans kernel)."man patch" pour pouvoir l'appliquer sur le kernel.

Le patch pour d'autres kernels peut être trouvé là : http://makotoworkshop.org/sources/patch15khz/

Pour que la Xin Mo fonctionne correctement il faut modifier le fichier drivers/hid/hid-input.c dans les sources de Linux. J'ai inclus ce fichier dans le dossier kernel. Les lignes à modifier ont été commentées (ça commence à la ligne 1023), et remplacées par ce qui est dans les
quelques lignes d'en dessous.

J'ai inclus les sources du kernel déjà patché dans kernel/. Si vous voulez compiler le kernel
il faudra le faire sur une machine 32 bits, ou dans une VM 32 bits. J'ai pour ma part utilisé
une Debian 8 32bits. Il n'est pas possible de compiler directement sur la borne, cela prendrait trop de temps
et les outils de compilation ne sont pas installés

J'ai également inclus le kernel compilé qui est utilisé actuellement 
(fichier 3.7.7-ARCH.tar.bz2), il suffit de le décompresser
et de l'installer. Se référer à la doc de Archlinux https://wiki.archlinux.org/index.php/Kernels/Traditional_compilation#Compilation_and_installation

###Frontend : Wah!Cade

Cette distribution lance automatiquement WahCade, un frontend permettant d'avoir une liste
des roms à disposition et de les lancer avec les émulateurs qui vont bien. Pour configurer
WahCade, il faut le quitter, puis une fois dans le menu de Groovy aller dans setup, puis 
frontend, choisir LXDE, revenir en arrière, faire start frontend. On arrive ensuite sur 
le bureau LXDE où il y a un raccourci pour WahCade setup. Une fois les réglages terminés, 
lancer lxterminal avec Alt-F2, faire "setxkbmap fr" si besoin, lancer "sudo gasetup", refaire
la manip faite plus haut en choisissant wahcade à la place de lxde, et redémarrer le PC 
("sudo reboot").

Le bureau lxde sera dégueulasse (texte non lisible)  parce que la résolution de l'écran est trop faible. Pour 
être sûrs de ce que vous faites, ayez à votre disposition sur un autre PC un VM avec GroovyArcade et faites les manips en même temps.
Il n'est PAS possible de brancher le VGA sur un moniteur classique juste pour faire les 
manips car la sortie vidéo du pc sera en 15Khz, ce qui n'est pas géré par les écrans LCD.

Les fichiers de configuration se trouvent dans ~/.wahcade

###Emulateur : Gens

Pour l'instant, le seul émulateur configuré est gens, pour émuler la Genesis/Megadrive.
Gens est un buggué et ne sauvegarde pas automatiquement la configuration. Lorsqu'un changement
de configuration est fait, il faut exporter le fichier de config (menu config -> export config as ou un truc du genre) dans ~/.gens/ avec le nom "config". FAITES UN BACKUP DE L'ANCIEN AVANT. D'ailleurs si vous en avez l'occasion, passez le moi, il faut que je le mette sur ce
git, je n'ai pas eu le temps de le faire avant de partir de l'imag.

### Roms

Les roms megadrive sont stockées dans ~/Roms. Il faut l'indiquer à WahCade lors de la 
configuration d'un émulateur pour qu'il puisse localiser les jeux et en faire une liste.
Il a donc fallu lui indiquer que les roms pour l'émulateur gens se trouvent dans ~/Roms et
qu'elles ont pour extension .bin (et non .zip !).



## Pistes d'amélioration

