# 5.1 Gérer les Secrets dans GitHub

<blockquote>
  <h2>Objectifs Pédagogiques</h2>
  <p>À la fin de ce module, l'apprenant sera en mesure de :</p>
  <ul>
    <li>Comprendre ce que sont les secrets et pourquoi ils sont essentiels pour sécuriser les workflows CI/CD.</li>
    <li>Savoir comment ajouter, modifier et gérer les secrets dans GitHub pour une utilisation dans GitHub Actions.</li>
    <li>Apprendre à utiliser des secrets dans des workflows pour interagir de manière sécurisée avec un VPS.</li>
  </ul>
</blockquote>

<blockquote>
  <h2>Prérequis</h2>
  <p>Connaissances de base de l'utilisation de GitHub et des workflows GitHub Actions.</p>
  <p>Compréhension élémentaire des serveurs VPS et de la connexion sécurisée via SSH.</p>
</blockquote>


La gestion des secrets est cruciale dans les workflows d'intégration et de déploiement continus (CI/CD), particulièrement lorsqu'il s'agit d'automatiser des interactions avec des systèmes externes comme les serveurs VPS. Les secrets permettent de stocker et d'utiliser des données sensibles de manière sécurisée, sans les exposer dans le code ou les logs de build.

## Découverte des Secrets

### Qu'est-ce qu'un Secret ?

Un secret dans GitHub est une donnée sensible que vous souhaitez garder privée, telle qu'un mot de passe, un jeton d'accès, une clé SSH, ou toute autre information confidentielle requise par votre workflow CI/CD.

### Pourquoi Utiliser des Secrets ?

Les secrets sont utilisés pour :

- Protéger vos données sensibles contre les expositions accidentelles.
- Séparer les informations de configuration du code source, conformément aux meilleures pratiques de sécurité.
- Permettre une modification et gestion centralisées des données d'accès sans nécessiter de changer le code source ou les workflows.

## Exemple Pratique : Utilisation d'un Secret avec un VPS

Imaginons que vous souhaitiez déployer votre application sur un VPS via SSH en utilisant GitHub Actions. Voici comment procéder :

### Configuration des Secrets

- `SSH_KEY` : Votre clé privée SSH, utilisée pour établir une connexion sécurisée au VPS sans exposer votre mot de passe.
- `VPS_HOST` : L'adresse de votre serveur VPS, permettant à GitHub Actions de savoir où se connecter.

### Création du Workflow

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

## Résumé

Les secrets dans GitHub offrent un moyen sécurisé de gérer les données sensibles nécessaires aux workflows CI/CD, en particulier lors de l'interaction avec des systèmes externes comme les VPS. En les utilisant, vous pouvez maintenir la sécurité et l'intégrité de vos processus d'automatisation tout en facilitant la gestion des informations d'accès critiques.

---
