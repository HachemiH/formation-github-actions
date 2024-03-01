# Module 5.2 : Utilisation des Variables d'Environnement dans GitHub Actions

<blockquote>
  <h2>Prérequis</h2>
  <p>Avant de plonger dans ce module, il est recommandé que vous ayez :</p>
  <ul>
    <li>Une compréhension solide de l'utilisation de GitHub et des principes fondamentaux des GitHub Actions.</li>
    <li>Des connaissances de base sur les serveurs VPS et les processus de déploiement d'applications web.</li>
    <li>Une familiarité avec l'utilisation des variables d'environnement dans le développement logiciel pour la gestion de configurations.</li>
  </ul>
</blockquote>

<blockquote>
  <h2>Objectifs Pédagogiques</h2>
  <p>À l'issue de ce module, vous serez capable de :</p>
  <ul>
    <li>Discerner les différents niveaux auxquels les variables d'environnement peuvent être définies dans GitHub Actions et leur utilisation optimale.</li>
    <li>Illustrer l'application pratique des variables d'environnement pour orchestrer la configuration de déploiement d'une application web sur un VPS de manière sécurisée.</li>
    <li>Implémenter des pratiques de sécurisation pour les variables d'environnement contenant des informations sensibles au sein de vos workflows GitHub Actions.</li>
  </ul>
</blockquote>

---

Les variables d'environnement jouent un rôle crucial dans les workflows CI/CD en permettant la personnalisation des opérations sans modifier le code source. Elles sont particulièrement utiles pour gérer des configurations spécifiques à l'environnement, telles que des URL de base, des clés d'API, ou des configurations de connexion à des bases de données, qui peuvent varier entre les environnements de développement, de test, et de production.

## 5.2.1 Où sont Stockées les Variables d'Environnement ?

Dans GitHub Actions, les variables d'environnement peuvent être définies à plusieurs niveaux :

- **Dans le fichier de workflow (`*.yml`)** : Directement dans le code YAML, permettant une utilisation spécifique à un job ou à une étape.
- **Dans les paramètres du dépôt GitHub** : Sous l'onglet "Settings" du dépôt, puis "Secrets and variables" > "Environment secrets", où elles peuvent être associées à des environnements spécifiques.
- **Au niveau de l'organisation** : Pour les variables partagées entre plusieurs dépôts au sein d'une organisation.

## 5.2.2 Exemple Pratique : Déploiement d'une Application Web sur un VPS

Imaginons une application web Node.js que vous souhaitez déployer automatiquement sur un VPS chaque fois que vous poussez du code sur la branche principale de votre dépôt GitHub.

### Définition des Variables d'Environnement

Vous avez besoin de définir plusieurs variables d'environnement pour gérer la configuration de votre application et la connexion à votre VPS :

- `NODE_ENV`: Indique l'environnement d'exécution de l'application (par exemple, `production`).
- `DATABASE_URL`: L'URL de connexion à la base de données de votre application.
- `VPS_HOST`: L'adresse IP ou le nom de domaine de votre VPS.
- `VPS_USERNAME`: Le nom d'utilisateur pour la connexion SSH à votre VPS.

### Configuration dans GitHub Actions

```yaml
name: Deploy Web Application

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest
    env:
      NODE_ENV: production
    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Set up Node.js
        uses: actions/setup-node@v2
        with:
          node-version: '14'

      - name: Install dependencies
        run: npm install

      - name: Build
        run: npm run build
        env:
          DATABASE_URL: ${{ secrets.DATABASE_URL }}

      - name: Deploy to VPS
        uses: appleboy/ssh-action@master
        with:
          host: ${{ secrets.VPS_HOST }}
          username: ${{ secrets.VPS_USERNAME }}
          key: ${{ secrets.SSH_PRIVATE_KEY }}
          script: |
            cd /path/to/your/app
            git pull
            npm install --production
            pm2 restart all
```

### Explication

- **Variables d'Environnement au Niveau Job** : `NODE_ENV` est définie pour tout le job, indiquant que l'application doit s'exécuter en mode production.
- **Variables d'Environnement au Niveau Étape** : `DATABASE_URL` est utilisée uniquement lors de la construction de l'application, garantissant que l'accès à la base de données est sécurisé.
- **Utilisation des Secrets** : `VPS_HOST`, `VPS_USERNAME`, et `SSH_PRIVATE_KEY` sont stockés comme secrets et utilisés pour établir une connexion sécurisée au VPS pour le déploiement.


## Résumé

Les variables d'environnement constituent un pilier dans la configuration des workflows CI/CD sur GitHub Actions, offrant une méthode sécurisée et flexible pour gérer des informations de configuration spécifiques aux environnements de développement, de test, et de production. 

- **Stockage et Application** : Vous avez appris que les variables d'environnement peuvent être configurées à différents niveaux, y compris directement dans les fichiers de workflow YAML, au niveau des secrets de dépôt pour une utilisation transversale, ou même au niveau de l'organisation pour un partage entre plusieurs dépôts.

- **Exemple d'Utilisation** : À travers un scénario pratique, vous avez vu comment déployer une application web Node.js sur un VPS en utilisant des variables d'environnement pour gérer des aspects critiques tels que les configurations de l'environnement d'exécution, la connexion à la base de données, et les détails de la connexion SSH au VPS.

- **Bonnes Pratiques** : Enfin, ce module a souligné l'importance de sécuriser les variables d'environnement, en particulier celles contenant des données sensibles, en les déclarant comme secrets et en limitant leur portée d'utilisation aux étapes spécifiques du workflow où elles sont nécessaires.

