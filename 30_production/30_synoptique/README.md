# Synoptique

Voici un diagramme expliquant la communication des différents élément présentes lors de l'ibstallation.

````mermaid
graph TD
    Ordinateur["Ordinateur central"]
    
    subgraph Éléments_Audio
        Synthé["Synthétiseur"]
        Micro["Micro"]
        HP["Haut-parleurs"]
        CarteSon["Carte de son"]
    end
    
    subgraph Éléments_Vidéo
        TV1["Écran 1"]
        TV2["Écran 2"]
        TV3["Écran 3"]
    end
    
    subgraph Éclairage
        QLC["QLC+"]
    end
    
    subgraph Connectiques
        SwitchPOE["Switch POE"]
        CableEthernet["Câble Ethernet"]
        AtomPOE["Atom POE"]
        Knobs["Knobs"]
        Sliders["Sliders"]
        BoutonM5Stack["Bouton M5Stack"]
    end
    
    %% Connexions Audio
    CarteSon --> |Connectée à| Ordinateur
    Synthé --> |Entrée/Sortie audio| CarteSon
    Micro --> |Entrée audio| CarteSon
    HP --> |Sortie audio| CarteSon
    Casque --> |Sortie audio| CarteSon

    %% Connexions Vidéo
    Ordinateur --> |Envoi vidéo| Spliter 4k
    Spliter 4k --> |Envoi vidéo| TV1 & TV2 & TV3
    Ordinateur --> |Interface DMX via| QLC
    

    

    %% Réseau
    Ordinateur --> |Connexion réseau| SwitchPOE
    SwitchPOE --> |Connexion via| CableEthernet --> AtomPOE

    %% Contrôles via AtomPOE
    AtomPOE --> Knobs
    AtomPOE --> Sliders
    AtomPOE --> BoutonM5Stack

````

Donc, l'utilisateur arrive devant les écrans et se met à utiliser le synthétiseur. Les données du synthétiseur sont reçus dans Reaper par la carte de son. Reaper traite le son avec des effets et analyse le son gràce au plugin de Plug Data. Le son est retourné a l'utilisateur via des hauts parleurs. Plug Data doit alors analyser le son pour isoler les données voulu et ensuite les envoyer vers unity et QLC+. Qlc+ utiliser les données pour changer les lumières et adapter l'ambiance. Unity et un outil de création d'arbre génératif utilisera aussi les données reçu pour rendre châque arbres uniques. 

## Références

* [Synoptique](https://tim-montmorency.com/582523-gestion/#/contenus/3_planification/10_synoptique/)

