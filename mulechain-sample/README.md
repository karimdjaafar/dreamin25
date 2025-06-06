# MuleSoft AI Chain - Knowledge Management System

## Description

Ce projet MuleSoft implémente un système de gestion de connaissances basé sur l'IA utilisant les capacités d'embedding et de recherche sémantique. Il permet de traiter automatiquement des documents, de créer des bases de connaissances et d'interroger ces dernières via des API REST.

## Fonctionnalités

### 1. Traitement automatique de documents
- **Surveillance SFTP** : Détection automatique de nouveaux fichiers dans `/muletest/upload/new/`
- **Extraction et stockage** : Sauvegarde locale temporaire des documents
- **Intégration embedding** : Ajout automatique des documents à la base de connaissances
- **Archivage** : Déplacement des fichiers traités vers `/muletest/upload/processed/`

### 2. Création de bases de connaissances
- **API REST** : `POST /embedding` pour créer de nouvelles bases de connaissances
- **Stockage distribué** : Synchronisation entre stockage local et SFTP

### 3. Interrogation intelligente
- **API REST** : `POST /prompt` pour poser des questions à la base de connaissances
- **Recherche sémantique** : Utilisation des embeddings pour des réponses contextuelles

## Architecture

Le projet est composé de 3 flows principaux :

### Flow 1: `ingest-knowledge`
**Traitement automatique des documents**
- Écoute les nouveaux fichiers via SFTP
- Traite et intègre les documents dans la base de connaissances
- Archive les fichiers traités

### Flow 2: `knowledge-new-store`
**Création de nouvelles bases de connaissances**
- Endpoint : `POST /embedding`
- Crée une nouvelle base de connaissances
- Synchronise avec le stockage SFTP

### Flow 3: `knowledge-ask-question`
**Interrogation de la base de connaissances**
- Endpoint : `POST /prompt`
- Recherche sémantique dans les documents
- Retourne des réponses contextuelles

## Configuration requise

### Connecteurs MuleSoft
- **SFTP Connector** : Pour la gestion des fichiers distants
- **File Connector** : Pour le stockage local
- **HTTP Connector** : Pour les APIs REST
- **MuleSoft AI Chain Connector** : Pour les fonctionnalités d'IA

### Configuration SFTP
- Serveur SFTP configuré avec les répertoires :
  - `/muletest/upload/new/` : Dépôt des nouveaux documents
  - `/muletest/upload/processed/` : Archive des documents traités
  - `/muletest/upload/embedding/` : Stockage des bases de connaissances

## Installation et déploiement

### Prérequis
1. Anypoint Studio ou environnement MuleSoft Runtime
2. Accès à un serveur SFTP
3. Licence MuleSoft AI Chain

### Étapes de déploiement
1. Cloner le repository
2. Configurer les connexions SFTP dans les fichiers de configuration
3. Configurer les endpoints HTTP selon votre environnement
4. Déployer l'application sur votre runtime MuleSoft

## Utilisation

### Création d'une base de connaissances
```bash
curl -X POST http://localhost:8081/embedding \
  -H "Content-Type: application/json" \
  -d '{"storeName": "ma-base-connaissances.store"}'
```

### Interrogation de la base
```bash
curl -X POST http://localhost:8081/prompt \
  -H "Content-Type: application/json" \
  -d '{"question": "Quelle est la procédure pour...?"}'
```

### Ajout de documents
Déposez simplement vos fichiers dans le répertoire SFTP `/muletest/upload/new/` et ils seront automatiquement traités et intégrés à la base de connaissances.

## Structure du projet

```
mulechain-project/
├── src/main/mule/
│   └── mulechain-sample.xml
├── src/main/resources/
│   └── (fichiers de configuration)
└── README.md
```

## Configuration des embeddings

- **Taille maximale des segments** : 2048 caractères
- **Taille de chevauchement** : 2048 caractères
- **Types de fichiers** : Tous formats supportés

## Monitoring et logs

Le système génère des logs détaillés pour :
- Le traitement des fichiers
- Les opérations d'embedding
- Les requêtes de recherche
- Les erreurs de traitement

## Contribution

1. Fork le projet
2. Créez une branche pour votre fonctionnalité
3. Commitez vos changements
4. Poussez vers la branche
5. Ouvrez une Pull Request

## Support

Pour toute question ou problème :
- Consultez la documentation MuleSoft AI Chain
- Vérifiez les logs de l'application
- Contactez l'équipe de développement

## Licence

openSource
