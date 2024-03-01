# Module 2.1 : Introduction à GitHub Actions 

<blockquote>
  <h2>Prérequis</h2>
  <p>Avant de vous lancer dans ce module, vous devriez avoir :</p>
  <ul>
    <li>Une compréhension de base des principes de développement logiciel et du workflow de développement.</li>
    <li>Une familiarité avec l'utilisation de Git et GitHub pour la gestion de versions.</li>
    <li>Une connaissance initiale des concepts DevOps, bien que non obligatoire, serait bénéfique.</li>
  </ul>
</blockquote>

<blockquote>
  <h2>Objectifs Pédagogiques</h2>
  <p>Après avoir complété ce module, vous serez capable de :</p>
  <ul>
    <li>Expliquer ce qu'est GitHub Actions et son rôle au sein de l'écosystème GitHub.</li>
    <li>Identifier comment GitHub Actions peut être utilisé pour automatiser les workflows de CI/CD.</li>
    <li>Comprendre l'intégration de GitHub Actions avec d'autres services et fonctionnalités GitHub.</li>
    <li>Gérer efficacement les minutes d'exécution pour optimiser l'utilisation des ressources dans GitHub Actions.</li>
  </ul>
</blockquote>

---

GitHub Actions est un outil d'automatisation puissant qui s'intègre parfaitement dans l'écosystème GitHub, offrant aux développeurs la capacité d'automatiser leurs workflows de CI/CD directement au sein de leurs dépôts GitHub. En tant que partie intégrante de cet écosystème, GitHub Actions interagit avec une variété de services et fonctionnalités GitHub pour améliorer le cycle de vie du développement logiciel.

## 2.1.1 L'Écosystème GitHub

L'écosystème GitHub englobe une large gamme de fonctionnalités et de services conçus pour soutenir le développement de logiciels, y compris :


