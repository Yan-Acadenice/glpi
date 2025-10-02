# Installation GLPI avec Docker Compose

Ce projet contient une installation complète de GLPI (Gestionnaire Libre de Parc Informatique) utilisant Docker Compose avec une base de données MariaDB.

## 📋 Prérequis

- Docker installé sur votre système
- Docker Compose installé
- Port 80 disponible sur votre machine

## 🚀 Installation rapide

### 1. Cloner ou télécharger le projet

```bash
git clone <votre-repo>
cd glpi
```

### 2. Démarrer les services

```bash
docker-compose up -d
```

### 3. Accéder à GLPI

Ouvrez votre navigateur et rendez-vous sur : **http://localhost**

## 📁 Structure du projet

```
.
├── docker-compose.yml    # Configuration Docker Compose
├── .env                 # Variables d'environnement (déjà configuré)
├── storage/
│   ├── glpi/           # Données GLPI persistantes
│   └── mysql/          # Données MySQL persistantes
└── README.md           # Ce fichier
```

## 🔧 Configuration

### Variables d'environnement (.env)

Le fichier `.env` est déjà pré-configuré avec :

```properties
GLPI_DB_HOST="db"
GLPI_DB_PORT="3306"
GLPI_DB_NAME="glpi_mediashcool"
GLPI_DB_USER="glpi_app"
GLPI_DB_PASSWORD="huieznji238U493Nncd!?QSKSO"
```

### Base de données

- **Type** : MariaDB 10.6
- **Base de données** : `glpi_mediashcool`
- **Utilisateur** : `glpi_app`
- **Mot de passe** : `huieznji238U493Nncd!?QSKSO`
- **Root password** : `huieznji238U493Nncd!?QSKSO`

## 🎯 Première connexion GLPI

Lors de votre première connexion sur http://localhost, GLPI vous guidera à travers l'installation :

1. **Sélection de la langue** : Choisissez votre langue
2. **Licence** : Acceptez la licence
3. **Configuration de la base de données** : 
   - Serveur MySQL : `db`
   - Utilisateur MySQL : `glpi_app`
   - Mot de passe MySQL : `huieznji238U493Nncd!?QSKSO`
   - Base de données : `glpi_mediashcool`

### Comptes par défaut après installation

- **Super-Administrateur** : `glpi` / `glpi`
- **Administrateur** : `tech` / `tech`
- **Supervisor** : `normal` / `normal`
- **Hotliner** : `post-only` / `postonly`

⚠️ **Important** : Changez ces mots de passe par défaut après la première connexion !

## 🛠️ Commandes utiles

### Démarrer les services
```bash
docker-compose up -d
```

### Arrêter les services
```bash
docker-compose down
```

### Voir les logs
```bash
# Tous les services
docker-compose logs -f

# Service GLPI uniquement
docker-compose logs -f glpi

# Service base de données uniquement
docker-compose logs -f db
```

### Redémarrer un service
```bash
# Redémarrer GLPI
docker-compose restart glpi

# Redémarrer la base de données
docker-compose restart db
```

### Accéder au conteneur GLPI
```bash
docker-compose exec glpi bash
```

### Accéder à la base de données
```bash
docker-compose exec db mysql -u glpi_app -p glpi_mediashcool
# Mot de passe : huieznji238U493Nncd!?QSKSO
```

## 🔄 Mise à jour

Pour mettre à jour GLPI vers la dernière version :

```bash
docker-compose pull
docker-compose up -d
```

## 📂 Données persistantes

Les données suivantes sont stockées dans le dossier `storage/` et persisteront même après la suppression des conteneurs :

- **`storage/glpi/`** : Configuration, fichiers, logs GLPI
- **`storage/mysql/`** : Base de données MariaDB

## ⚠️ Dépannage

### GLPI ne se charge pas
- Vérifiez que le port 80 n'est pas utilisé : `sudo netstat -tlnp | grep :80`
- Vérifiez les logs : `docker-compose logs glpi`

### Erreur de base de données
- Vérifiez que le service db est démarré : `docker-compose ps`
- Vérifiez les logs de la DB : `docker-compose logs db`

### Problèmes de permissions
```bash
sudo chown -R 33:33 storage/glpi/
sudo chmod -R 755 storage/glpi/
```

## 🛡️ Sécurité

Pour un environnement de production :

1. Changez tous les mots de passe par défaut
2. Utilisez des mots de passe complexes
3. Configurez HTTPS
4. Limitez l'accès réseau si nécessaire

## 📞 Support

Pour toute question ou problème :
- Consultez la documentation officielle GLPI : https://glpi-project.org/
- Vérifiez les logs avec `docker-compose logs`

---

*Ce projet est configuré pour faciliter le déploiement en formation. Les données et la configuration sont pré-configurées pour un usage pédagogique.*