### Projet Odysée Mécanique
## Planification Technique

# Description
Planification complète d'une installation multimédia interactive en traitant les aspects conceptuels, scénaristiques, techniques et logistiques.

Livrable: Document technique en ligne avec URL

Cette activité consiste à concevoir une planification détaillée pour un projet multimédia, intégrant la réflexion sur le concept, le scénario interactif, le scénarimage, le synoptique, la plantation des dispositifs, ainsi que l’anticipation des besoins matériels et logiciels.
# Communication
## Concept
Recréé un atmosphère des années 1978 avec le jeu d'arcade réinventer de Space Invaders. Les joueurs seront poussé à faire competition pour battre le record du plus grand concurrent antécédant.

Je veux intégrer les connaissances apprises pendant la technique pour effectuer un jeu avec une capacité physique mobile pour que le testeur/joueur est une expérience de cette arcade bien plus réaliste et immersive avec les lasers et tout.






# Visualisation
![Paint](medias/paintExpl.PNG)









## Scénario
Le joueur sera invité à jouer au jeu. Pour débuter le jeu, il devra actionner le bouton [Appuyer pour tirer].

Le jeu débutera alors de difficulté croissante. Débutant ainsi relativement lentement. Le joueur devra déplacer le TriggerStick de gauche à droite pour déplacer son vaisseau tireur. Il devra aussi esquiver les tirs ennemies et appuyer sur le bouton pour tirer les cibles aussi.

Le joueur pourra attraper des Pouvoirs temporaires en jeu lui procurant un avantage temporel.

Le joueur aura trois vies, pour lequel il détiendra d'un 3 secondes d'immunité à chaque perte de vie.

Une fois la partie terminé, il pourra soit partir, ou réappuyer le boutons du TriggerStick pour recommencer une autre partie.
## Scénarimage
```mermaid
graph TD;
    A[Accueil] --> B{Prendre le levier, Appuyer pour tirer};

    B -->|Tirer| C;
    B -->|Pas tirer| A;

    C{Expérience commence};

    C -->|Perdre une vie| E;
    C -->|Tirer un item PowerUp| F(Buff temporaire du tirs);

    F -->|Perdre une vie| E;
    E[Jeu continue avec 3 secondes d'invicibilité];

    E -->|Perdre tout les vies| H;
    

    H[Game Over];
    H-->|Tirer pour recommencer| A;

    

    
```
## Simulation
![visuel](medias/scenarimage.PNG)

## Synoptique

```mermaid
graph TD;
    %% Définition du studio
    subgraph Studio
        Projecteur[Projecteur vidéo - Projection du jeu]
        
        subgraph Kiosque
            CapteurMouvement1[Détecteur de mouvement M5Stack 1]
            Levier[TriggerStick avec bouton Bluetooth]
            
            
            CapteurMouvement2[Détecteur de mouvement M5Stack 2]
        end
        
        Speakers[Hauts-parleurs stéréo]
    end
    
    %% Définition du système de jeu
    subgraph Systeme_Jeu
        Ordinateur[Ordinateur avec Unity]
        Arduino[Capter dans Arduino l'emplacement et le bouton]
    end
    
    %% Connexions
    CapteurMouvement1 -->|Envoie données de position ou TOF1| Arduino
    Projecteur -->|Affiche le jeu| Ordinateur
    Levier -->|Envoie signal du bouton| Arduino
    
    
    
    Arduino -->|Communication des capteurs et bouton| Ordinateur
    CapteurMouvement2 -->|Envoie données de position ou TOF2| Arduino
    Ordinateur -->|Position du joueur| Projecteur
    Ordinateur -->|Gère l'audio stéréo| Speakers
    
    Speakers -->|---------
     Son spatialisé selon emplacement| Studio

```
### Kiosque
```mermaid
graph TD;
    %% Définition du kiosque
    subgraph Kiosque
        Levier[TriggerStick avec bouton Bluetooth]
        
        CapteurMouvement1[Détecteur de mouvement M5Stack 1]
        CapteurMouvement2[Détecteur de mouvement M5Stack 2]
        Bouton[Signal de tir depuis le levier]
    end

    %% Connexions
    Levier -->|Envoie signal du bouton| Arduino
    CapteurMouvement1 -->|Envoie données de position| Arduino
    CapteurMouvement2 -->|Envoie données de position| Arduino

```
### Son & Vidéo
```mermaid
graph TD;
    %% Définition des haut-parleurs et du projecteur
    subgraph Studio
        Projecteur[Projecteur vidéo - Projection du jeu]
        Speakers[Hauts-parleurs stéréo]
    end

    %% Connexions
    Projecteur -->|Affiche le jeu| Ordinateur
    Ordinateur -->|Gère l'audio stéréo| Speakers
    Speakers -->|Son spatialisé selon emplacement
    -| Studio

```
### Informatique
```mermaid
graph TD;
    %% Définition du système
    subgraph Systeme_Jeu
        Arduino[Carte Arduino pour capteurs et bouton]
        Ordinateur[Ordinateur avec Unity]
    end

    %% Connexions
    Levier -->|Envoie signal du bouton| Arduino
    CapteurMouvement1 -->|Envoie données de position OSC| Arduino
    CapteurMouvement2 -->|Envoie données de position OSC| Arduino
    Arduino -->|Communication des capteurs et bouton OSC| Ordinateur
    Ordinateur -->|Gère le jeu et la logique| Arduino


```
### Interaction
```mermaid
graph TD;
   

    %% Section interaction
    subgraph Interaction
        Levier[TriggerStick avec bouton Bluetooth]
        CapteurMouvement1[Détecteur de mouvement M5Stack 1]
        CapteurMouvement2[Détecteur de mouvement M5Stack 2]
        Bouton[Signal de tir depuis le levier]
    end
    
    %% Connexions
   
    Levier -->|Envoie signal du bouton| Arduino
    
    CapteurMouvement1 -->|Envoie données de position ou TOF1| Arduino
    CapteurMouvement2 -->|Envoie données de position ou TOF2| Arduino
    


```
### Branchement
![branchement](medias/branchement.png)
## Logiciels & Réseaux
### Logiciels:
* Unity
* PlugData
* Arduino
* Maya
* VCV Rack
### Réseautage:
Arduino communique grâce à une communication OSC vers Unity dans l'ordinateur. Unity générera le son transmis au travers les speakers et la projection sera celle que Unity génerera grâce à l'OSC.

