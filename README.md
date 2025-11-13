# 🌐 Mettez en place des infrastructures et services Web sécurisés

<span style="color:#0099FF">Mettez en place des infrastructures et services Web sécurisés</span>

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
- 1. Installer et configurer une VM Linux avec Ubuntu Server pour le serveur LAMP.
    - Avec deux Pattes Réseaux : 
        - Public simulé avec `150.10.0.0/16`
        - Privé avec `192.168.10.0/24`

- 2. Créer deux sites distincts :  
  - 🌐 **Extranet public**  - Acces Public simulé sur `150.10.0.0/16`
  - 🔒 **Intranet privé** - Acces Uniquement via la patte réseau `192.168.10.0/24`

- 3. Redirection HTTP vers HTTPS avec generation Certificat SSL

- 4. Mettre en place un serveur FTPS sécurisé
    - Les **developpeur** ont *acces* a l'ensemble des fichiers `/Extranet` et `/Intranet`
    - Les **graphistes** ont *accès* seulement aux Dossiers `/Images` de chaque sites, Extranet et Intranet
    - Toute personne ayant *acces* à l'Extranet doit pouvoir deposer un fichier .PDF dans le dossier `/pdf` dans Extranet depuis l'Extranet

- 5. Configurer un filtrage réseau strict :
    - Avec UFW
    - Mod_Evasive

- 6. Déployer CrowdSec pour prévenir les attaques :
    - Simuler des Attaques et Remonter sur la console CrowdSec