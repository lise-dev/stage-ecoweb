Pour installer et configurer un environnement SonarQube avec le plugin ecoCode sur Ubuntu, macOS, et Windows à l'aide de Docker et Docker Compose, suivez ce guide complet. Cela inclut la configuration de la base de données avec PostgreSQL et l'installation manuelle du plugin ecoCode.

## Guide d'Installation Complet de SonarQube avec ecoCode Plugin

### Prérequis

- Docker et Docker Compose installés sur votre machine.

### 1. Création du fichier `docker-compose.yml`

Créez un fichier `docker-compose.yml` pour définir les services nécessaires (SonarQube et PostgreSQL). Enregistrez ce fichier dans votre répertoire de travail.

```yaml
version: '3.7'

services:
  db:
    image: postgres:12-alpine
    container_name: postgresql_sonar
    environment:
      POSTGRES_USER: sonar
      POSTGRES_PASSWORD: sonar
      POSTGRES_DB: sonarqube
    volumes:
      - postgresql_data:/var/lib/postgresql/data

  sonarqube:
    image: sonarqube:latest
    container_name: sonarqube
    depends_on:
      - db
    environment:
      - SONAR_JDBC_URL=jdbc:postgresql://db:5432/sonarqube
      - SONAR_JDBC_USERNAME=sonar
      - SONAR_JDBC_PASSWORD=sonar
    ports:
      - "9000:9000"
    volumes:
      - sonarqube_data:/opt/sonarqube/data
      - sonarqube_logs:/opt/sonarqube/logs
      - sonarqube_extensions:/opt/sonarqube/extensions

volumes:
  postgresql_data:
  sonarqube_data:
  sonarqube_logs:
  sonarqube_extensions:
```

### 2. Lancement de SonarQube et PostgreSQL

Dans le terminal, naviguez vers le dossier contenant votre fichier `docker-compose.yml`. Exécutez la commande suivante pour démarrer les services :

```bash
docker-compose up -d
```

### 3. Téléchargement et Installation Manuelle du Plugin ecoCode

1. **Téléchargez le Plugin ecoCode** :
   - Rendez-vous sur le site officiel ou la source de téléchargement du plugin ecoCode et téléchargez le fichier JAR correspondant à votre version de SonarQube.

2. **Installez le Plugin dans SonarQube** :
   - Copiez le fichier JAR téléchargé dans le dossier des extensions de SonarQube. Vous pouvez le faire en accédant au conteneur SonarQube ou en localisant le volume approprié si vous utilisez Docker.
   ```bash
   docker cp ecoCode-plugin.jar sonarqube:/opt/sonarqube/extensions/plugins/
   ```

3. **Redémarrez SonarQube** :
   - Pour activer le plugin, redémarrez SonarQube. Cela peut être fait en redémarrant le conteneur Docker.
   ```bash
   docker-compose restart sonarqube
   ```

### 4. Configuration de SonarQube

Après le redémarrage, connectez-vous à l'interface web de SonarQube à `http://localhost:9000` avec le nom d'utilisateur et le mot de passe par défaut (`admin/admin`). Changez le mot de passe lors de la première connexion.

### 5. Vérification et Utilisation

- **Vérifiez l'Installation du Plugin** :
  - Allez à **Administration > Marketplace > Installed** pour confirmer que le plugin ecoCode est correctement installé.
  
- **Configurez et utilisez SonarQube** :
  - Créez des projets, configurez des analyses, et inspectez les résultats pour évaluer la qualité du code à l'aide du nouveau plugin.

