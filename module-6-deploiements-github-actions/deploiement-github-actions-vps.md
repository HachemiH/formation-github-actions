# 6.2 Déploiement Direct sur VPS

<blockquote>
  <h2>Objectifs Pédagogiques</h2>
  <p>À la fin de ce module, vous serez en mesure de :</p>
  <ul>
    <li>Configurer un VPS pour recevoir des déploiements automatiques via GitHub Actions.</li>
    <li>Stocker et utiliser de manière sécurisée des informations sensibles avec les secrets GitHub.</li>
    <li>Créer un workflow GitHub Actions pour automatiser le déploiement de votre application web sur un VPS.</li>
    <li>Appliquer des pratiques de sécurité de base pour sécuriser votre déploiement.</li>
  </ul>
</blockquote>

<blockquote>
  <h2>Prérequis</h2>
  <p>Pour suivre ce module, vous devriez avoir :</p>
  <ul>
    <li>Une connaissance de base des workflows GitHub Actions.</li>
    <li>Un accès à un VPS avec SSH configuré.</li>
    <li>Une compréhension élémentaire des opérations de base du serveur, comme la gestion de services et l'utilisation de SSH.</li>
    <li>Une familiarité avec les concepts de CI/CD.</li>
  </ul>
</blockquote>

## Application Pratique : Déploiement Direct sur VPS

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

### Bonnes Pratiques de Sécurité

- **Clés SSH** : Utilisez une paire de clés SSH dédiée pour le déploiement automatique et limitez ses permissions autant que possible.
- **Ports SSH** : Changez le port SSH par défaut pour réduire le risque d'attaques automatisées.
- **Surveillance** : Mettez en place un système de surveillance pour votre application afin de détecter et de répondre rapidement à tout problème post-déploiement.

## Résumé

Le déploiement direct sur un VPS via GitHub Actions offre une méthode simple et efficace pour automatiser la mise en production de vos applications web. En suivant les étapes décrites dans ce module, vous pouvez configurer un workflow sécurisé qui facilite le déploiement continu sans nécessiter d'infrastructure complexe. Ce module souligne l'importance de la sécurité et de la préparation dans le processus de déploiement, garantissant que vos déploiements sont à la fois rapides et sûrs.


