# Mémoiree Technique 

## Table des matières
1. [Introduction](#introduction)
2. [Proposition technique](#proposition-technique)
   - [Description de la topologie réseau choisie](#description-de-la-topologie-réseau-choisie)
3. [Calculs techniques](#calculs-techniques)
4. [Schémas](#schémas)
5. [Maquette fonctionnelle](#maquette-fonctionnelle)
6. [DPGF](#dpgf)
7. [Conclusion](#conclusion)

---

## Introduction
Concevoir un réseau complet pour un bâtiment d’entreprise.
Présente le besoin du client, le type de bâtiment et les contraintes imposées.
- Technologie choisie : Cizco
Explication de l'approche adoptée pour répondre aux exigences du projet.
---

## Proposition 

## Proposition technique

### Description de la topologie réseau choisie
Pour ce projet, nous avons opté pour une **topologie réseau hiérarchique en arborescence** afin de garantir une organisation claire et scalable. Cette structure se compose de trois niveaux distincts : **Core**, **Distribution**, et **Access**.

#### 1. Niveau Core
Le niveau Core représente le cœur du réseau. Il est composé de plusieurs switches interconnectés, offrant :
- **Redondance** : Chaque switch de distribution est connecté à plusieurs switches Core pour éviter toute panne critique.
- **Haute disponibilité** : Le trafic entre les étages et les sous-réseaux est optimisé pour réduire les goulots d'étranglement.

#### 2. Niveau Distribution
Le niveau Distribution sert d'intermédiaire entre le Core et les utilisateurs finaux. Ses caractéristiques principales sont :
- **Segmentation du réseau** : Mise en place de VLANs pour isoler les flux de trafic (par exemple : VoIP, IoT, utilisateurs).
- **Sécurité et contrôle** : Application de politiques réseau pour filtrer et gérer le trafic entre les sous-réseaux.
- **Fiabilité** : Les switches de distribution sont connectés à deux switches Core, garantissant une redondance optimale.

#### 3. Niveau Access
Le niveau Access connecte directement les équipements des utilisateurs finaux, tels que :
- **Postes de travail** : Connexion des ordinateurs et imprimantes.
- **Téléphones IP** : Pour les communications vocales.
- **Caméras de sécurité** : Intégrées au réseau pour la surveillance.
- **Points d’accès Wi-Fi** : Assurant une couverture sans fil dans le bâtiment.

#### Avantages de la topologie hiérarchique
- **Performance** : Les flux de données sont optimisés grâce à la séparation des rôles entre les niveaux.
- **Évolutivité** : Il est facile d'ajouter de nouveaux équipements ou de nouvelles branches sans perturber l'ensemble du réseau.
- **Redondance** : Grâce aux liens multiples entre les switches, le réseau reste opérationnel en cas de panne.
- **Gestion simplifiée** : Chaque niveau ayant un rôle précis, le dépannage et la maintenance sont plus simples.

### Adressage IP
Pour garantir une gestion efficace du réseau, l’adressage IP a été soigneusement planifié en fonction des besoins de chaque VLAN. Voici les détails de l'adressage :
- **VLANs** : Chaque département ou service se voit attribuer un VLAN unique pour isoler le trafic réseau et renforcer la sécurité.
- **Réseau IP** : Chaque VLAN a son propre réseau IP pour faciliter la configuration et le routage.
- **Accessibilité** :  Les règles d'accès inter-VLANs, aux imprimantes et à Internet sont définies pour répondre aux besoins des utilisateurs tout en respectant les bonnes pratiques de sécurité.
- **Taille et plage d'adresses** : Chaque VLAN dispose d'une plage d'adresses suffisante pour couvrir le nombre d'appareils connectés.
- **Passerelle par défaut** : Une passerelle est définie pour chaque VLAN afin d'assurer une connectivité optimale.

### Tableau d’adressage IP :

| **VLAN**                | **id VLAN** | **Réseau IP**    | **Est accessible par les autres VLAN** | **Accès aux autres VLAN** | **Accès imprimantes** | **Accès à internet** | **Taille** | **Masque**        | **Passerelle par défaut** | **Nb max d’appareils** | **Adresse de début** | **Adresse de fin** |
|-------------------------|-------------|------------------|---------------------------------------|---------------------------|-----------------------|----------------------|------------|-------------------|--------------------------|------------------------|----------------------|---------------------|
| RH                      | 10          | 192.168.10.0     | Non                                   | Non                       | Oui                   | Oui                  | /24        | 255.255.255.0     | 192.168.10.1             | 254                    | 192.168.10.1         | 192.168.10.254      |
| Comptabilité            | 11          | 192.168.11.0     | Non                                   | Non                       | Oui                   | Oui                  | /24        | 255.255.255.0     | 192.168.11.1             | 254                    | 192.168.11.1         | 192.168.11.254      |
| Design                  | 12          | 192.168.12.0     | Non                                   | Non                       | Oui                   | Oui                  | /24        | 255.255.255.0     | 192.168.12.1             | 254                    | 192.168.12.1         | 192.168.12.254      |
| Logistique              | 13          | 192.168.13.0     | Non                                   | Non                       | Oui                   | Oui                  | /24        | 255.255.255.0     | 192.168.13.1             | 254                    | 192.168.13.1         | 192.168.13.254      |
| Imprimantes             | 14          | 192.168.14.0     | Non                                   | Non                       | Oui                   | Oui                  | /24        | 255.255.255.0     | 192.168.14.1             | 254                    | 192.168.14.1         | 192.168.14.254      |
| Direction               | 15          | 192.168.15.0     | Non                                   | Non                       | Oui                   | Oui                  | /24        | 255.255.255.0     | 192.168.15.1             | 254                    | 192.168.15.1         | 192.168.15.254      |
| DSI                     | 16          | 192.168.16.0     | Non                                   | Non                       | Oui                   | Oui                  | /24        | 255.255.255.0     | 192.168.16.1             | 254                    | 192.168.16.1         | 192.168.16.254      |
| R&D                     | 17          | 192.168.17.0     | Non                                   | Non                       | Oui                   | Oui                  | /24        | 255.255.255.0     | 192.168.17.1             | 254                    | 192.168.17.1         | 192.168.17.254      |
| Dev                     | 18          | 192.168.18.0     | Oui                                   | Oui                       | Oui                   | Oui                  | /24        | 255.255.255.0     | 192.168.18.1             | 254                    | 192.168.18.1         | 192.168.18.254      |
| Data                    | 19          | 192.168.19.0     | Oui                                   | Oui                       | Oui                   | Oui                  | /24        | 255.255.255.0     | 192.168.19.1             | 254                    | 192.168.19.1         | 192.168.19.254      |
| Conception              | 20          | 192.168.20.0     | Oui                                   | Oui                       | Oui                   | Oui                  | /24        | 255.255.255.0     | 192.168.20.1             | 254                    | 192.168.20.1         | 192.168.20.254      |
| Invités Wi-Fi           | 21          | 192.168.30.0     | Non                                   | Non                       | Non                   | Oui                  | /23        | 255.255.254.0     | 192.168.30.1             | 510                    | 192.168.30.1         | 192.168.31.254      |
| Contrôle d'accès        | 22          | 192.168.40.0     | Non                                   | Non                       | Non                   | Non                  | /26        | 255.255.255.192   | 192.168.40.1             | 62                     | 192.168.40.1         | 192.168.40.62       |
| Sécurité Incendie       | 23          | 192.168.41.0     | Non                                   | Non                       | Non                   | Non                  | /27        | 255.255.255.224   | 192.168.41.1             | 30                     | 192.168.41.1         | 192.168.41.30       |
| Vidéosurveillance       | 24          | 192.168.45.0     | Non                                   | Non                       | Non                   | Non                  | /28        | 255.255.255.240   | 192.168.45.1             | 14                     | 192.168.45.1         | 192.168.45.14       |
| Système audio           | 25          | 192.168.46.0     | Non                                   | Non                       | Non                   | Non                  | /28        | 255.255.255.240   | 192.168.46.1             | 14                     | 192.168.46.1         | 192.168.46.14       |

---

### Équipements

Voici la liste des équipements choisis pour le projet :

| **Équipement**             | **Quantité** | **Prix unitaire** | **Remise** | **Prix après remise** |
|---------------------------|--------------|-------------------|------------|-----------------------|
| **C9130AXI-I**             | 2            | 2 855,00 €        | 50%        | 1 427,50 €            |
| **C9200L-48P-4G-E**        | 1            | 13 230,25 €       | 50%        | 6 615,13 €            |
| **N9K-C9336C-FX2=**        | 1            | 38 477,00 €       | 50%        | 19 238,50 €           |

**Justification des choix techniques** :  
- Le **C9130AXI-I** a été choisi pour sa capacité à gérer de nombreux utilisateurs sans sacrifier la performance du réseau sans fil.  
- Le **C9200L-48P-4G-E** est une solution PoE pour alimenter les appareils réseau via Ethernet, ce qui permet de réduire le besoin en alimentation séparée pour certains dispositifs comme les caméras ou les points d’accès Wi-Fi.  
- Le **N9K-C9336C-FX2=** a été retenu pour son haut débit et sa capacité à gérer de gros volumes de données, adapté aux besoins d'un réseau d'entreprise en pleine croissance.

Ces équipements répondent aux exigences techniques et financières du projet, tout en garantissant une évolutivité future.

---

## Calculs techniques

### Vérification PoE

L'alimentation par Ethernet (PoE) est utilisée pour fournir de l'énergie à plusieurs équipements réseau, comme les points d'accès Wi-Fi, les caméras de surveillance, et les téléphones IP. Afin de garantir que les switchs choisis sont capables de fournir la puissance nécessaire, nous avons effectué une estimation de la consommation PoE totale pour chaque étage et chaque zone du bâtiment.

#### Consommation PoE par équipement :

| **Zone**    | **Consommation PoE (W)** |
|-------------|--------------------------|
| R6          | 90                       |
| R5          | 148                      |
| R4          | 172                      |
| R3          | 170                      |
| R2          | 169                      |
| R1          | 167                      |
| RDC         | 427                      |
| SS1         | 286                      |
| SS2         | 87                       |
| SS3         | 82                       |
| SS4         | 57                       |
| SS5         | 22                       |

**Total PoE consommé : 1877 W**

#### Capacité des switchs à fournir le PoE nécessaire

Les switchs choisis pour ce projet, notamment le **C9200L-48P-4G-E**, sont capables de fournir jusqu’à 370 W de puissance PoE sur 24 ports. En prenant en compte la consommation totale de 1877 W, le nombre de switchs nécessaires pour assurer une alimentation correcte est calculé comme suit :

- Chaque switch **C9200L-48P-4G-E** peut alimenter jusqu'à 370 W via PoE.
- Nombre de switchs nécessaires :  
  \( \frac{1877}{370} \approx 5.07 \)

Nous aurons donc besoin d’au moins **5 switchs** pour répondre aux besoins en PoE du réseau.

Cela garantit que chaque appareil alimenté via PoE reçoit l'énergie nécessaire sans surcharge des switchs.

### Bande passante

L'estimation de la bande passante nécessaire pour chaque étage et zone a été réalisée en fonction des équipements et des usages prévus (comme les postes de travail, téléphones IP, caméras de sécurité, etc.). Cette estimation permet de garantir que le réseau sera capable de gérer le trafic de manière fluide et sans congestion.

#### Consommation de bande passante par zone :

| **Zone**    | **Consommation (Mbps)** |
|-------------|-------------------------|
| R6          | 62                      |
| R5          | 34                      |
| R4          | 40                      |
| R3          | 39                      |
| R2          | 40                      |
| R1          | 112,8                   |
| RDC         | 188                     |
| SS1         | 159                     |
| SS2         | 52                      |
| SS3         | 43                      |
| SS4         | 20                      |
| SS5         | 11                      |

**Total de bande passante consommée : 800 Mbps**

#### Vérification des équipements

Les équipements choisis pour ce projet doivent être capables de gérer la bande passante totale estimée, qui est de **800 Mbps**.

Les switchs **C9200L-48P-4G-E** et les points d'accès **C9130AXI-I** sont spécifiquement conçus pour supporter des débits élevés. Par exemple, chaque switch peut gérer des vitesses de **1 Gbps par port**, ce qui permet de couvrir largement les besoins en bande passante du réseau, même avec un trafic élevé. 

Le réseau est donc dimensionné de manière à garantir que tous les équipements puissent fonctionner simultanément sans congestion, tout en permettant une évolutivité future pour gérer une augmentation du trafic si nécessaire.


## Datasheets des équipements

Voici les spécifications techniques importantes pour chaque équipement choisi pour le projet :

### **C9130AXI-I** - Point d'accès WiFi 6
- **Description** : Ce point d'accès est conçu pour les bureaux d'entreprise à forte densité d'utilisateurs. Il garantit une couverture sans fil optimale et une bonne connexion même dans les zones étendues. Il prend en charge le WiFi 6, offrant ainsi des vitesses plus rapides et une meilleure gestion des appareils connectés simultanément.
- **Caractéristiques principales** :
  - WiFi 6 (802.11ax)
  - Support des bandes 2.4 GHz et 5 GHz
  - Débit théorique maximal : jusqu'à 5.3 Gbps
  - Gestion avancée du spectre radio pour une couverture optimale
  - Sécurité renforcée avec WPA3

### **C9200L-48P-4G-E** - Switch Cisco 48 ports PoE
- **Description** : Le **C9200L-48P-4G-E** est un switch de niveau entreprise avec 48 ports Ethernet PoE et 4 ports uplink haute capacité (de 1G à 10G). Il est idéal pour les réseaux en expansion, offrant une gestion facile des équipements PoE (comme les points d'accès Wi-Fi, les caméras de surveillance, et plus).
- **Caractéristiques principales** :
  - 48 ports Ethernet PoE+ (jusqu'à 370 W PoE total)
  - 4 ports uplink 1G à 10G
  - Capacité de gestion de VLANs et de sécurité avancée
  - Optimisé pour les environnements à haute densité
  - Support de l'automatisation et de la gestion via Cisco DNA Center

### **N9K-C9336C-FX2** - Switch Core Cisco Nexus 9000
- **Description** : Le **N9K-C9336C-FX2** est un switch cœur de réseau ultra-performant avec une latence très faible, conçu pour supporter de lourds trafics dans les datacenters ou les réseaux à très haute capacité. Il est adapté pour les réseaux d'entreprise de grande taille, offrant des performances exceptionnelles.
- **Caractéristiques principales** :
  - 36 ports 100GbE et 48 ports 25GbE
  - Latence ultra-faible pour des performances maximales
  - Support de la virtualisation du réseau avec VXLAN et EVPN
  - Idéal pour les environnements de cloud hybride et les réseaux à fort volume de données

## Conclusion

Ce projet de conception de réseau pour un bâtiment d’entreprise vise à offrir une solution robuste, évolutive et efficace. La topologie en **arborescence hiérarchique** choisie permet d’assurer une gestion claire du réseau, avec une séparation entre les niveaux **Core**, **Distribution**, et **Access** pour garantir des performances optimales et une scalabilité future.

### Avantages de la proposition :
- **Scalabilité** : La solution choisie permet une expansion facile du réseau, avec des équipements capables de supporter un nombre accru d'appareils et un trafic réseau plus élevé sans perturber la performance.
- **Coût** : L'utilisation d'équipements Cisco garantit un rapport qualité-prix optimal, en combinant haute performance et fiabilité. De plus, le recours à la technologie PoE réduit le besoin en alimentation séparée, ce qui simplifie l'installation et réduit les coûts.
- **Efficacité** : Les équipements choisis sont adaptés pour gérer de manière fluide le trafic réseau, même à haute densité d'utilisateurs, tout en assurant une faible latence et une couverture sans fil optimale.

### Perspectives ou améliorations possibles :
- **Améliorations de la sécurité** : Des politiques de sécurité supplémentaires pourraient être mises en place, telles que l'intégration d'une segmentation encore plus poussée des VLANs ou l'utilisation de solutions de détection d'intrusions.
- **Optimisation de la gestion du réseau** : L’intégration de la gestion via des outils comme **Cisco DNA Center** pourrait permettre d’automatiser davantage la configuration et la gestion du réseau.
- **Évolution vers la 5G** : Avec l'essor des réseaux mobiles 5G, une évolution vers cette technologie pourrait être envisagée pour des connexions ultra-rapides et pour l’Internet des objets (IoT) à grande échelle.

---
