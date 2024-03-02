# Module 2.2 : Composants de base de GitHub Actions

<blockquote>
  <h2>Prérequis</h2>
  <p>Avant de plonger dans ce chapitre, il est recommandé d'avoir :</p>
  <ul>
    <li>Une compréhension de base de l'usage et de la navigation sur GitHub.</li>
    <li>Une familiarité avec le concept de l'intégration continue (CI) et du déploiement continu (CD).</li>
    <li>Des connaissances élémentaires en YAML et en scripting.</li>
  </ul>
</blockquote>

<blockquote>
  <h2>Objectifs Pédagogiques</h2>
  <p>Après avoir terminé ce chapitre, vous serez capable de :</p>
  <ul>
    <li>Identifier et décrire les composants clés de GitHub Actions, y compris les workflows, jobs, steps, actions, et runners.</li>
    <li>Comprendre la structure et le fonctionnement des fichiers YAML pour la configuration des workflows GitHub Actions.</li>
    <li>Appliquer des pratiques d'optimisation pour l'utilisation efficace des ressources GitHub Actions, notamment la gestion des minutes d'exécution.</li>
  </ul>
</blockquote>

---

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

Elles sont comparables à des outils spécialisés ou des plugins que vous pouvez incorporer dans vos workflows pour accomplir des tâches spécifiques sans avoir à réécrire le code à chaque fois. Elles représentent des blocs de construction réutilisables conçus pour étendre les fonctionnalités de vos workflows, en facilitant l'exécution de tâches communes ou complexes, telles que le déploiement d'une application, la gestion des versions, ou l'envoi de notifications.

### Approfondissement des Actions

- **Réutilisabilité** : Les actions sont conçues pour être réutilisées dans différents workflows. Vous pouvez les voir comme des briques LEGO® ; chaque action offre une fonctionnalité spécifique, et vous pouvez les assembler pour construire le processus d'intégration et de déploiement qui correspond à vos besoins.

- **Sources des Actions** :
  - **GitHub Marketplace** : Une plateforme où vous pouvez découvrir et utiliser des milliers d'actions développées par la communauté GitHub et par GitHub lui-même. Ces actions couvrent un large éventail de tâches et sont souvent maintenues et mises à jour par leurs créateurs.
  - **Actions Personnalisées** : Vous pouvez également créer vos propres actions spécifiques à vos besoins et les stocker dans votre dépôt. Cela vous permet d'adapter précisément les étapes d'un workflow à votre projet.

Les actions simplifient la mise en œuvre des processus CI/CD en encapsulant des tâches complexes dans des modules réutilisables, réduisant le besoin de scripts volumineux et améliorant la lisibilité et la maintenance de vos workflows.

### 2.2.7 Runners

Les **runners** sont des serveurs qui exécutent vos workflows. GitHub fournit des runners hébergés pour différents systèmes d'exploitation, ou vous pouvez configurer vos propres serveurs comme runners auto-hébergés.

Ils fonctionnent comme des ouvriers spécialisés chargés d'exécuter les tâches que vous avez définies dans vos workflows. Imaginez une équipe de construction où chaque membre a une compétence unique ; de la même façon, les runners prennent en charge l'exécution des jobs que vous avez spécifiés, chaque runner pouvant être spécialisé dans un environnement d'exploitation particulier.

### 2 types de Runners

- **Hébergés par GitHub** : GitHub propose des runners préconfigurés pour les systèmes d'exploitation courants (Linux, Windows, macOS). Ces runners hébergés sont gérés par GitHub, ce qui signifie que vous n'avez pas à vous soucier de leur maintenance ou de leur mise à jour. Ils sont prêts à l'emploi et peuvent être utilisés dès que vous activez GitHub Actions dans votre dépôt.

- **Auto-hébergés** : Pour les cas où vous avez besoin d'un contrôle plus approfondi sur l'environnement d'exécution, par exemple pour des exigences spécifiques de sécurité ou d'utilisation de ressources, GitHub Actions vous permet de configurer vos propres serveurs comme runners. Cela vous donne la flexibilité de personnaliser l'environnement selon les besoins de votre projet, tout en gardant la facilité d'utilisation des workflows GitHub Actions.


En fournissant à la fois des options de runners hébergés et la possibilité de configurer des runners auto-hébergés, GitHub Actions offre une flexibilité maximale pour répondre à différents besoins d'exécution de workflow, que ce soit pour des projets simples ou pour des infrastructures complexes nécessitant des configurations personnalisées.

Cette structure clarifie la manière dont les différents composants de GitHub Actions interagissent pour automatiser les processus de développement, de la définition du workflow jusqu'à l'exécution des tâches sur des runners.

## Résumé

1. **Configuration des Workflows avec des Fichiers YAML** : Apprenez à créer et configurer des workflows GitHub Actions à l'aide de fichiers YAML, qui définissent les événements déclencheurs, les jobs à exécuter, et les étapes spécifiques de chaque job.

2. **Composants Clés** :
   - **Workflows** : Séquences d'instructions automatisées déclenchées par des événements spécifiques dans votre dépôt GitHub.
   - **Jobs** : Groupes de steps qui s'exécutent sur le même runner, pouvant s'exécuter en parallèle ou séquentiellement.
   - **Steps** : Tâches individuelles au sein d'un job, pouvant exécuter des commandes shell ou des actions.
   - **Actions** : Ensembles de tâches préemballées que vous pouvez utiliser dans vos steps pour exécuter des opérations complexes sans écrire de code supplémentaire.
   - **Runners** : Serveurs qui exécutent vos workflows, disponibles en versions hébergées par GitHub ou auto-hébergées pour une personnalisation plus poussée.

3. **Gestion des Minutes d'Exécution** : Optimisez l'utilisation des minutes d'exécution allouées à votre compte GitHub pour exécuter des workflows, en mettant en œuvre des stratégies telles que la réduction du temps d'exécution des workflows, l'usage de runners auto-hébergés, et la configuration précise des événements déclencheurs.


