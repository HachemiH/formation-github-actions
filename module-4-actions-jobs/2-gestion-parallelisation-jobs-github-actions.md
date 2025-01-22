# Module 4.2 : Gestion et Parallélisation des Jobs


<blockquote>
  <h2>Prérequis</h2>
  <p>Pour tirer le meilleur parti de ce chapitre vous devriez avoir :</p>
  <ul>
    <li>Une compréhension de base des concepts d'intégration continue (CI) et de déploiement continu (CD).</li>
    <li>Une familiarité avec GitHub, y compris la création et la gestion de dépôts.</li>
    <li>Des connaissances de base en YAML et en scripting, pour la rédaction et la configuration de workflows GitHub Actions.</li>
    <li>Une expérience préalable en développement logiciel, notamment en ce qui concerne le processus de construction, de test, et de déploiement d'applications.</li>
  </ul>
</blockquote>

<blockquote>
  <h2>Objectif Pédagogique</h2>
  <p>À la fin de ce chapitre vous serez capable de :</p>
  <ul>
    <li>Comprendre et appliquer les principes de gestion des jobs dans un environnement CI/CD en utilisant GitHub Actions, en se concentrant sur la définition d'objectifs clairs pour chaque job et l'orchestration de ces jobs à travers des dépendances explicites.</li>
    <li>Concevoir des workflows optimisés par la parallélisation des jobs et des tâches, en utilisant des matrices pour exécuter simultanément plusieurs instances d'un job dans différentes conditions, afin de réduire le temps total nécessaire à l'exécution du workflow.</li>
  </ul>
</blockquote>



## 4.2.1 Gestion des Jobs

Dans un processus d'intégration et de déploiement continus (CI/CD), la gestion des jobs est essentielle pour orchestrer les différentes tâches nécessaires à la préparation et au déploiement d'une application. Un job peut être vu comme une unité de travail ou une tâche individuelle qui fait partie d'un ensemble plus vaste d'opérations dans un workflow.


### Structuration des Jobs dans un Workflow

La structuration des jobs dans un workflow nécessite une attention particulière pour maximiser l'efficacité et la clarté du processus CI/CD. Voici comment procéder :

- **Définir des Jobs Indépendants :** Chaque job doit avoir un objectif clair et se concentrer sur une tâche spécifique, telle que construire, tester, ou déployer l'application. Cela simplifie non seulement le suivi de chaque étape mais facilite également la maintenance et les ajustements futurs du workflow.

- **Utiliser des Dépendances :** Les dépendances entre jobs permettent de créer un flux d'exécution ordonné et logique, où certains jobs doivent être terminés avant que d'autres puissent débuter. Cela est crucial pour maintenir l'intégrité et la fiabilité du processus de déploiement.

#### Exemple d'Utilisation des Dépendances

Supposons que vous ayez trois jobs principaux dans votre workflow : `build`, `test`, et `deploy`. Voici comment vous pourriez structurer ces jobs en utilisant des dépendances pour s'assurer qu'ils s'exécutent dans l'ordre correct :

```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
    - name: Build step
      run: echo "Executing build steps here..."

  test:
    needs: build
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
    - name: Test step
      run: echo "Executing tests here..."

  deploy:
    needs: test
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
    - name: Deploy step
      run: echo "Deploying application here..."
```

Dans cet exemple, le job `test` n'est pas lancé tant que le job `build` n'est pas terminé avec succès. De même, le job `deploy` attend la réussite du job `test` avant de commencer. Cette approche assure que votre application est construite et testée avant tout déploiement, minimisant les risques d'erreurs ou de problèmes dans l'environnement de production.

En structurant les jobs de cette manière, vous bénéficiez d'une orchestration fluide et logique de vos tâches CI/CD, garantissant que chaque étape est exécutée sur des fondations solides et vérifiées.


## 4.2.2 Parallélisation des Jobs

La parallélisation implique l'exécution simultanée de multiples jobs ou étapes pour réduire le temps total nécessaire à l'exécution d'un workflow.

### Application de la Parallélisation

- **Diviser pour Conquérir :** Séparez les tests ou les tâches en plusieurs jobs pouvant s'exécuter en parallèle.
- **Utiliser des Matrices :** Exécutez le même job sous différentes configurations en parallèle. Cela est particulièrement utile pour les tests sur plusieurs versions d'un langage de programmation ou sur différents systèmes d'exploitation.

### Exemple de Parallélisation avec une Matrice

```yaml
jobs:
  test:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        node-version: [12.x, 14.x, 16.x]
    steps:
    - uses: actions/checkout@v2
    - name: Utiliser Node.js ${{ matrix.node-version }}
      uses: actions/setup-node@v2
      with:
        node-version: ${{ matrix.node-version }}
    - run: npm test
```

Ce snippet démontre comment exécuter des tests en parallèle pour différentes versions de Node.js, en utilisant la fonctionnalité de matrice de GitHub Actions.


## Résumé

La gestion des jobs dans un workflow CI/CD repose sur deux concepts clés : **la dépendance entre jobs** et **la parallélisation**. 

- **Dépendance entre jobs :** Permet d'orchestrer l'ordre d'exécution des jobs, en s'assurant qu'un job ne démarre que lorsque les jobs dont il dépend ont été complétés avec succès. Cela garantit que les tâches sont réalisées dans une séquence logique et ordonnée.

- **Parallélisation :** Optimise le temps d'exécution du workflow en permettant l'exécution simultanée de plusieurs jobs ou étapes qui ne dépendent pas les uns des autres. La parallélisation est efficace pour les tests qui peuvent être segmentés ou pour les tâches pouvant s'exécuter indépendamment, réduisant ainsi le temps global nécessaire pour le processus CI/CD.

