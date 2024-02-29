# 6.1 Stratégies de Déploiement

<blockquote>
  <h2>Objectifs Pédagogiques</h2>
  <p>À la fin de ce module, vous serez en mesure de :</p>
  <ul>
    <li>Identifier les différentes stratégies de déploiement applicables dans un workflow GitHub Actions.</li>
    <li>Comprendre les avantages et les inconvénients de chaque stratégie de déploiement en fonction des besoins spécifiques du projet.</li>
    <li>Appliquer les meilleures pratiques pour mettre en œuvre une stratégie de déploiement fiable et efficace via GitHub Actions.</li>
  </ul>
</blockquote>

<blockquote>
  <h2>Prérequis</h2>
  <p>Pour aborder ce module dans les meilleures conditions, vous devriez posséder :</p>
  <ul>
    <li>Une compréhension solide des fondamentaux de GitHub Actions, incluant la création et la gestion de workflows.</li>
    <li>Une familiarité avec les concepts de base du déploiement d'applications, tels que l'intégration continue (CI) et le déploiement continu (CD).</li>
    <li>Des connaissances de base sur les serveurs et l'hébergement d'applications, notamment sur les VPS.</li>
  </ul>
</blockquote>

---

Dans le domaine du développement logiciel, le déploiement est une phase cruciale qui consiste à mettre à disposition une application pour les utilisateurs finaux. GitHub Actions offre une flexibilité remarquable pour automatiser cette étape, adaptant le processus aux besoins spécifiques de chaque projet grâce à différentes stratégies de déploiement.

## Les Stratégies de Déploiement

Les stratégies de déploiement définissent comment les applications sont livrées aux environnements de production. Voici quelques stratégies couramment utilisées :

- **Déploiement Blue/Green** : Cette approche implique d'avoir deux environnements de production identiques mais actifs de manière exclusive. L'un est en ligne (bleu) pendant que l'autre (vert) est mis à jour et testé. Une fois prêt, le trafic est basculé du bleu vers le vert, minimisant ainsi le temps d'arrêt.
- **Déploiement Canary** : Des versions nouvelles ou modifiées de l'application sont déployées à un sous-ensemble limité d'utilisateurs avant d'être déployées à l'ensemble de la base d'utilisateurs. Cela permet de tester les changements dans un environnement de production avec un risque minimal.
- **Déploiement Rolling** : Le déploiement se fait progressivement par mises à jour successives des instances ou des serveurs. Chaque serveur est mis à jour individuellement, assurant ainsi que le service reste disponible pendant le processus de déploiement.
- **Déploiement Direct sur VPS** : Pour les projets de petite à moyenne taille, cette stratégie consiste à mettre à jour directement l'environnement de production sur un VPS à chaque push sur une branche spécifique, comme `main`. Cela peut être réalisé en utilisant des actions GitHub pour exécuter des scripts de déploiement qui transfèrent les fichiers mis à jour vers le VPS et redémarrent les services si nécessaire. Cette méthode est simple et efficace pour les projets n'exigeant pas de stratégies de déploiement complexes avec zéro temps d'arrêt.

### Application Pratique : Déploiement Direct sur VPS

Cette stratégie est idéale pour les développeurs ou les petites équipes qui cherchent à automatiser le déploiement de leurs applications web sans la complexité des environnements multiples. Voici un exemple de workflow GitHub Actions pour déployer une application web simple sur un VPS :

1. **Préparez votre VPS** : Assurez-vous que votre VPS est configuré pour recevoir le code (e.g., avec SSH et Git installés).

2. **Configurez les Secrets GitHub** : Stockez les informations sensibles telles que les clés SSH et les adresses des serveurs dans les secrets GitHub.

3. **Créez le Workflow GitHub Actions** :
   - Utilisez `actions/checkout` pour récupérer le code de votre dépôt.
   - Utilisez une action comme `appleboy/ssh-action` pour exécuter un script de déploiement sur votre VPS qui mettra à jour l'application et redémarrera les services nécessaires.


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
      - name: Checkout code
        uses: actions/checkout@v2
      
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

Ce workflow effectue les actions suivantes à chaque push sur la branche `main` :

- **Checkout** : Extrait le code le plus récent.
- **Connexion SSH** : Utilise `appleboy/ssh-action` pour se connecter à votre VPS via SSH.
- **Script de Déploiement** : Met à jour le code de l'application, installe les dépendances, construit l'application et redémarre le processus avec PM2 (ou tout autre gestionnaire de processus que vous utilisez).



### Avantages du Déploiement Direct sur VPS

- **Simplicité** : Facile à mettre en place pour des projets ne nécessitant pas de stratégies de déploiement avancées.
- **Contrôle** : Vous avez un contrôle total sur le processus de déploiement et l'environnement de production.
- **Rapidité** : Les mises à jour peuvent être déployées rapidement après chaque push, facilitant les cycles de développement itératifs.
- **Coût-Efficace** : Réduit le besoin de ressources supplémentaires ou d'une infrastructure complexe.

### Bonnes Pratiques

- **Planifiez et documentez** : Avant d'implémenter une stratégie de déploiement, assurez-vous de comprendre ses implications et de documenter le processus.
- **Testez Localement** : Avant de pousser vos changements, assurez-vous que tout fonctionne comme prévu en local.
- **Backup** : Ayez toujours une stratégie de sauvegarde en place pour votre serveur et votre base de données en cas de problème lors du déploiement.
- **Sécurisez vos Secrets** : Gardez vos informations d'accès au VPS sécurisées en utilisant les secrets GitHub.
- **Automatisez les Tests** : Intégrez des tests automatiques dans votre workflow avant le déploiement pour minimiser les risques de bugs en production.
- **Surveillance et Logs** : Mettez en place une surveillance et des logs adéquats sur votre VPS pour rapidement identifier et résoudre tout problème post-déploiement.

Le déploiement direct sur un VPS est une stratégie efficace pour les petits projets ou les applications web simples, offrant une méthode rapide et automatisée pour mettre à jour votre application en production. En utilisant GitHub Actions pour ce processus, vous pouvez minimiser les temps d'arrêt et maximiser l'efficacité de votre flux de travail de déploiement.

## Application Pratique

Pour appliquer ces stratégies via GitHub Actions, vous utiliserez des workflows qui définissent les étapes de déploiement, incluant des tests, la mise en place de l'environnement et le basculement du trafic. La sélection d'une stratégie dépend de plusieurs facteurs, tels que la tolérance au temps d'arrêt, la capacité à tester en production et la complexité de l'infrastructure.


## Résumé

Les stratégies de déploiement jouent un rôle essentiel dans la gestion efficace et sécurisée des releases d'applications. En vous familiarisant avec les différentes approches et en intégrant celles-ci dans vos workflows GitHub Actions, vous pouvez améliorer la fiabilité et la disponibilité de vos applications lors de leur mise en production.
