# Synoptique

## Synoptique

### Installation intéractive
Voici un diagramme expliquant la communication des différents élément présentes lors de l'ibstallation.

````mermaid
graph TD
    Ordinateur["Ordinateur central"]
    
    subgraph Éléments_Audio
        Synthé["Synthétiseur"]
        Micro["Micro"]
        HP["Haut-parleurs"]
        Casque["Casque"]
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
    Ordinateur --> |Envoi vidéo| TV1 & TV2 & TV3
    Ordinateur --> |Interface DMX via| QLC
    

    

    %% Réseau
    Ordinateur --> |Connexion réseau| SwitchPOE
    SwitchPOE --> |Connexion via| CableEthernet --> AtomPOE

    %% Contrôles via AtomPOE
    AtomPOE --> Knobs
    AtomPOE --> Sliders
    AtomPOE --> BoutonM5Stack

````

## Références

* [Synoptique](https://tim-montmorency.com/582523-gestion/#/contenus/3_planification/10_synoptique/)

