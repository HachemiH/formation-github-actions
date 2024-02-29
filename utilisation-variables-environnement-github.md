# 5.2. Utilisation des Variables d'Environnement dans GitHub Actions

<blockquote>
  <h2>Objectifs Pédagogiques</h2>
  <p>À la fin de ce module, l'apprenant sera en mesure de :</p>
  <ul>
    <li>Identifier les différents niveaux où les variables d'environnement peuvent être définies et utilisées dans GitHub Actions.</li>
    <li>Comprendre comment et pourquoi utiliser les variables d'environnement pour gérer la configuration de déploiement d'une application web sur un VPS.</li>
    <li>Appliquer les meilleures pratiques pour sécuriser les variables d'environnement contenant des données sensibles.</li>
  </ul>
</blockquote>
<blockquote>
  <h2>Prérequis</h2>
  <p>Pour une compréhension optimale de ce module, les apprenants devraient posséder :</p>
  <ul>
    <li>Une compréhension de base de l'utilisation de GitHub et des principes de GitHub Actions.</li>
    <li>Des connaissances élémentaires sur les serveurs VPS et le processus de déploiement d'applications web.</li>
    <li>Une familiarité avec la notion de variables d'environnement et leur utilité dans le développement logiciel.</li>
  </ul>
</blockquote>


Les variables d'environnement jouent un rôle crucial dans les workflows CI/CD en permettant la personnalisation des opérations sans modifier le code source. Elles sont particulièrement utiles pour gérer des configurations spécifiques à l'environnement, telles que des URL de base, des clés d'API, ou des configurations de connexion à des bases de données, qui peuvent varier entre les environnements de développement, de test, et de production.

## Où sont Stockées les Variables d'Environnement ?

Dans GitHub Actions, les variables d'environnement peuvent être définies à plusieurs niveaux :

- **Dans le fichier de workflow (`*.yml`)** : Directement dans le code YAML, permettant une utilisation spécifique à un job ou à une étape.
- **Dans les paramètres du dépôt GitHub** : Sous l'onglet "Settings" du dépôt, puis "Secrets and variables" > "Environment secrets", où elles peuvent être associées à des environnements spécifiques.
- **Au niveau de l'organisation** : Pour les variables partagées entre plusieurs dépôts au sein d'une organisation.

## Exemple Pratique : Déploiement d'une Application Web sur un VPS

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

L'utilisation de variables d'environnement dans GitHub Actions offre une flexibilité et une sécurité essentielles lors du déploiement d'applications dans différents environnements. En les définissant à différents niveaux et en combinant leur utilisation avec des secrets pour les données sensibles, vous pouvez créer des workflows CI/CD robustes et sécurisés adaptés à vos besoins spécifiques de déploiement.


