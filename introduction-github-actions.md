
# Module 2.1 : Introduction à GitHub Actions 

GitHub Actions est un outil d'automatisation puissant qui s'intègre parfaitement dans l'écosystème GitHub, offrant aux développeurs la capacité d'automatiser leurs workflows de CI/CD directement au sein de leurs dépôts GitHub. En tant que partie intégrante de cet écosystème, GitHub Actions interagit avec une variété de services et fonctionnalités GitHub pour améliorer le cycle de vie du développement logiciel.

## 2.1.1 L'Écosystème GitHub

L'écosystème GitHub englobe une large gamme de fonctionnalités et de services conçus pour soutenir le développement de logiciels, y compris :

- **Dépôts Git** : Au cœur de GitHub, permettant le stockage et la gestion de code source.
- **Pull Requests et Code Review** : Facilitent la collaboration et l'amélioration du code entre les développeurs.
- **GitHub Issues** : Un système de suivi pour signaler et suivre les bugs, les demandes de fonctionnalités et les tâches.
- **GitHub Pages** : Permet de héberger gratuitement des sites web directement à partir d'un dépôt GitHub.
- **GitHub Marketplace** : Un marché pour trouver et partager des outils et des services qui se connectent à GitHub, y compris des actions personnalisées pour GitHub Actions.
- **GitHub Security** : Des fonctionnalités comme le scanning de vulnérabilités et les advisories pour améliorer la sécurité des projets.

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



