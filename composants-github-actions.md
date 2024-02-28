# 2.2 Composants de base de GitHub Actions

GitHub Actions est un outil puissant de CI/CD intégré à l'écosystème GitHub. Il permet aux développeurs d'automatiser leurs workflows de développement logiciel directement depuis leurs dépôts GitHub. Pour comprendre comment GitHub Actions fonctionne, il est essentiel de se familiariser avec ses composants de base : workflows, jobs, steps, actions, et runners.


## 2.2.1 Configuration des Workflows avec des Fichiers YAML

Les workflows de GitHub Actions sont configurés à l'aide de fichiers YAML (*.yml ou *.yaml), un format de sérialisation de données lisible par l'homme, conçu pour être simple et clair. Ces fichiers YAML décrivent les étapes précises que les workflows doivent exécuter, y compris les conditions de déclenchement, les jobs, les actions à utiliser, les environnements d'exécution (runners), et toute autre configuration nécessaire.

## 2.2.2 Diagramme en Arborescence des Composants

```md
GitHub Actions
├── Workflows
│   ├── Jobs
│   │   ├── Steps
│   │   │   ├── Actions
│   │   │   └── Commandes shell
│   │   └── Runners
│   └── Déclencheurs d'événements
│       ├── push
│       ├── pull_request
│       └── schedule
└── GitHub Marketplace (pour trouver des actions)
```

### 2.2.3 Workflows

Les **workflows**, dans le contexte de GitHub Actions, sont essentiellement des recettes ou des plans d'action que vous créez pour automatiser certaines tâches au sein de votre projet GitHub. Imaginez les workflows comme des scripts ou des séquences d'instructions qui s'exécutent automatiquement en réponse à des événements spécifiques au sein de votre dépôt. Ces événements peuvent être, par exemple, un `push` de code nouveau ou mis à jour vers le dépôt, une `pull_request` pour demander l'intégration de modifications, ou encore des déclencheurs basés sur une programmation horaire (`schedule`), parmi d'autres.

Un workflow se compose de `jobs`, qui sont des groupes d'étapes ou de tâches qui s'exécutent sur la même machine virtuelle ou conteneur. Chaque job peut effectuer des tâches comme la construction d'une application, l'exécution de tests ou le déploiement d'un site web. Les jobs au sein d'un même workflow peuvent s'exécuter séquentiellement ou en parallèle, selon comment vous les configurez.

Pour créer un workflow, vous écrivez un fichier YAML qui décrit les événements déclencheurs, les jobs à exécuter, et les étapes spécifiques de chaque job. Ce fichier YAML est ensuite placé dans un répertoire spécifique de votre dépôt GitHub (`.github/workflows`), où GitHub Actions peut le trouver et l'utiliser pour exécuter vos workflows automatiquement en réponse aux événements définis.

### 2.2.4 Jobs

Les **jobs** sont des groupes de **steps** qui s'exécutent sur le même runner. Ils peuvent s'exécuter en parallèle ou séquentiellement, selon leur configuration dans le workflow.

Dans GitHub Actions ce sont essentiellement des tâches ou des ensembles d'opérations que vous souhaitez exécuter dans le cadre de votre workflow. Vous pouvez les voir comme des "missions" spécifiques attribuées à des "agents" (les runners), où chaque job contient une série d'étapes ou de commandes à accomplir. Ces étapes peuvent inclure des tâches comme la construction de votre code, l'exécution de tests, ou le déploiement d'une application.

#### Comprendre les Jobs dans GitHub Actions

- **Groupement de Tâches** : Un job regroupe logiquement des étapes qui accomplissent un objectif commun. Par exemple, un job peut être dédié à la construction de votre application, tandis qu'un autre pourrait se concentrer sur l'exécution de tests automatisés.
  
- **Exécution sur des Runners** : Les jobs s'exécutent sur des runners, qui sont des serveurs ou des environnements virtuels mis à disposition par GitHub pour exécuter les actions et les commandes définies dans vos jobs. Chaque job démarre dans un environnement propre, garantissant que les tâches sont exécutées dans un contexte isolé et contrôlé.

- **Configuration de l'Exécution** : Dans le fichier YAML de votre workflow, vous pouvez configurer vos jobs pour qu'ils s'exécutent en parallèle ou de manière séquentielle. L'exécution en parallèle peut accélérer le processus global de CI/CD en permettant à plusieurs tâches de se dérouler simultanément, tandis que l'exécution séquentielle est utile pour des tâches qui doivent être réalisées dans un ordre spécifique.


Les jobs sont au cœur des workflows GitHub Actions, fournissant la structure nécessaire pour diviser vos processus d'intégration et de déploiement continus en tâches gérables et logiquement organisées. Cette structuration facilite non seulement la compréhension et la maintenance de vos workflows mais permet également une exécution plus efficace et flexible de vos pipelines CI/CD.

### 2.2.5 Steps

Les **steps** sont les tâches individuelles qui s'exécutent dans un job. Un step peut exécuter une commande shell ou utiliser une **action**.

Dans le contexte de GitHub Actions, ce sont les éléments constitutifs d'un job. Imaginez que chaque job est une recette de cuisine, et chaque **step** est une instruction ou une action spécifique nécessaire pour compléter cette recette. Ces étapes peuvent varier de simples commandes shell, comme vérifier la version d'un logiciel installé, à l'utilisation d'actions plus complexes disponibles dans le GitHub Marketplace, telles que déployer une application sur le cloud.

#### Comprendre les Steps dans GitHub Actions

- **Actions Individuelles** : Chaque step représente une action individuelle ou une commande qui doit être exécutée. Les steps sont exécutés séquentiellement, dans l'ordre où ils sont définis dans le fichier YAML de votre workflow.

- **Types de Steps** :
  - **Commandes Shell** : Vous pouvez écrire directement des commandes shell ou des scripts qui s'exécuteront sur le runner. C'est utile pour des tâches de préparation, comme la configuration de l'environnement ou la vérification des prérequis.
  - **Actions** : Les actions sont des ensembles de commandes ou de scripts préemballés que vous pouvez réutiliser dans vos workflows. GitHub Marketplace offre une large gamme d'actions créées par la communauté et GitHub pour accomplir des tâches courantes, comme le déploiement sur AWS ou l'envoi de notifications Slack.

Les steps sont essentiels pour décomposer les jobs en tâches gérables, permettant une structure claire et logique de votre pipeline CI/CD. En combinant diverses actions et commandes, vous pouvez créer des workflows puissants et flexibles qui répondent précisément aux besoins de votre projet.


### 2.2.6 Actions

Les **actions** sont des ensembles de tâches préemballées que vous pouvez utiliser dans vos steps. Elles peuvent être trouvées sur le **GitHub Marketplace** ou définies dans votre dépôt.

### 2.2.7 Runners

Les **runners** sont des serveurs qui exécutent vos workflows. GitHub fournit des runners hébergés pour différents systèmes d'exploitation, ou vous pouvez configurer vos propres serveurs comme runners auto-hébergés.

Cette structure clarifie la manière dont les différents composants de GitHub Actions interagissent pour automatiser les processus de développement, de la définition du workflow jusqu'à l'exécution des tâches sur des runners.


