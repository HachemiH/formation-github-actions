# Module 6.1 : Stratégies de Déploiement

<blockquote>
  <h2>Prérequis</h2>
  <p>Avant de vous lancer dans ce module, il est recommandé que vous ayez :</p>
  <ul>
    <li>Une solide compréhension des fondamentaux de GitHub Actions, y compris la création et la gestion de workflows.</li>
    <li>Une familiarité avec les concepts de déploiement d'applications, tels que l'intégration continue (CI) et le déploiement continu (CD).</li>
    <li>Des connaissances de base concernant les serveurs et l'hébergement d'applications, en particulier sur les VPS.</li>
  </ul>
</blockquote>

<blockquote>
  <h2>Objectifs Pédagogiques</h2>
  <p>À l'issue de ce module, vous serez capable de :</p>
  <ul>
    <li>Discerner les différentes stratégies de déploiement qui peuvent être intégrées dans un workflow GitHub Actions.</li>
    <li>Évaluer les avantages et les inconvénients de chaque stratégie de déploiement par rapport aux besoins spécifiques de votre projet.</li>
    <li>Mettre en œuvre des stratégies de déploiement choisies de manière fiable et efficace en utilisant GitHub Actions.</li>
  </ul>
</blockquote>

---

Dans le domaine du développement logiciel, le déploiement est une phase cruciale qui consiste à mettre à disposition une application pour les utilisateurs finaux. GitHub Actions offre une flexibilité remarquable pour automatiser cette étape, adaptant le processus aux besoins spécifiques de chaque projet grâce à différentes stratégies de déploiement.

## 6.1.1 Les Stratégies de Déploiement

Les stratégies de déploiement définissent comment les applications sont livrées aux environnements de production. Voici quelques stratégies couramment utilisées :

- **Déploiement Blue/Green** : Cette approche implique d'avoir deux environnements de production identiques mais actifs de manière exclusive. L'un est en ligne (bleu) pendant que l'autre (vert) est mis à jour et testé. Une fois prêt, le trafic est basculé du bleu vers le vert, minimisant ainsi le temps d'arrêt.
- **Déploiement Canary** : Des versions nouvelles ou modifiées de l'application sont déployées à un sous-ensemble limité d'utilisateurs avant d'être déployées à l'ensemble de la base d'utilisateurs. Cela permet de tester les changements dans un environnement de production avec un risque minimal.
- **Déploiement Rolling** : Le déploiement se fait progressivement par mises à jour successives des instances ou des serveurs. Chaque serveur est mis à jour individuellement, assurant ainsi que le service reste disponible pendant le processus de déploiement.
- **Déploiement Direct sur VPS** : Pour les projets de petite à moyenne taille, cette stratégie consiste à mettre à jour directement l'environnement de production sur un VPS à chaque push sur une branche spécifique, comme `main`. Cela peut être réalisé en utilisant des actions GitHub pour exécuter des scripts de déploiement qui transfèrent les fichiers mis à jour vers le VPS et redémarrent les services si nécessaire. Cette méthode est simple et efficace pour les projets n'exigeant pas de stratégies de déploiement complexes avec zéro temps d'arrêt.


## 6.1.2 Bonnes Pratiques

- **Planifiez et documentez** : Avant d'implémenter une stratégie de déploiement, assurez-vous de comprendre ses implications et de documenter le processus.
- **Testez Localement** : Avant de pousser vos changements, assurez-vous que tout fonctionne comme prévu en local.
- **Backup** : Ayez toujours une stratégie de sauvegarde en place pour votre serveur et votre base de données en cas de problème lors du déploiement.
- **Sécurisez vos Secrets** : Gardez vos informations d'accès au VPS sécurisées en utilisant les secrets GitHub.
- **Automatisez les Tests** : Intégrez des tests automatiques dans votre workflow avant le déploiement pour minimiser les risques de bugs en production.
- **Surveillance et Logs** : Mettez en place une surveillance et des logs adéquats sur votre VPS pour rapidement identifier et résoudre tout problème post-déploiement.

Le déploiement direct sur un VPS est une stratégie efficace pour les petits projets ou les applications web simples, offrant une méthode rapide et automatisée pour mettre à jour votre application en production. En utilisant GitHub Actions pour ce processus, vous pouvez minimiser les temps d'arrêt et maximiser l'efficacité de votre flux de travail de déploiement.

## 6.1.3 Application Pratique

Pour appliquer ces stratégies via GitHub Actions, vous utiliserez des workflows qui définissent les étapes de déploiement, incluant des tests, la mise en place de l'environnement et le basculement du trafic. La sélection d'une stratégie dépend de plusieurs facteurs, tels que la tolérance au temps d'arrêt, la capacité à tester en production et la complexité de l'infrastructure.


## Résumé

Dans ce module, vous avez exploré la variété des stratégies de déploiement disponibles pour automatiser la mise en production de vos applications via GitHub Actions. Chaque stratégie présente des caractéristiques uniques adaptées à différents scénarios de déploiement :

1. **Déploiement Blue/Green** : Vous avez appris comment cette méthode réduit le temps d'arrêt en alternant entre deux environnements de production presque identiques.

2. **Déploiement Canary** : Cette stratégie permet de déployer des changements à un petit groupe d'utilisateurs initialement, ce qui est idéal pour tester les impacts en production avec un risque minimal.

3. **Déploiement Rolling** : Vous avez vu comment les mises à jour progressives peuvent maintenir le service disponible en mettant à jour les serveurs un par un.

4. **Déploiement Direct sur VPS** : Cette approche simple convient parfaitement aux petits projets, permettant des mises à jour directes sur un VPS à chaque push sur une branche spécifique.

En comprenant ces stratégies et en les appliquant à travers des workflows GitHub Actions, vous pouvez choisir la méthode la plus adaptée à vos besoins, améliorant ainsi l'efficacité et la sécurité de vos processus de déploiement. Le choix de la stratégie idéale dépend de plusieurs critères, dont la tolérance au temps d'arrêt, la nécessité de tests en production, et la complexité de votre infrastructure.

