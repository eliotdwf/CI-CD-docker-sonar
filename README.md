# BobApp

[Last build test coverage](https://jeanungerer.github.io/Gerez-un-projet-collaboratif-en-int-grant-une-demarche-CI-CD/)

Clone project:

> git clone XXXXX

## Front-end 

Go inside folder the front folder:

> cd front

Install dependencies:

> npm install

Launch Front-end:

> npm run start;

### Docker

Build the container:

> docker build -t bobapp-front .  

Start the container:

> docker run -p 8080:8080 --name bobapp-front -d bobapp-front

## Back-end

Go inside folder the back folder:

> cd back

Install dependencies:

> mvn clean install

Launch Back-end:

>  mvn spring-boot:run

Launch the tests:

> mvn clean install

### Docker

Build the container:

> docker build -t bobapp-back .  

Start the container:

> docker run -p 8080:8080 --name bobapp-back -d bobapp-back



# Document explicatif sur les GitHub Actions mises en place.

## Introduction
Ce document a pour but de détailler les étapes mises en œuvre dans les GitHub Actions, de proposer des indicateurs de performance clés (KPI) et d'analyser les métriques ainsi que les avis des utilisateurs concernant le projet.

## Workflows GitHub Actions

### Workflow de Build & Test Backend
- **Description** : Ce workflow construit et teste le backend du projet.
- **Étapes impliquées** :
  1. **Déclencheurs** : 
     - workflow_dispatch pour un déclenchement manuel.
     - push sur la branche main pour les changements dans le répertoire back/**.
     - pull_request pour les demandes de tirage sur la branche main.
  2. **Checkout du code** : Utilisation de actions/checkout@v4 pour cloner le dépôt.
  3. **Installation des dépendances** : Utilisation de mvn clean install pour installer les paquets Maven.
  4. **Exécution des tests** : Utilisation de mvn clean test pour exécuter les tests.
  5. **Génération des rapports** : Utilisation de mvn jacoco:report pour créer un rapport de couverture de code.
  6. **Commit des résultats dans une branche** : Ajout et commit des rapports générés dans la branche test-result.

### Workflow de Build & Test Frontend
- **Description** : Ce workflow construit et teste le frontend du projet.
- **Étapes impliquées** :
  1. **Déclencheurs** : 
     - workflow_dispatch pour un déclenchement manuel.
     - push sur la branche main pour les changements dans le répertoire front/**.
     - pull_request pour les demandes de tirage sur la branche main.
  2. **Checkout du code** : Utilisation de actions/checkout@v4 pour cloner le dépôt.
  3. **Installation des dépendances** : Utilisation de npm install pour installer les paquets.
  4. **Construction et exécution des tests** : Utilisation de npm run build et npm run test:prod.
  5. **Génération des rapports de couverture de code** : Utilisation de actions/upload-artifact@v4 pour télécharger les rapports générés.
  6. **Commit des résultats dans une branche** : Ajout et commit des rapports générés dans la branche test-result.

### Workflow d'Analyse de la Qualité du Code
- **Description** : Ce workflow exécute des analyses de qualité du code à l'aide de SonarCloud pour le backend et le frontend.
- **Étapes impliquées** :
  1. **Déclencheurs** : Déclenché sur push et pull_request pour les répertoires back/** et front/**.
  2. **Configuration de l'environnement JDK et Node.js** : Installation des versions appropriées.
  3. **Analyse avec SonarCloud** : Utilisation des plugins Maven et des actions SonarCloud pour l'analyse.
  4. **Téléchargement des rapports SonarQube** : Utilisation de actions/upload-artifact@v4 pour stocker les rapports d'analyse.

### Workflow CI d'Image Docker
- **Description** : Ce workflow construit et pousse des images Docker pour le backend et le frontend.
- **Étapes impliquées** :
  1. **Déclencheurs** : Déclenché sur push et pull_request pour les répertoires back/** et front/**.
  2. **Login à Docker Hub** : Authentification avec le nom d'utilisateur et le mot de passe.
  3. **Construction et poussée des images Docker** : Construction des images et poussée vers Docker Hub.

### pages-build-deployment
- **Description** : Ce workflow construit une page web à partir du readme de la branche test result pour fournir un espace pour suivre les derniers resultats de tests.

## Indicateurs de Performance Clés (KPI)
- **Définition des KPI** : 
  - Taux de réussite des builds.
  - Couverture des tests (pourcentage de code couvert par les tests).
  - Fréquence des déploiements.
  - Temps de construction.
  - Temps attribué au suivi des pull request et maintien des version sur dockerhub.

## Analyse des Métriques
- **Collecte des Métriques** : Les métriques sont collectées à partir des résultats des workflows GitHub Actions.
- **Interprétation des Métriques** : 
  - Suivi des tendances au fil du temps.
  - Identification des points faibles et des succès.
- **Aperçus** : Améliorations possibles dans le processus de développement.

## Analyse des Avis des Utilisateurs
- **Résumé des Avis des Utilisateurs** : 
  - Retours positifs sur la rapidité des tests.
  - Suggestions pour améliorer la documentation.
- **Augmentation du nombres de personnes impliqués et de leur qualité de code.** 

## Conclusion
Ce document présente un aperçu complet des étapes mises en œuvre dans les workflows GitHub Actions, des KPI proposés, ainsi que l'analyse des métriques et des avis des utilisateurs.
