# FAQ pour l'Installation et l'Utilisation de SonarQube

## Problèmes d'Installation

### Q: Que faire si SonarQube ne démarre pas après l'exécution de `docker-compose up` ?
**R:** Vérifiez les logs de Docker pour identifier le problème spécifique. Vous pouvez consulter les logs avec la commande:
```bash
docker logs sonarqube
```
Vérifiez les messages d'erreur. Souvent, les problèmes sont liés à des configurations insuffisantes de ressources, comme la mémoire.

### Q: Comment résoudre les erreurs de mémoire insuffisante pour SonarQube ?
**R:** SonarQube nécessite au moins 2GB de RAM pour fonctionner correctement. Si vous êtes sur Docker Desktop, augmentez la mémoire allouée à Docker via les préférences de Docker Desktop. Pour les systèmes Linux, assurez-vous que votre machine a suffisamment de RAM disponible.

### Q: Que faire si le port 9000 est déjà utilisé ?
**R:** Changez le port dans le fichier `docker-compose.yml`. Modifiez la ligne des ports pour utiliser un autre port libre sur votre machine:
```yaml
ports:
  - "9001:9000"
```
Après modification, redémarrez SonarQube avec `docker-compose up -d`.

## Problèmes de Configuration

### Q: Comment configurer SonarQube pour utiliser une base de données externe ?
**R:** Vous pouvez modifier le fichier `docker-compose.yml` pour connecter SonarQube à une base de données externe. Remplacez les variables d'environnement sous le service SonarQube par les détails de votre base de données :
```yaml
environment:
  - SONAR_JDBC_URL=jdbc:postgresql://host:port/database
  - SONAR_JDBC_USERNAME=username
  - SONAR_JDBC_PASSWORD=password
```
N'oubliez pas de retirer ou commenter le service de base de données intégré si vous ne l'utilisez pas.

### Q: Comment réinitialiser le mot de passe administrateur par défaut ?
**R:** Si vous pouvez accéder à la console d'administration, changez le mot de passe dans **Administration > Security > Users**. Si vous êtes bloqué, une réinstallation pourrait être nécessaire, ou vous pourriez modifier le mot de passe directement dans la base de données, ce qui est plus complexe et nécessite des compétences en base de données.

## Problèmes Divers

### Q: Comment mettre à jour SonarQube vers une nouvelle version ?
**R:** Pour mettre à jour SonarQube, modifiez la version de l'image dans votre fichier `docker-compose.yml` :
```yaml
image: sonarqube:latest
```
Changez "latest" par la nouvelle version désirée. Ensuite, exécutez :
```bash
docker-compose down
docker-compose pull
docker-compose up -d
```
Assurez-vous de sauvegarder vos données avant de faire une mise à jour.

### Q: Comment installer des plugins supplémentaires dans SonarQube ?
**R:** Vous pouvez installer des plugins via le Marketplace dans l'interface web de SonarQube sous **Administration > Marketplace**. Si vous avez besoin d'installer manuellement, placez les fichiers JAR des plugins dans le volume de plugins que vous avez configuré et redémarrez SonarQube.