- [**Dépôts Git**](https://docs.github.com/fr/repositories) : Au cœur de GitHub, permettant le stockage et la gestion de code source.
- [**Pull Requests et Code Review**](https://docs.github.com/fr/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-pull-requests) : Facilitent la collaboration et l'amélioration du code entre les développeurs.
- [**GitHub Issues**](https://docs.github.com/fr/issues/tracking-your-work-with-issues/about-issues) : Un système de suivi pour signaler et suivre les bugs, les demandes de fonctionnalités et les tâches.
- [**GitHub Pages**](https://pages.github.com/) : Permet de héberger gratuitement des sites web directement à partir d'un dépôt GitHub.
- [**GitHub Marketplace**](https://github.com/marketplace) : Un marché pour trouver et partager des outils et des services qui se connectent à GitHub, y compris des actions personnalisées pour GitHub Actions.
- [**GitHub Security**](https://github.com/features/security) : Des fonctionnalités comme le scanning de vulnérabilités et les advisories pour améliorer la sécurité des projets.
- [**Explore**](https://github.com/explore) : Découvrez les projets, collections, tendances, et ressources partagées par la communauté GitHub.

## 2.1.2 Intégration de GitHub Actions

GitHub Actions s'intègre de manière fluide dans cet écosystème, en tirant parti des fonctionnalités existantes de GitHub pour automatiser les workflows de développement. Par exemple :

- **Automatisation des Tests** : Lancer automatiquement des tests chaque fois qu'un nouveau code est poussé ou qu'une Pull Request est créée, en utilisant les résultats pour informer les décisions de code review.
- **Déploiement Automatisé** : Utiliser GitHub Actions pour déployer automatiquement des applications sur des services comme GitHub Pages ou des serveurs cloud, chaque fois que le code dans la branche principale est mis à jour.
- **Intégration avec GitHub Issues** : Automatiser la création d'issues basées sur des erreurs de compilation ou des échecs de tests pour faciliter le suivi des problèmes.
- **Sécurité et Conformité** : Exécuter des scans de sécurité automatiques et appliquer des politiques de conformité à chaque étape du développement.

GitHub Actions rend l'automatisation accessible directement à partir du dépôt GitHub, renforçant l'écosystème GitHub en offrant une plateforme d'automatisation intégrée qui connecte tous ces éléments ensemble. Cela simplifie la mise en place de workflows CI/CD, réduit les barrières à l'entrée pour l'automatisation, et améliore la cohérence et la fiabilité des processus de développement.


## 2.1.3 Gestion des Minutes d'Exécution avec GitHub Actions

GitHub Actions utilise un système de crédits pour gérer l'utilisation des ressources nécessaires à l'exécution des workflows. Ces crédits sont calculés en minutes d'exécution, qui varient selon le type de runner utilisé (Ubuntu, macOS, Windows) et le plan de facturation du dépôt GitHub.

### 2.1.3.1 Compréhension des Minutes d'Exécution

- **Minutes Gratuites** : GitHub offre un certain nombre de minutes gratuites par mois pour l'exécution de workflows, qui varie selon le type de compte (public, privé) et le plan souscrit.
- **Au-delà des Minutes Gratuites** : Une fois le quota de minutes gratuites dépassé, les utilisateurs sont facturés selon un tarif fixe par minute supplémentaire utilisée. Les tarifs varient en fonction du type de runner.

### 2.1.3.2 Optimisation de l'Utilisation des Minutes

Pour maximiser l'efficacité et minimiser les coûts, considérez les stratégies suivantes :

- **Réduire le Temps d'Exécution** : Optimisez les workflows en réduisant les étapes inutiles ou en combinant des commandes pour diminuer le temps d'exécution global.
- **Utiliser des Runners Auto-Hébergés** : Pour les workflows intensifs ou fréquents, envisagez d'utiliser des runners auto-hébergés pour éviter les coûts supplémentaires.
- **Cibler les Pushs Importants** : Configurez les workflows pour qu'ils se déclenchent uniquement sur des événements spécifiques, comme des pushs sur des branches particulières ou des tags, pour réduire le nombre d'exécutions inutiles.

### 2.1.3.3 Suivi et Gestion

GitHub fournit des outils pour suivre et gérer l'utilisation des minutes d'exécution :

- **Dashboard d'Utilisation** : Accédez au dashboard de facturation de votre compte GitHub pour voir l'utilisation actuelle des minutes et ajuster vos workflows en conséquence.
- **Alertes de Consommation** : Configurez des alertes pour être notifié lorsque vous approchez de votre limite de minutes gratuites, vous permettant de prendre des mesures avant d'engager des frais supplémentaires.

En comprenant et en gérant activement l'utilisation des minutes d'exécution, vous pouvez tirer le meilleur parti de GitHub Actions tout en contrôlant les coûts associés à l'automatisation de vos workflows.


## Résumé

1. **Introduction à GitHub Actions** : GitHub Actions est un outil d'automatisation intégré à GitHub qui permet d'orchestrer des workflows de CI/CD directement depuis un dépôt GitHub.

2. **L'Écosystème GitHub** : GitHub Actions tire parti des fonctionnalités GitHub existantes, comme les dépôts Git, les Pull Requests, GitHub Issues, et GitHub Pages, pour simplifier l'automatisation des tests, du déploiement, et d'autres tâches liées au développement logiciel.

3. **Intégration de GitHub Actions** :
   - Automatisation des tests lors de chaque push ou Pull Request.
   - Déploiements automatisés sur diverses plateformes, y compris GitHub Pages ou des serveurs cloud.
   - Utilisation avec GitHub Issues pour le suivi automatique des bugs.
   - Exécution de scans de sécurité et de vérifications de conformité.

4. **Gestion des Minutes d'Exécution** :
   - GitHub offre un nombre de minutes gratuites pour l'exécution des workflows, avec des coûts additionnels si le quota est dépassé.
   - Optimisez l'utilisation des minutes en réduisant le temps d'exécution des workflows et en utilisant des runners auto-hébergés pour les tâches intensives.
   - Utilisez le dashboard d'utilisation et configurez des alertes pour gérer votre consommation et éviter des coûts inattendus.

Ce module vous a fourni une vue d'ensemble de GitHub Actions et de son importance dans l'automatisation des workflows de CI/CD, ainsi que des stratégies pour gérer efficacement les ressources et optimiser vos processus d'automatisation.

---

Si vous avez d'autres modules ou sujets pour lesquels vous souhaitez un format similaire, n'hésitez pas à les partager.
