
## Accès à SonarQube

- **Ouvrir un navigateur** et accéder à [http://localhost:9000](http://localhost:9000).
- **Se connecter** avec les identifiants par défaut : `admin` pour le nom d'utilisateur et `admin` pour le mot de passe.

## Configurer votre premier projet

1. **Créer un projet** : Suivez les instructions sur l'écran d'accueil pour créer un nouveau projet.
2. **Générer un token** : Créez un token d'authentification lorsque vous configurez votre projet. Ce token sera utilisé par SonarScanner pour envoyer les analyses à SonarQube.
3. **Configurer SonarScanner** : Configurez SonarScanner sur votre machine de développement ou utilisez le scanner intégré dans votre IDE.

### Exemple de Configuration pour SonarScanner

Dans votre projet, créez un fichier `sonar-project.properties` avec le contenu suivant :

```properties
sonar.projectKey=mon_projet
sonar.host.url=http://localhost:9000
sonar.login=<le_token_d'authentification_généré>
```

## Lancer une Analyse

- **Exécutez SonarScanner** depuis la racine de votre projet :

```bash
sonar-scanner
```

## Vérifier les Résultats

- Retournez à l'interface web de SonarQube pour voir les résultats de votre analyse.
- Explorez les problèmes détectés et travaillez à leur résolution pour améliorer la qualité de votre code.

