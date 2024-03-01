# 6.3 Intégration avec Docker

<blockquote>
  <h2>Objectifs Pédagogiques</h2>
  <p>À la fin de ce module, vous serez en mesure de :</p>
  <ul>
    <li>Comprendre les avantages d'utiliser Docker dans le cadre de GitHub Actions pour le déploiement.</li>
    <li>Configurer un workflow GitHub Actions qui utilise Docker pour construire et déployer des applications.</li>
    <li>Appliquer des pratiques de sécurité pour le déploiement de conteneurs Docker via GitHub Actions.</li>
  </ul>
</blockquote>

<blockquote>
  <h2>Prérequis</h2>
  <p>Pour suivre ce module, vous devriez avoir :</p>
  <ul>
    <li>Une compréhension de base de Docker et des conteneurs.</li>
    <li>Une familiarité avec les workflows GitHub Actions.</li>
    <li>Des connaissances de base sur les serveurs et le déploiement d'applications.</li>
  </ul>
</blockquote>

## Introduction

Docker est devenu un outil incontournable pour le développement, le test, et le déploiement d'applications en fournissant un environnement isolé et reproductible. L'intégration de Docker dans les workflows GitHub Actions simplifie le processus de CI/CD en permettant la construction, le test, et le déploiement uniformes des applications, indépendamment de l'environnement.

## Configuration d'un Workflow Docker avec GitHub Actions

L'utilisation de Docker dans un workflow GitHub Actions se fait généralement en deux phases : la construction de l'image Docker et son déploiement.

### Construction de l'Image Docker

1. **Définir un Dockerfile** : Commencez par créer un Dockerfile dans votre projet, décrivant l'environnement d'exécution de votre application.

2. **Construire l'Image dans GitHub Actions** :
   - Utilisez une étape dans votre workflow pour construire l'image Docker à partir de votre Dockerfile, en utilisant la commande `docker build`.

### Déploiement de l'Image Docker

1. **Push de l'Image sur un Registry** : Après la construction, poussez l'image sur Docker Hub ou un autre registry Docker, en utilisant `docker push`.

2. **Déploiement sur le Serveur** :
   - Configurez votre serveur pour tirer et exécuter l'image Docker mise à jour, en utilisant des secrets GitHub pour stocker de manière sécurisée les informations d'authentification du registry.

### Exemple de Workflow

```yaml
name: CI/CD avec Docker

on:
  push:
    branches:
      - main

jobs:
  build-and-push:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v2
      
      - name: Build Docker image
        run: docker build . -t monapp:latest
      
      - name: Push to Docker Hub
        run: |
          echo ${{ secrets.DOCKER_PASSWORD }} | docker login -u ${{ secrets.DOCKER_USERNAME }} --password-stdin
          docker push monapp:latest
```

La commande de run effectue deux opérations principales :

1. **Login au Docker Hub** : Utilise `echo` pour passer le mot de passe Docker au client Docker via `stdin`, en utilisant l'option `--password-stdin`. Cela permet une connexion sécurisée sans avoir besoin d'écrire le mot de passe en clair dans le script. Les valeurs `${{ secrets.DOCKER_USERNAME }}` et `${{ secrets.DOCKER_PASSWORD }}` sont des variables d'environnement qui doivent être définies dans les secrets de votre dépôt GitHub. Elles contiennent respectivement votre nom d'utilisateur et votre mot de passe pour Docker Hub.

2. **Push de l'Image Docker** : Après une connexion réussie, l'image Docker est poussée vers votre compte sur Docker Hub avec `docker push monapp:latest`. Le tag `latest` est utilisé ici à titre d'exemple ; dans un cas d'utilisation réel, il est recommandé de gérer les versions de votre image avec des tags plus spécifiques pour mieux contrôler les déploiements.

Assurez-vous que les secrets `DOCKER_USERNAME` et `DOCKER_PASSWORD` sont bien configurés dans les paramètres de votre dépôt GitHub pour que ces commandes fonctionnent correctement. Cette approche renforce la sécurité de votre workflow en évitant l'exposition de vos identifiants Docker Hub.


### Bonnes Pratiques

- **Sécurisez vos Secrets** : Stockez toujours les informations d'authentification du registry Docker comme des secrets GitHub.
- **Gestion des Tags d'Image** : Utilisez des tags d'image pour gérer différentes versions de votre application.
- **Automatisez les Tests** : Intégrez des tests dans votre workflow avant de construire et de déployer l'image Docker, pour assurer la qualité du code.

## Résumé

Dans ce module, nous avons couvert l'intégration de Docker dans vos workflows GitHub Actions pour le déploiement d'applications. Voici les étapes clés à retenir :

1. **Préparation** : Commencez par créer un `Dockerfile` dans votre projet qui décrit l'environnement d'exécution de votre application.

2. **Sécurité** : Configurez les secrets GitHub (`DOCKER_USERNAME` et `DOCKER_PASSWORD`) pour stocker de manière sécurisée vos identifiants Docker Hub.

3. **Workflow GitHub Actions** :
   - **Étape 1** : Utilisez `actions/checkout@v2` pour extraire le code de votre dépôt.
   - **Étape 2** : Construisez votre image Docker en utilisant `docker build`.
   - **Étape 3** : Connectez-vous à Docker Hub avec `docker login` en utilisant les secrets GitHub pour vos identifiants.
   - **Étape 4** : Poussez l'image construite vers Docker Hub avec `docker push`.

4. **Déploiement** : En option, déployez l'image Docker sur votre serveur ou plateforme d'hébergement en exécutant les commandes nécessaires via SSH ou tout autre mécanisme d'orchestration de conteneurs.

5. **Bonnes Pratiques** :
   - Assurez la sécurité de vos informations d'identification en utilisant des secrets GitHub.
   - Utilisez des tags d'image pour gérer les versions de votre application.
   - Intégrez des tests automatiques dans votre workflow pour maintenir la qualité du code.

Ce résumé fournit une structure simple pour revoir rapidement les concepts clés et les étapes impliquées dans l'intégration de Docker avec GitHub Actions pour le déploiement d'applications.
