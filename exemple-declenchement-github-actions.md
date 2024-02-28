# Module 3.3 : Automatisation d'une Réponse à une Issue avec GitHub Actions

Ce module vous apprendra comment configurer un workflow GitHub Actions pour automatiser une réponse à une issue. Ce processus met en œuvre des déclencheurs d'événements pour activer le workflow, illustrant un cas d'usage pratique de GitHub Actions.

## Étape 1 : Création du Fichier de Workflow

1. **Accédez à votre dépôt GitHub** où vous souhaitez ajouter le workflow.
2. **Créez un nouveau fichier** dans le répertoire `.github/workflows` à la racine de votre dépôt. Si le dossier n'existe pas, créez-le.
3. Nommez votre fichier, par exemple `issue_response.yml`.

## Étape 2 : Configuration du Workflow

Dans le fichier `issue_response.yml`, ajoutez le contenu suivant :

```yaml
name: Issue Response

on:
  issues:
    types: [opened]

jobs:
  respond_to_issue:
    runs-on: ubuntu-latest
    steps:
    - name: Send a response
      uses: actions/github-script@v3
      with:
        github-token: ${{secrets.GITHUB_TOKEN}}
        script: |
          github.issues.createComment({
            issue_number: context.issue.number,
            owner: context.repo.owner,
            repo: context.repo.repo,
            body: 'Merci pour votre issue, notre équipe va se pencher dessus !'
          })
```

## Explication du Fichier YAML

- **`name`**: Nomme votre workflow, facilitant son identification.
- **`on`**: Définit le déclencheur de l'événement, ici `issues` avec le type `opened`, signifiant que le workflow s'exécute chaque fois qu'une issue est ouverte.
- **`jobs`**: Définit les tâches à exécuter, ici `respond_to_issue`.
- **`runs-on`**: Spécifie le type de runner, `ubuntu-latest` dans ce cas.
- **`steps`**: Les étapes à exécuter dans le job, utilisant ici `actions/github-script` pour exécuter un script permettant de commenter automatiquement la nouvelle issue.
- **`github-token`**: Utilise le token `GITHUB_TOKEN` pour authentifier les actions avec GitHub.
- **`script`**: Le script exécuté pour créer un commentaire sur l'issue, indiquant un message de prise en charge.

## Testez Votre Workflow

1. **Poussez** les modifications à votre dépôt.
2. **Ouvrez une nouvelle issue** dans votre dépôt pour déclencher le workflow.
3. **Vérifiez** l'issue pour voir le commentaire automatique posté par GitHub Actions.

Ce module offre un aperçu pratique de l'utilisation des déclencheurs d'événements avec GitHub Actions, démontrant comment automatiser des tâches courantes pour améliorer l'efficacité de la gestion de votre projet.
