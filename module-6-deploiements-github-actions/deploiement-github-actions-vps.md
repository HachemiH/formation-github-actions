# Module 6.2 : Déploiement Direct sur VPS

<blockquote>
  <h2>Prérequis</h2>
  <p>Pour optimiser votre apprentissage dans ce module, il est recommandé d'avoir :</p>
  <ul>
    <li>Une base solide dans la création et la gestion des workflows GitHub Actions.</li>
    <li>Un accès à un VPS configuré pour les connexions SSH.</li>
    <li>Une connaissance des opérations serveur de base, y compris la gestion des services et l'utilisation de SSH.</li>
    <li>Une familiarité avec les principes de CI/CD pour le déploiement d'applications.</li>
  </ul>
</blockquote>

<blockquote>
  <h2>Objectifs Pédagogiques</h2>
  <p>À la fin de ce module, vous serez en mesure de :</p>
  <ul>
    <li>Configurer un VPS pour recevoir des déploiements automatiques via GitHub Actions.</li>
    <li>Gérer de manière sécurisée des informations sensibles telles que les clés SSH en utilisant les secrets GitHub.</li>
    <li>Développer un workflow GitHub Actions pour automatiser le déploiement de votre application web sur un VPS.</li>
    <li>Implémenter des mesures de sécurité fondamentales pour protéger votre déploiement.</li>
  </ul>
</blockquote>

---

## 6.2.1 Application Pratique : Déploiement Direct sur VPS

Le déploiement direct sur un VPS est une stratégie efficace pour les développeurs et les petites équipes visant à simplifier le processus de mise en production. Voici comment mettre en œuvre cette stratégie :

### 1. Préparez votre VPS

- **Configuration SSH** : Assurez-vous que SSH est configuré sur votre VPS. Cela inclut la génération d'une paire de clés SSH et l'ajout de la clé publique au fichier `~/.ssh/authorized_keys` sur le serveur.
- **Sécurité** : Modifiez le port SSH par défaut et configurez Fail2Ban pour renforcer la sécurité de votre serveur.

### 2. Configurez les Secrets GitHub

- Stockez la clé SSH privée, l'adresse du serveur (HOST), et les autres informations sensibles comme des secrets dans votre dépôt GitHub pour les utiliser de manière sécurisée dans votre workflow.

### 3. Créez le Workflow GitHub Actions

```yaml
name: Déploiement Simple sur VPS

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Déploiement sur VPS
        uses: appleboy/ssh-action@master
        with:
          host: ${{ secrets.HOST }}
          username: ${{ secrets.USERNAME }}
          key: ${{ secrets.SSH_KEY }}
          script: |
            cd /var/www/monapp
            git pull origin main
            npm install
            npm run build
            pm2 restart all
```

Ce workflow assure que chaque push sur la branche `main` déclenche une série d'actions automatisées pour mettre à jour votre application sur le VPS.

## 6.2.2 Bonnes Pratiques de Sécurité

- **Clés SSH** : Utilisez une paire de clés SSH dédiée pour le déploiement automatique et limitez ses permissions autant que possible.
- **Ports SSH** : Changez le port SSH par défaut pour réduire le risque d'attaques automatisées.
- **Surveillance** : Mettez en place un système de surveillance pour votre application afin de détecter et de répondre rapidement à tout problème post-déploiement.


## Résumé

Ce module vous a guidé à travers l'établissement d'un pipeline de déploiement direct sur un VPS, en utilisant GitHub Actions pour automatiser et sécuriser le processus. Les étapes clés comprennent :

1. **Préparation de votre VPS** : Configuration de SSH et renforcement de la sécurité de votre serveur pour préparer le terrain à un déploiement sécurisé.

2. **Configuration des Secrets GitHub** : Sécurisation des informations sensibles telles que la clé SSH privée et les détails de connexion au serveur, en les stockant comme secrets dans votre dépôt GitHub.

3. **Création du Workflow GitHub Actions** : Mise en place d'un workflow automatisé qui exécute le déploiement à chaque push sur la branche `main`, détaillant les actions nécessaires pour mettre à jour votre application sur le VPS.

4. **Adoption de Bonnes Pratiques de Sécurité** : Application de mesures de sécurité telles que l'utilisation de clés SSH dédiées, le changement du port SSH par défaut, et la mise en place d'une surveillance pour votre application post-déploiement.

