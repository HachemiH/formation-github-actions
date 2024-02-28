# 3.1 Création de votre premier Workflow

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

