Si vous aimez mon travail, n'hésitez pas à me soutenir en me payant une 🍺 ou un ☕. Merci 🙂

 [ ![Download](https://user-images.githubusercontent.com/12702322/115148445-e5a40100-a05f-11eb-8552-c1f5d4355987.png) ](https://www.paypal.me/CyrilGuislain)

<img align="left" width=600 src="https://user-images.githubusercontent.com/12702322/116473468-7b693880-a877-11eb-8783-5eccf0b5fbc0.jpg" />
<img align="right" width=175 src="buildroot/share/pixmaps/logo/marlin-250.png" />

<br /><br /><br /><br /><br /><br /><br /><br />

**Firmware Marlin configuré pour Artillery Sidewinder X1 avec carte mère BigTreeTech SRK 2.0**

Le firmware pour écran BigTreeTech TFT43 3.0 est disponible [ici](https://github.com/Guilouz/BTT-TFT43-Sidewinder-X1).

<br /><br />

Le firmware pour carte mère BigTreeTech SKR 1.4 Turbo est disponible [ici](https://github.com/Guilouz/Marlin-Sidewinder-X1-SKR1.4-Turbo/).

<br />

## ATTENTION

Lire attentivement ceci pour [SKR 2.0 Rev. A et Rev. B](https://docs.google.com/document/d/1IeKgfE2WIDjqH1fx5Yg7n1FOHVwhDFmDlZ-7QMlOEV0/edit?fbclid=IwAR3gCoyRlxSNaZfyHNV_BgGn1apJKmvagmzduOfGGYjY7I8kDBUVAuLyIi4).

EDIT 06/12/2021 : En raison de la pénurie de composants, BigTreeTech utilise désormait une autre version de processeur `STM32F429VGT6` à la place du `STM32F407VGT6`. Il est donc nécessaire de changer l'environnement dans le fichier `platformio.ini` pour la compilation car le firmware fourni dans la partie <a href="https://github.com/Guilouz/Marlin-SuperRacer-SKR2.0-LGX/releases">releases</a> est compilé pour la version `STM32F429VGT6`.

- `default_envs = BIGTREE_SKR_2` <br/>
<img src="https://user-images.githubusercontent.com/12702322/144914479-673edf80-81ff-497d-a279-61d9cbf0199f.jpeg" width="400" /><br/>

- `default_envs = BIGTREE_SKR_2_F429` <br/>
<img src="https://user-images.githubusercontent.com/12702322/144914613-1f89739c-371e-442d-b07d-eaeff1332e45.jpeg" width="400" /><br/>

## Schema de câblage :

![Sidewinder X1 SKR2](https://user-images.githubusercontent.com/12702322/131006518-100e18dd-2e8a-4744-8004-b7228acdadc0.png)

![Capture d’écran 2021-12-08 à 00 44 42](https://user-images.githubusercontent.com/12702322/145123306-7c05586d-4bce-4032-9f6a-ef15c015cfec.jpg)


## Principales fonctionnalités configurées :

- Support carte mère BigTreeTech SKR 2.0
- Support drivers TMC2209/TMC2226 UART
- Support écrans BigTreeTech
- Support Bed Leveling Bilinear 5 x 5 points
- Support BLTouch (High Speed Mode)
- Support M600 & Nozzle Park / Advanced Pause
- Support Babystepping
- Support Neopixels
- Support EEPROM
- Support PID Buse & Plateau
- Support protection thermique contre l'emballement
- Support S-Curve Acceleration & Junction Deviation
- Support G34 - Z Steppers Auto-Alignment
- Support G26 - Mesh Validation Pattern
- Support du transfert de fichier binaire (transfert du fichier firmware à distance via Octoprint)
- Activation du ventilateur de la hotend uniquement quand la chauffe dépasse 50°C
- Support des commandes d'action de l'hôte
- Optimisation du buffer pour Octoprint
- Marlin en français

## Procédure d'installation :

- Effectuez un reset EEPROM avant flash du nouveau firmware (commande M502 suivi de la commande M500 ou via l'écran TFT).
- Copiez le fichier `firmware.bin` à la racine de la carte microSD (capacité max de 32Go, formatée en FAT32, taille d'unité d'allocation 4096).
- Imprimante éteinte, insérez la carte microSD dans le port dédié sur la carte mère et allumez l'imprimante.
- La procédure de flash démarre (sans rien afficher à l'écran) et dure quelques secondes.
- Vérifiez le contenu de la carte microSD, le fichier `firmware.bin` a été renommé en `FIRMWARE.CUR` ce qui indique que le flash s'est bien déroulé.
- Effectuez de nouveau un reset EEPROM (commande M502 suivi de la commande M500 ou via l'écran TFT).
- Lancez un PID Buse & Plateau depuis les paramètres de l'écran.
- Lancez une calibration de l'extrudeur depuis les paramètres de l'écran.
- Lancez une calibration Delta depuis les menus de l'écran.
- Lancez un auto-nivellement depuis les menus de l'écran.

## Changements éventuels :

Ce firmware est configuré pour une carte mère BigTreeTech SKR 2.0 Rev. B avec MCU STM32F407VGT6. Certains changements peuvent être effectués si vous disposez d'une autre version de la carte mère.
    
  - Si `SKR 2.0 Rev. A`, définissez ces valeurs :
    - Dans Configuration.h : `#define MOTHERBOARD BOARD_BTT_SKR_V2_0_REV_A`
    - Dans Configuration_adv.h : `#define DISABLE_DRIVER_SAFE_POWER_PROTECT` en vous assurant d'avoir vérifier ceci : [SKR 2.0 Rev. A et Rev. B](https://docs.google.com/document/d/1IeKgfE2WIDjqH1fx5Yg7n1FOHVwhDFmDlZ-7QMlOEV0/edit?fbclid=IwAR3gCoyRlxSNaZfyHNV_BgGn1apJKmvagmzduOfGGYjY7I8kDBUVAuLyIi4).

  - Si `SKR 2.0 avec MCU STM32F429VGT6`, définissez ces valeurs :
    - Dans platformio.ini : `default_envs = BIGTREE_SKR_2_F429`
  
Recompilez ensuite le firmware à l'aide de VSCode et PlatformIO (voir [ici](https://marlinfw.org/docs/basics/install_platformio_vscode.html)).
