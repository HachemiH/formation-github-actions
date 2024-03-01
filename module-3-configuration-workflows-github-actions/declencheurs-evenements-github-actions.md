# Module 3.2 : Déclencheurs d'Événements dans GitHub Actions

<blockquote>
  <h2>Prérequis</h2>
  <p>Avant d'aborder ce module, il est recommandé d'avoir :</p>
  <ul>
    <li>Une compréhension de base des workflows GitHub Actions introduits dans les modules précédents.</li>
    <li>Une familiarité avec les concepts de base de Git, notamment les commits, les branches, et les Pull Requests.</li>
  </ul>
</blockquote>

<blockquote>
  <h2>Objectifs Pédagogiques</h2>
  <p>Après avoir complété ce module, vous serez capable de :</p>
  <ul>
    <li>Comprendre et utiliser différents types de déclencheurs d'événements pour automatiser les workflows GitHub Actions.</li>
    <li>Configurer des workflows pour réagir à des événements spécifiques tels que les push, les Pull Requests, et les événements planifiés avec la syntaxe cron.</li>
    <li>Exploiter la flexibilité des déclencheurs d'événements pour améliorer l'automatisation et l'efficacité de votre pipeline CI/CD.</li>
  </ul>
</blockquote>

---

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



## Résumé

1. **Push** : Automatisez l'exécution de workflows à chaque fois qu'un commit est poussé vers le dépôt, permettant une intégration continue efficace.

2. **Pull Request** : Utilisez ce déclencheur pour lancer des workflows lorsqu'une action est effectuée sur une Pull Request, facilitant les tests automatisés et les vérifications de code avant la fusion.

3. **Schedule** : Planifiez l'exécution de workflows à des moments précis avec la syntaxe cron, idéal pour les tâches récurrentes comme les mises à jour ou les audits réguliers.

4. **Workflow Dispatch** : Offre la possibilité de déclencher manuellement des workflows depuis GitHub, apportant une flexibilité pour exécuter des tâches à la demande.

5. **Autres Événements** : GitHub Actions prend en charge une large gamme d'événements, vous permettant de créer des workflows personnalisés qui s'adaptent à divers besoins et scénarios d'automatisation.

6. **Configuration d'un Déclencheur** : La configuration des déclencheurs se fait facilement dans le fichier YAML du workflow, vous permettant de spécifier les branches et les conditions sous lesquelles vos workflows doivent s'exécuter.

