# Synoptique

Voici le diagramme qui explique la communication inter logiciel dans l'ordinateur principale.

````mermaid
graph TD
    A[Arduino] -->|Envoie des données| B[OSCBridge]
    B -->|WebSocket| C[Three.js]
    B -->|UDP| D[Plug-Data]
    D -->|Traite les infos reçues| E[Reaper]

````

Voici un diagramme expliquant la communication des différents élément présentes lors de l'installation.

````mermaid
graph TD
    Ordinateur["Ordinateur central"]
    
    subgraph Éléments_Audio
        Synthé["Synthétiseur"]
        HP["Haut-parleurs"]
        CarteSon["Carte son"]
    end
    
    subgraph Éléments_Vidéo
        TV1["Écran 1"]
        TV2["Écran 2"]
        TV3["Écran 3"]
        Splitter["Splitter 4K"]
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
    Ordinateur --> |Connexion| CarteSon
    Synthé --> |Entrée/Sortie audio| CarteSon
    HP --> |Sortie audio| CarteSon

    %% Connexions Vidéo
    Ordinateur --> |Envoi vidéo| Splitter
    Splitter --> |Sortie vidéo| TV1
    Splitter --> |Sortie vidéo| TV2
    Splitter --> |Sortie vidéo| TV3
    Ordinateur --> |Interface DMX via| QLC
    
    %% Réseau
    Ordinateur --> |Connexion réseau| SwitchPOE
    SwitchPOE --> |Connexion via| CableEthernet
    CableEthernet --> |Alimentation et données| AtomPOE

    %% Contrôles via AtomPOE
    AtomPOE --> |Commande| Knobs
    AtomPOE --> |Commande| Sliders
    AtomPOE --> |Commande| BoutonM5Stack
````

Donc, l'utilisateur arrive devant les écrans et se met à utiliser le synthétiseur. Les données du synthétiseur sont reçus dans Reaper par la carte de son. Reaper traite le son avec des effets et analyse le son gràce au plugin de Plug Data. Le son est retourné a l'utilisateur via des hauts parleurs. Plug Data doit alors analyser le son pour isoler les données voulu et ensuite les envoyer vers unity et QLC+. Qlc+ utiliser les données pour changer les lumières et adapter l'ambiance. Unity et un outil de création d'arbre génératif utilisera aussi les données reçu pour rendre châque arbres uniques. Il fait ensuite trois rendues de trois points de vues différents qu'il envoie vers les trois écrans.


