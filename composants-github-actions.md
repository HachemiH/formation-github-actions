# 2.2 Composants de base de GitHub Actions

GitHub Actions est un outil puissant de CI/CD intégré à l'écosystème GitHub. Il permet aux développeurs d'automatiser leurs workflows de développement logiciel directement depuis leurs dépôts GitHub. Pour comprendre comment GitHub Actions fonctionne, il est essentiel de se familiariser avec ses composants de base : workflows, jobs, steps, actions, et runners.

## 2.2.1 Diagramme en Arborescence des Composants

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

### 2.2.2 Workflows

Les **workflows** sont des processus automatisés que vous définissez dans votre dépôt GitHub, déclenchés par des événements spécifiques, tels que `push`, `pull_request`, ou des planifications (`schedule`). Ils sont composés de **jobs**.

### 2.2.3 Jobs

Les **jobs** sont des groupes de **steps** qui s'exécutent sur le même runner. Ils peuvent s'exécuter en parallèle ou séquentiellement, selon leur configuration dans le workflow.

### 2.2.4 Steps

Les **steps** sont les tâches individuelles qui s'exécutent dans un job. Un step peut exécuter une commande shell ou utiliser une **action**.

### 2.2.5 Actions

Les **actions** sont des ensembles de tâches préemballées que vous pouvez utiliser dans vos steps. Elles peuvent être trouvées sur le **GitHub Marketplace** ou définies dans votre dépôt.

### 2.2.6 Runners

Les **runners** sont des serveurs qui exécutent vos workflows. GitHub fournit des runners hébergés pour différents systèmes d'exploitation, ou vous pouvez configurer vos propres serveurs comme runners auto-hébergés.

Cette structure clarifie la manière dont les différents composants de GitHub Actions interagissent pour automatiser les processus de développement, de la définition du workflow jusqu'à l'exécution des tâches sur des runners.
