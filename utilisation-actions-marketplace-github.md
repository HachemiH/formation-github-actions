# 4.1 Utilisation d'Actions du GitHub Marketplace

GitHub Actions est un puissant outil d'automatisation qui permet aux développeurs de simplifier et d'automatiser leur flux de travail CI/CD directement au sein de leurs dépôts GitHub. Un des avantages clés de GitHub Actions est sa capacité à intégrer des "Actions" préfabriquées disponibles via le GitHub Marketplace. Ces Actions peuvent être considérées comme des "briques de Lego" que vous pouvez assembler pour créer des workflows personnalisés sans avoir à réinventer la roue pour chaque nouvelle tâche.

## Rechercher des Actions dans le GitHub Marketplace

Pour trouver des Actions adaptées à vos besoins :
1. Rendez-vous sur le [GitHub Marketplace](https://github.com/marketplace?type=actions).
2. Utilisez la barre de recherche pour filtrer les Actions par des mots-clés spécifiques, comme "lint", "test", "deploy", etc.
3. Parcourez les résultats pour trouver une Action qui correspond à vos besoins. Chaque Action sur le Marketplace est accompagnée d'une description, d'instructions d'utilisation, et souvent d'un lien vers le dépôt source pour plus de détails.

## Choisir une Action

Lorsque vous choisissez une Action, prenez en compte :
- **La popularité et les avis** : Une Action largement utilisée et bien notée est généralement un choix sûr.
- **La maintenance et l'activité du dépôt** : Une Action régulièrement mise à jour est plus susceptible de fonctionner sans problème et de rester compatible avec les versions futures de GitHub Actions.

## Intégrer une Action dans votre Workflow

Supposons que vous vouliez intégrer une Action simple pour exécuter des tests sur votre application. Voici comment vous pourriez procéder :

1. Créez un fichier de workflow dans votre dépôt, par exemple `.github/workflows/ci.yml`.
2. Utilisez la syntaxe YAML pour définir votre workflow. Commencez par nommer votre workflow et définir sur quels événements il doit être déclenché :

```yaml
name: CI Workflow

on: [push, pull_request]
```

3. Ajoutez un job qui utilise l'Action trouvée dans le Marketplace. Par exemple, pour utiliser une Action qui exécute des tests npm :

```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Run npm test
        uses: actions/setup-node@v2
        with:
          node-version: '14'
      - run: npm install
      - run: npm test
```

Dans cet exemple :
- `actions/checkout@v2` est une Action qui permet à votre workflow de cloner votre dépôt GitHub.
- `actions/setup-node@v2` est une Action pour configurer l'environnement Node.js.
- Les étapes `npm install` et `npm test` sont des commandes exécutées dans le runner pour installer les dépendances et exécuter les tests.

En suivant ces étapes, vous pouvez rapidement intégrer et tirer parti des Actions disponibles sur le GitHub Marketplace pour automatiser et améliorer vos flux de travail CI/CD sans effort de développement supplémentaire.