Les Time Of Flights envoyeront des données pour calculé l'emplacement du vaisseau mère.





## Plantation

![Grand Studio](medias/plan_des_studios_2D.jpg)

Studio T.I.M Montmorency





## Études matériels
*  1 x Installation interactive
* Projecteur vidéo
* Ordinateur (Arduino & Unity avec Plugdata comme osc communication)
* Stock M5Stack
    - 1 Mechanical key [Bluetooth version]
    - 2 TOF ou 3 PIR M5Stack
* Kiosque prisme rectangulaire
* 2 Haut-parleurs
* TriggerStick


### Etude Projecteur
![Projecteur](medias/projecteur.png)

Servira à projeter l'expérience sur une étandue élevé. Placé pas trop loin pour éviter une pollution visuels des pixels.
[DOCUMENTATION](https://www.bureauengros.com/products/3094403-fr-optoma-technology-4k400stx-projecteur-dlp-4k-uhd-a-courte-focale-4-000-lumens) 

### Etude Kiosque
![Kiosque](medias/kiosque.png)

Servira à l'interactivité. C'est l'endroit ou le joueur pourra intéragir avec l'expérience en tant que telle. Ce kiosque sera aménagé avec tout les matériels pour le bon fonctionnement de l'expérience.
### American DJ
![light](medias/5px-hex-01-39923.jpg)

Lumière directement visé sur le kiosque tout en évitant tout intensité trop élevé. Accorde une luminosité minimale pour intéragir avec l'expérience.
[DOCUMENTATION](https://www.adj.com/5px-hex)
### Etude Equipement M5Stack
#### Etude Bouton
![triggerstick](medias/triggerstick.png)

Batton avec bouton pour tirer. il est une visualisation de ce que je veux reproduire. Le batton sera toutefois fait à la main et ressemblera bien plus à ça : 

![ideaTrigger](medias/ideal.png)
#### Etude TOF
![TimeOfFlight](medias/timeOfFlight.png)

Le "Time of Flight" de M5Stack sera utilisé pour détecter l'emplacement du levier.

[DOCUMENTATION](https://eu.mouser.com/new/m5stack/m5stack-tof-distance-sensor/) 
#### Etude Key Unit
![bluetoothButton](medias/m5stackButtonBluetooth.png)

Placé directement sur le triggerstick, il sera le bouton bluetooth qui communiquera avec Arduino. À l'action, il enverra un message comme expliqué dans le synoptique. [OSC]
[DOCUMENTATION](https://www.tinytronics.nl/en/switches/manual-switches/push-buttons-and-switches/m5stack-button-unit)

### Etude Speaker
![Speaker](medias/genelec.png)

Positionner sur le plafond du studio.

[DOCUMENTATION](https://www.genelec.com/8040b)

### Etude Câbles
* Câble XLR 3pines
 
 ![XLR-NoWire](medias/xlrWire.jpg)
[Acheter Amazon](https://www.amazon.ca/AmazonBasics-C%C3%A2ble-microphone-m%C3%A2le-femelle/dp/B01JNLTTKS/ref=sr_1_1_ffob_sspa?dib=eyJ2IjoiMSJ9.Qc7Bm99GBP3_XdgZcQz45tvwI3ZqROZzvEu4V-F-QT388d0dx-YLODgUtsRmCb0TR1FPGUPEwhox88PlZm-JDHYXqmpN1VxeKf3W5k1g5NU1RZ2TFPbPHEgvEOSrXuJr0p9KFPer01MgBdV8xSHpXD5YZ1GfRCRcvu-F_YgfHtW0nnIjJADUKZ3dbmYpX97Y90rhmCpxBn37eHkWwjjazddP0l0gZG9GyMqQk0WBrxC5mV0aQjAITQ2gDr7Wvfz22xvF73O-EgQPh9p3sYhI7UYglNw0inOt6GjZYTSyBVE.dWFeMSa3GcqU8O-ySO4vj7Pt5r6aBAjf_mexNg1_OKA&dib_tag=se&hvadid=208379556679&hvdev=c&hvlocphy=9000598&hvnetw=g&hvqmt=e&hvrand=5867566891861396795&hvtargid=kwd-299658550019&hydadcr=5480_9838916&keywords=cable%2Bxlr&qid=1730664946&sr=8-1-spons&sp_csd=d2lkZ2V0TmFtZT1zcF9hdGY&th=1 )

* Câble XLR vers USB 3pines
 
 ![XLR-USB](medias/USB-XLR.jpg)
[Acheter Amazon](https://www.amazon.ca/femelle-microphone-adaptateur-instruments-enregistrement/dp/B07WR14TYX/ref=sr_1_4_sspa?__mk_fr_CA=%C3%85M%C3%85%C5%BD%C3%95%C3%91&crid=2IOWF3QHGFSZN&dib=eyJ2IjoiMSJ9.dQGpMpgA9Iulza1HVu-XlK5gRTuLdXG4dKc3tbkKYKA-jMTHiCHNEq1TxnnkXODERf6h6RV-d2g33HtukI6CtW-rpr89U-fAFdxlsNMZ4OfGr21F6ud2zMlh0LZVeyRD0NEMft_wn6JiwvrKmUaYTlQTdfAbuoZpqtVW8t33pGZMe2eCrpvzHhdHhy04AVP7s8HqiZ-ufZRq5aGKWQAI3qPhduy1nDt4jcRi3K5roeoHq32kwXn4Mz8g2hQ1RTwyvAErp7RcdgnHTD0Kfsecbc5vVrnb_O79Sg42bqguw1c.Nf0Li0DKLt-J9auJCgwXc5akNUq49SsF3rtb7SSuqas&dib_tag=se&keywords=cable+xlr+usb&qid=1730665110&sprefix=cable+xlr+usb%2Caps%2C83&sr=8-4-spons&sp_csd=d2lkZ2V0TmFtZT1zcF9hdGY&psc=1)

 * Barre Multi-prise
  
 ![Multi-prise](medias/multi-prise.jpg)
 
 [Acheter Amazon](https://www.amazon.ca/-/fr/Multiprise-interrupteurs-individuels-multiprise-rallonge/dp/B08617QZN5)
## Visiteurs & Sécurité
Les visiteurs auront une zone auquel il ne pourront pas traverser si un autre visiteur est dans cette zone. Limitant tout risque de contact et risque de blessure.

Le TriggerStick aura un feutre dessus pour éviter tout blessure au main d'un coup que le déplacement "JAM" d'un coup-sec. Un feutre& ou un ressort épais amortissera aussi le méchanisme de mouvement s'il est poussé aux rebords.
## Câblage
Étant donné que l'installation est dans le studio, le stock peut être caché dans le kiosque. Les prises dans le sol permettent de cacher les fils et pour ceux du projecteur et et speakers au plafond, il sera simple de placer les fils pour qu'ils longent un mur inutilisé. 

![Visualisation câblage](medias/visualisation.PNG)








# Mediagraphie
* [Jeu Web](https://www.free80sarcade.com/spaceinvaders.php#google_vignette)
* [Specification Projecteur](https://www.bureauengros.com/products/3038983-fr-epson-projecteur-intelligent-portable-1080p-epiqvision-flex?listId=collection)
* [Documentation détection distance](https://en.wikipedia.org/wiki/Time_of_flight)
* [3D spatiale](https://www.artstation.com/artwork/kBWkx)


###### *Documentation par Isaac Fafard