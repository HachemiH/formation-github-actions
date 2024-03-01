# 3.1 Création de votre premier Workflow

<blockquote>
  <h2>Prérequis</h2>
  <p>Avant de commencer ce module, assurez-vous de connaître :</p>
  <ul>
    <li>Les bases de l'utilisation de GitHub, y compris la création et la gestion de dépôts.</li>
    <li>Une compréhension élémentaire de YAML et de son syntaxe.</li>
    <li>Les concepts initiaux de l'intégration continue (CI) et du déploiement continu (CD).</li>
  </ul>
</blockquote>

<blockquote>
  <h2>Objectifs Pédagogiques</h2>
  <p>À la fin de ce module, vous serez capable de :</p>
  <ul>
    <li>Créer et configurer un fichier de workflow dans un dépôt GitHub.</li>
    <li>Comprendre et définir les événements déclencheurs pour automatiser les workflows de CI/CD.</li>
    <li>Identifier et utiliser des actions basiques pour exécuter des tâches au sein d'un workflow.</li>
    <li>Planifier l'exécution de workflows à l'aide de déclencheurs basés sur le temps avec la syntaxe cron.</li>
  </ul>
</blockquote>

---

Un **workflow** est un processus automatisé qui vous permet de définir une série de tâches à exécuter sur des événements spécifiques dans votre dépôt GitHub. Voici comment démarrer :

## Étape 1 : Créer un fichier de Workflow

1. Dans votre dépôt GitHub, créez un dossier nommé `.github/workflows`.
2. À l'intérieur de ce dossier, créez un fichier YAML pour votre workflow. Par exemple, `ci.yml`.

## Étape 2 : Définir votre Workflow

Ouvrez le fichier `ci.yml` et commencez à définir votre workflow. Voici un exemple simple :

```yaml
name: Exemple de Workflow CI

on: [push]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
    - name: Exécution d'un script simple
      run: echo "Le workflow CI est déclenché par un push sur GitHub!"
```

### Explications :

- **`name`** : Nomme votre workflow. Ici, "Exemple de Workflow CI".
- **`on`** : Définit le ou les événements qui déclencheront le workflow. Dans cet exemple, le workflow se déclenche à chaque `push`.
- **`jobs`** : Contient un ensemble de jobs à exécuter. Ici, il y a un seul job nommé `build`.
- **`runs-on`** : Spécifie le type de runner que le job doit utiliser. `ubuntu-latest` indique la dernière version d'Ubuntu fournie par GitHub.
- **`steps`** : Étapes à exécuter dans le job. 
  - **`uses: actions/checkout@v2`** : Utilise l'action `checkout` pour cloner votre dépôt dans le runner.
  - **`run`** : Exécute une commande shell. Ici, affiche un message dans les logs.

## 3.2 Déclencheurs d'Événements Communs

Les workflows GitHub Actions peuvent être déclenchés par divers événements GitHub. Voici quelques déclencheurs communs :

- **`push`** : Déclenche le workflow sur les push dans le dépôt.
- **`pull_request`** : Déclenche le workflow sur les événements de Pull Request.
- **`schedule`** : Permet de planifier le workflow à exécuter à des moments précis, en utilisant la syntaxe cron.

### Exemple avec `schedule` :

```yaml
on:
  schedule:
    - cron: '0 2 * * *'
```

- **`schedule`** : Déclenche le workflow selon un planning défini.
- **`cron`** : La syntaxe cron `'0 2 * * *'` signifie que le workflow s'exécute tous les jours à 2h00 UTC.


## Résumé

1. **Création d'un Fichier de Workflow** :
   - **Étape 1** : Créez un dossier `.github/workflows` dans votre dépôt GitHub pour stocker vos fichiers de workflow.
   - **Étape 2** : À l'intérieur de ce dossier, créez un fichier YAML, par exemple `ci.yml`, qui contiendra la définition de votre workflow.

2. **Définition de votre Workflow** :
   - Nommez votre workflow et définissez les événements qui le déclencheront, comme les `push` sur le dépôt.
   - Configurez les `jobs` à exécuter, spécifiant le type de `runner` et les `steps` que le job doit effectuer, y compris l'utilisation d'actions pour cloner votre dépôt et exécuter des commandes shell.

3. **Déclencheurs d'Événements Communs** :
   - Les workflows peuvent être activés par des événements tels que `push`, `pull_request`, ou à des moments précis grâce à `schedule`, en utilisant la syntaxe cron pour la planification.


