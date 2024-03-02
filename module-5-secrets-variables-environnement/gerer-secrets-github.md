# Module 5.1 : Gérer les Secrets dans GitHub

<blockquote>
  <h2>Prérequis</h2>
  <p>Pour aborder efficacement ce chapitre, vous devriez avoir :</p>
  <ul>
    <li>Une connaissance de base de l'utilisation de GitHub et une compréhension initiale des workflows GitHub Actions.</li>
    <li>Une compréhension élémentaire des principes de sécurité, tels que la connexion sécurisée via SSH, et de l'importance de protéger les informations sensibles.</li>
    <li>Des notions de base sur les serveurs VPS et leur gestion.</li>
  </ul>
</blockquote>

<blockquote>
  <h2>Objectifs Pédagogiques</h2>
  <p>À la fin de ce chapitre, vous serez capable de :</p>
  <ul>
    <li>Identifier ce que sont les secrets dans le contexte des workflows GitHub Actions et comprendre leur importance pour sécuriser les pipelines CI/CD.</li>
    <li>Démontrer la capacité à ajouter, modifier, et gérer efficacement les secrets au sein de GitHub pour sécuriser les données sensibles utilisées dans les workflows.</li>
    <li>Appliquer les secrets de manière pratique dans les workflows GitHub Actions pour sécuriser les interactions avec un serveur VPS, notamment pour les déploiements.</li>
  </ul>
</blockquote>

---

La gestion des secrets est cruciale dans les workflows d'intégration et de déploiement continus (CI/CD), particulièrement lorsqu'il s'agit d'automatiser des interactions avec des systèmes externes comme les serveurs VPS. Les secrets permettent de stocker et d'utiliser des données sensibles de manière sécurisée, sans les exposer dans le code ou les logs de build.

## 5.1.1 Découverte des Secrets

### Qu'est-ce qu'un Secret ?

Un secret dans GitHub est une donnée sensible que vous souhaitez garder privée, telle qu'un mot de passe, un jeton d'accès, une clé SSH, ou toute autre information confidentielle requise par votre workflow CI/CD.

### Pourquoi Utiliser des Secrets ?

Les secrets sont utilisés pour :

- Protéger vos données sensibles contre les expositions accidentelles.
- Séparer les informations de configuration du code source, conformément aux meilleures pratiques de sécurité.
- Permettre une modification et gestion centralisées des données d'accès sans nécessiter de changer le code source ou les workflows.

## 5.1.2 Exemple Pratique : Utilisation d'un Secret avec un VPS

Imaginons que vous souhaitiez déployer votre application sur un VPS via SSH en utilisant GitHub Actions. Voici comment procéder :

### Configuration des Secrets

- `SSH_KEY` : Votre clé privée SSH, utilisée pour établir une connexion sécurisée au VPS sans exposer votre mot de passe.
- `VPS_HOST` : L'adresse de votre serveur VPS, permettant à GitHub Actions de savoir où se connecter.


# Fichier de Workflow 

```yaml
name: Deploy to VPS

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v2
      
      - name: SSH and Deploy
        uses: appleboy/ssh-action@master
        with:
          host: ${{ secrets.VPS_HOST }}
          username: "votre_user"
          key: ${{ secrets.SSH_KEY }}
          script: |
            cd /path/to/your/app
            git pull
            ./deploy.sh
```

Ce fichier de workflow GitHub Actions définit un processus automatique pour déployer une application sur un VPS chaque fois qu'un push est effectué sur la branche `main`.

## 5.1.3 Qu'est-ce qu'Appleboy/ssh-action ?

`appleboy/ssh-action` est une action GitHub qui permet d'établir une connexion SSH à un serveur distant directement depuis un workflow GitHub Actions. Cette action simplifie l'exécution de commandes SSH sur un serveur distant, ce qui est idéal pour déployer des applications, exécuter des scripts, ou effectuer des tâches de maintenance à distance.

- **Avantages :**
  - Automatisation du déploiement : Permet de déployer automatiquement votre application sur un serveur distant après chaque push, réduisant le risque d'erreurs humaines et accélérant le processus de déploiement.
  - Sécurité : Utilise des secrets GitHub pour gérer les informations d'identification, assurant que les données sensibles restent sécurisées.

## 5.1.4 Le Script `deploy.sh`

Le `deploy.sh` mentionné dans l'exemple de workflow est un script shell que vous devriez avoir sur votre VPS. Ce script contient les commandes nécessaires pour déployer ou mettre à jour votre application sur le serveur. L'utilisation d'un script de déploiement permet de centraliser et de standardiser le processus de déploiement, garantissant que toutes les étapes nécessaires sont exécutées de manière cohérente.

**Une explication et un exemple de ce `deploy.sh` se trouve plus loin dans cette page.**

- **Fonctions typiques de `deploy.sh` :**
  - Arrêt de l'ancienne version de l'application (si nécessaire).
  - Mise à jour des fichiers de l'application, souvent en utilisant `git pull` pour récupérer la dernière version du code depuis un dépôt.
  - Installation des dépendances, par exemple avec `npm install` pour un projet Node.js.
  - Migration de base de données ou autres tâches préalables au lancement.
  - Démarrage de la nouvelle version de l'application.


L'utilisation de `appleboy/ssh-action` dans un workflow GitHub Actions offre une méthode puissante et sécurisée pour automatiser le déploiement d'applications sur un VPS. En combinaison avec un script de déploiement comme `deploy.sh`, les développeurs peuvent simplifier et sécuriser le processus de mise à jour et de maintenance de leurs applications sur des serveurs distants, en s'assurant que les bonnes pratiques sont suivies et que les configurations sont cohérentes.



