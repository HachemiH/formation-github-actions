# 4.1 Utilisation d'Actions du GitHub Marketplace

GitHub Actions transforme vos dépôts GitHub en un puissant atelier d'automatisation CI/CD, où chaque "Action" du GitHub Marketplace agit comme un outil spécialisé sur votre établi. Pensez à ces Actions comme à des applications que vous téléchargez sur votre smartphone pour accomplir des tâches spécifiques - sauf que dans ce cas, elles aident à automatiser des aspects de votre développement logiciel.

## Découvrir des Actions pour Automatiser votre Workflow

### Comment trouver les bons outils pour votre atelier ?

1. Visitez le [GitHub Marketplace](https://github.com/marketplace?type=actions) - votre magasin d'outils pour l'automatisation.
2. Utilisez la barre de recherche comme votre guide. Tapez des mots-clés relatifs à ce que vous souhaitez automatiser (par exemple, "lint", "build", "test", ou "deploy").
3. Explorez les options disponibles. Chaque Action est présentée avec une description détaillée, des instructions pour l'incorporer dans votre workflow, et parfois un lien vers son dépôt GitHub pour plus d'informations.

### Sélectionner la Meilleure Action

Quand vous choisissez un outil de votre kit d'automatisation :
- **Regardez les étoiles et lisez les critiques** : Ce sont vos indices pour choisir un outil fiable et approuvé par la communauté.
- **Vérifiez la date de la dernière mise à jour** : Un outil fréquemment mis à jour est synonyme de fiabilité et de compatibilité continue.

## Mise en Place d'une Action dans votre Workflow

Imaginons que vous voulez établir une chaîne de montage automatisée pour tester votre application à chaque mise à jour. Voici la recette pour y arriver :

1. **Créez le plan de votre chaîne de montage** : Ouvrez un nouveau fichier dans `.github/workflows/`, par exemple, `ci.yml`. Ce fichier est votre blueprint.
2. **Définissez les déclencheurs de votre chaîne** :

    ```yaml
    name: CI Workflow

    on: [push, pull_request]
    ```

    Ici, vous dites : "Chaque fois qu'il y a un push ou une pull request, démarrez la chaîne."

3. **Ajoutez les outils (Actions) à votre chaîne** :

    ```yaml
    jobs:
      build:
        runs-on: ubuntu-latest
        steps:
          - uses: actions/checkout@v2
          - name: Set up Node.js
            uses: actions/setup-node@v2
            with:
              node-version: '14'
          - run: npm install
          - run: npm test
    ```

    Dans cet exemple :
    - `actions/checkout@v2` vous permet de cloner votre code sur le serveur qui exécutera le workflow.
    - `actions/setup-node@v2` prépare l'environnement pour Node.js.
    - `npm install` et `npm test` sont vos commandes pour assembler et tester le produit.

En assemblant ces éléments, vous créez un processus automatisé qui teste votre application à chaque mise à jour, comme une chaîne de montage qui assure que chaque pièce est prête avant de quitter l'usine.

