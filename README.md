# 🌐 Mettez en place des infrastructures et services Web sécurisés

**Projet n°04 Réalisé dans le cadre de la Formation Openclassrooms d'Administrateur systeme réseaux et Cybersécurité**

## Mission 
**Objectif :** Créer un prototype opérationnel pour **l’EXTRANET** et **l’INTRANET** de la **mairie de Valserac**, 
- incluant : 
    - Serveur LAMP sécurisé, 
    - Serveur FTP sécurisé en FTPS
    - Filtrage réseau,
    - Protection avancée.

**Context :**
Administrateur systèmes et réseaux. Le Dr. Bertri a validé le projet. 
Votre mission : fournir un prototype fonctionnel pour valider l’infrastructure avant le développement complet.

--- 

## Objectifs Detaillé :
- **n°1.** Installer et configurer une VM Linux avec Ubuntu Server pour le serveur LAMP.
    - Avec deux Pattes Réseaux : 
        - Public simulé avec `150.10.0.0/16`
        - Privé avec `192.168.10.0/24`

- **n°2.** Créer deux sites distincts :  
  - 🌐 **Extranet public**  - Acces Public simulé sur `150.10.0.0/16`
  - 🔒 **Intranet privé** - Acces Uniquement via la patte réseau `192.168.10.0/24`

- **n°3.** Redirection HTTP vers HTTPS avec generation Certificat SSL

- **n°4.** Mettre en place un serveur FTPS sécurisé
    - Les **developpeur** ont *acces* a l'ensemble des fichiers `/Extranet` et `/Intranet`
    - Les **graphistes** ont *accès* seulement aux Dossiers `/Images` de chaque sites, Extranet et Intranet
    - Toute personne ayant *acces* à l'Extranet doit pouvoir deposer un fichier au format `.PDF` dans le dossier `/pdf` dans Extranet depuis l'Extranet

- **n°5.** Configurer un filtrage réseau strict :
    - Avec UFW
    - Mod_Evasive

- **n°6.** Déployer CrowdSec pour prévenir les attaques :
    - Simuler des Attaques et Remonter sur la console CrowdSec

---

## ![Static Badge](https://img.shields.io/badge/Etape%201?style=flat&logoSize=auto) : Configuration réseau - VM-Serveur

1. VM Créé via VirtualBox : 
    - OS : Ubuntu Server 22.04 - minimal graphic
    - 2 Pattes Réseaux NATNetwork : 
        - `192.168.10.0/24`
        - `150.10.0.0/16`

2. **Attribution IPs Statiques** 
    - Pour intranet (eth0) : `192.168.10.5/24`
    - Pour extranet (eth1) : `150.10.0.5/16`

    - S'assurer que tout est à jours : `sudo apt update && sudo apt upgrade -y`

    - Un Fichier de Configuration IP avec Netplan a été créé au format `.yaml` 
    ici : `/etc/netplan/00-installer-config.yaml`
    ```yaml 
    network:
        version: 2
        ethernets:
            eth0:
                dhcp4: no
                addresses: [192.168.10.5/24]
                gateway4: 192.168.10.1
                nameservers:
                    addresses: [8.8.8.8,8.8.4.4]
            eth1:
                dhcp4: no
                addresses: [150.10.0.5/16]           
    ```
    
    - La configuration réseau a été appliqué via : `sudo netplan apply`
    

**Configuration LAB** :
|         | SERVEUR | DEV | GRAPHISTE |
|----------|--------|-----------|-----------|
| OS      | Ubuntu-Serveur 22.04 | Ubuntu 22.04 | Ubuntu 22.04 |
| Nom DNS | vm-serveur| vm-dev | vm-graphiste |
| IP Privé | `192.168.10.5` | `192.168.10.10` | `192.168.10.12` |
| IP Public simulé | `150.10.0.5` | `150.10.0.10` | `150.10.0.12` |

- Ici le DNS à été simulié via `/etc/hosts` de chaque machine

On a donc mainteant :
- [x] Serveur Configuré
- [x] Machine Dev Test Configuré
- [x] Machine Graphiste Test Configuré
- [x] Réseaux Fonctionnel inter-machine