## 5.1.5 Détails de la Création du Workflow

```yaml
name: Deploy to VPS
```
- Définit le nom du workflow, "Deploy to VPS", pour une identification facile dans l'interface GitHub Actions.

```yaml
on:
  push:
    branches:
      - main
```
- Déclenche le workflow sur chaque `push` à la branche `main`, garantissant que le déploiement s'effectue automatiquement après chaque mise à jour importante.

```yaml
jobs:
  deploy:
    runs-on: ubuntu-latest
```
- Définit un job nommé `deploy` qui s'exécutera sur le dernier runner Ubuntu disponible, fournissant un environnement de build standardisé.

```yaml
steps:
  - name: Checkout code
    uses: actions/checkout@v2
```
- Inclut une étape pour extraire le code source du dépôt GitHub, en utilisant l'action `actions/checkout@v2`, afin que le workflow puisse opérer sur le code actuel.

```yaml
  - name: SSH and Deploy
    uses: appleboy/ssh-action@master
```
- Utilise l'action `appleboy/ssh-action@master` pour établir une connexion SSH au VPS, permettant l'exécution de commandes à distance.

```yaml
    with:
      host: ${{ secrets.VPS_HOST }}
      username: "votre_user"
      key: ${{ secrets.SSH_KEY }}
      script: |
        cd /path/to/your/app
        git pull
        ./deploy.sh
```
- Spécifie les détails de la connexion SSH et le script à exécuter sur le VPS :
  - **host:** Utilise le secret `VPS_HOST` pour indiquer l'adresse du serveur.
  -

 **username:** Votre nom d'utilisateur sur le VPS.
  - **key:** Utilise le secret `SSH_KEY` pour l'authentification SSH.
  - **script:** Les commandes à exécuter sur le VPS, comme naviguer vers le répertoire de votre application, mettre à jour le code source avec `git pull`, et lancer un script de déploiement.


### Explication du `deploy.sh`

L'exemple suivant suppose que vous avez une application web simple que vous souhaitez mettre à jour et redémarrer sur votre serveur VPS.

```bash
#!/bin/bash

# Naviguer dans le répertoire de votre application
cd /path/to/your/app

# Mettre à jour le code source
# Supposons que votre code est hébergé sur un dépôt Git
git pull origin main

# Installer les dépendances
# Exemple pour une application Node.js
npm install

# Construire votre projet si nécessaire
# Exemple pour une application construite avec un outil comme webpack
npm run build

# Redémarrer le serveur
# Cela dépend de la manière dont votre application est servie
# Exemple pour une application Node.js utilisant pm2
pm2 restart app_name

# Pour d'autres types d'applications, vous pouvez avoir besoin de commandes spécifiques
# Exemple pour redémarrer un service systemd
# systemctl restart my_application.service

echo "Déploiement terminé"
```

Ce script effectue les actions suivantes :

1. **Navigation** : Se déplace dans le répertoire où votre application est située sur le serveur.
2. **Mise à jour du code** : Utilise `git pull` pour mettre à jour le code de l'application à la dernière version disponible sur la branche principale.
3. **Installation des dépendances** : Exécute `npm install` pour s'assurer que toutes les dépendances nécessaires sont installées ou mises à jour.
4. **Construction du projet** : Pour les applications qui nécessitent une étape de construction, `npm run build` est exécuté.
5. **Redémarrage du serveur/application** : Utilise `pm2` pour redémarrer l'application Node.js. Si vous utilisez un autre système pour servir votre application, vous aurez besoin d'adapter cette partie du script à vos besoins (par exemple, en utilisant `systemctl restart` pour un service systemd).

Assurez-vous de modifier le script en fonction de l'environnement spécifique de votre serveur et des exigences de votre application. Par exemple, si votre application est une application Python utilisant Gunicorn et Nginx, les commandes de redémarrage et de construction seront différentes.


## Résumé

1. **Introduction aux Secrets** : Les secrets permettent de stocker des informations sensibles, telles que des mots de passe, des jetons d'accès, ou des clés SSH, de manière sécurisée dans GitHub. Ils sont essentiels pour protéger vos données et configurations sensibles lors de l'automatisation des workflows CI/CD.

2. **Utilisation Pratique des Secrets** : 
   - Pour sécuriser la communication avec un serveur VPS dans un workflow GitHub Actions, les secrets tels que `SSH_KEY` et `VPS_HOST` sont utilisés pour stocker respectivement votre clé privée SSH et l'adresse de votre serveur VPS.
   - Un exemple de fichier de workflow, `deploy.yml`, montre comment ces secrets peuvent être intégrés pour déployer une application sur un VPS de manière sécurisée.

3. **`appleboy/ssh-action`** : Cette action GitHub est utilisée pour établir une connexion SSH sécurisée avec un serveur distant, permettant l'exécution de commandes pour le déploiement ou la maintenance. L'utilisation de cette action dans votre workflow facilite l'automatisation des déploiements tout en maintenant la sécurité grâce à l'usage de secrets.

4. **Le Script de Déploiement `deploy.sh`** : 
   - Un script shell côté serveur qui contient les commandes nécessaires pour mettre à jour et redémarrer votre application.
   - Le script est invoqué dans le workflow GitHub Actions, démontrant comment les tâches de déploiement peuvent être automatisées de manière sécurisée en utilisant des secrets pour gérer les informations d'accès.

