# Module 3.2 : Déclencheurs d'Événements dans GitHub Actions

GitHub Actions permet de définir des workflows automatisés qui sont exécutés en réponse à des événements spécifiques dans votre dépôt GitHub. Ces déclencheurs d'événements jouent un rôle clé dans l'automatisation de votre pipeline CI/CD, en permettant aux workflows de réagir de manière dynamique à des changements ou à des actions spécifiques.

## Types de Déclencheurs d'Événements

### Push

- **Syntaxe**: `on: push`
- **Description**: Ce déclencheur active un workflow chaque fois qu'un commit est poussé vers le dépôt. Il peut être configuré pour réagir à des poussées sur des branches ou des tags spécifiques.

### Pull Request

- **Syntaxe**: `on: pull_request`
- **Description**: Active un workflow lorsqu'une action est effectuée sur une Pull Request, comme sa création, sa mise à jour, ou sa fermeture. Ce déclencheur est utile pour automatiser des tests ou des vérifications de code avant la fusion d'une Pull Request.

### Schedule

- **Syntaxe**: `on: schedule`
- **Description**: Permet de planifier l'exécution d'un workflow à des moments précis, en utilisant la syntaxe cron. Ce déclencheur est idéal pour des tâches récurrentes, comme des mises à jour quotidiennes ou des vérifications régulières de l'état du dépôt.

### Workflow Dispatch

- **Syntaxe**: `on: workflow_dispatch`
- **Description**: Ce déclencheur permet de lancer manuellement un workflow depuis GitHub, offrant une flexibilité pour exécuter des workflows selon les besoins, sans attendre un événement automatique.

### Autres Événements

- **Syntaxe**: `on: <event_name>`
- **Description**: GitHub Actions supporte une variété d'autres événements, tels que `issues`, `release`, et `fork`. Chaque type d'événement permet de déclencher des workflows pour des cas d'usage spécifiques, renforçant l'intégration et l'automatisation dans l'écosystème GitHub.

## Configuration d'un Déclencheur d'Événement

La configuration d'un déclencheur se fait dans le fichier YAML du workflow, sous la clé `on`. Voici un exemple de workflow déclenché par des push sur la branche principale et par des événements sur des Pull Requests :

```yaml
name: Mon Workflow CI
on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
    - run: echo "Workflow exécuté suite à un push ou une pull request sur la branche main."
```

En utilisant ces déclencheurs d'événements, vous pouvez créer des workflows qui s'alignent précisément sur le cycle de vie de votre projet, améliorant l'efficacité et la réactivité de votre pipeline CI/CD.
