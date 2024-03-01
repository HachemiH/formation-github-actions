# Module 4.1 : Utilisation d'Actions du GitHub Marketplace

<blockquote>
  <h2>Prérequis</h2>
  <p>Avant de commencer ce module, vous devriez avoir :</p>
  <ul>
    <li>Une compréhension basique de GitHub Actions et de la création de workflows.</li>
    <li>Une familiarité avec les concepts de CI/CD.</li>
    <li>Des connaissances élémentaires en YAML.</li>
  </ul>
</blockquote>

<blockquote>
  <h2>Objectifs Pédagogiques</h2>
  <p>À la fin de ce module, vous serez capable de :</p>
  <ul>
    <li>Explorer et sélectionner des Actions dans le GitHub Marketplace pour automatiser vos workflows CI/CD.</li>
    <li>Intégrer efficacement des Actions trouvées sur le Marketplace dans vos fichiers de workflow GitHub Actions.</li>
    <li>Évaluer la fiabilité et la pertinence des Actions en fonction des évaluations de la communauté et de la fréquence des mises à jour.</li>
  </ul>
</blockquote>

---

GitHub Actions transforme vos dépôts GitHub en un puissant atelier d'automatisation CI/CD, où chaque "Action" du GitHub Marketplace agit comme un outil spécialisé sur votre établi. Pensez à ces Actions comme à des applications que vous téléchargez sur votre smartphone pour accomplir des tâches spécifiques - sauf que dans ce cas, elles aident à automatiser des aspects de votre développement logiciel.

## 4.1.1 Découvrir des Actions pour Automatiser votre Workflow

### Comment trouver les bons outils pour votre atelier ?

1. Visitez le [GitHub Marketplace](https://github.com/marketplace?type=actions) - votre magasin d'outils pour l'automatisation.
2. Utilisez la barre de recherche comme votre guide. Tapez des mots-clés relatifs à ce que vous souhaitez automatiser (par exemple, "lint", "build", "test", ou "deploy").
3. Explorez les options disponibles. Chaque Action est présentée avec une description détaillée, des instructions pour l'incorporer dans votre workflow, et parfois un lien vers son dépôt GitHub pour plus d'informations.

### Sélectionner la Meilleure Action

Quand vous choisissez un outil de votre kit d'automatisation :
- **Regardez les étoiles et lisez les critiques** : Ce sont vos indices pour choisir un outil fiable et approuvé par la communauté.
- **Vérifiez la date de la dernière mise à jour** : Un outil fréquemment mis à jour est synonyme de fiabilité et de compatibilité continue.

## 4.1.2 Mise en Place d'une Action dans votre Workflow

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


## Résumé

1. **Découverte des Actions** :
   - Visitez le GitHub Marketplace pour trouver des Actions qui correspondent aux tâches que vous souhaitez automatiser.
   - Utilisez des mots-clés relatifs à vos besoins (comme "lint", "build", "test", "deploy") pour filtrer les résultats.

2. **Critères de Sélection** :
   - Lisez les avis et vérifiez le nombre d'étoiles pour évaluer la popularité et la satisfaction des utilisateurs.
   - Assurez-vous que l'Action est régulièrement mise à jour pour garantir sa fiabilité et sa compatibilité.

3. **Intégration d'une Action dans votre Workflow** :
   - Créez un fichier de workflow dans le dossier `.github/workflows/`, par exemple `ci.yml`.
   - Définissez les événements déclencheurs (comme `push` et `pull_request`) pour spécifier quand le workflow doit être exécuté.
   - Ajoutez des Actions spécifiques à votre chaîne de production automatisée, en configurant chaque étape selon les besoins de votre projet, depuis le clonage du code jusqu'à l'exécution des tests.

4. **Exemple Pratique** :
   - L'exemple donné illustre comment configurer un workflow simple pour tester une application Node.js à chaque `push` ou `pull_request`, en utilisant des Actions pour configurer l'environnement, installer les dépendances et exécuter les tests.

