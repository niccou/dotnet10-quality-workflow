# dotnet10-quality-workflow

Repo de démo .NET 10 (LTS) sous GitHub Codespaces : tests unitaires en NUnit + "quality workflow" shift-left via pre-commit (Python) pour lancer format/analyzers/tests avant commit, et CI GitHub Actions pour garantir un code propre et reproductible.

## Structure du projet

```
dotnet10-quality-workflow/
├── src/
│   └── App/                    # Minimal API .NET 10
├── tests/
│   └── App.Tests/              # Tests NUnit
├── .devcontainer/
│   └── devcontainer.json       # Configuration GitHub Codespaces
├── .github/
│   └── workflows/
│       └── dotnet.yml          # CI GitHub Actions
├── .editorconfig               # Configuration du formatage de code
├── .pre-commit-config.yaml     # Hooks pre-commit
└── DotNet10QualityWorkflow.sln # Solution .NET
```

## Prérequis

- .NET 10 SDK
- Python 3.x (pour pre-commit)
- pip (pour installer pre-commit)

## Démarrage rapide

### 1. Cloner le dépôt

```bash
git clone https://github.com/niccou/dotnet10-quality-workflow.git
cd dotnet10-quality-workflow
```

### 2. Restaurer les dépendances

```bash
dotnet restore
```

### 3. Compiler le projet

```bash
dotnet build
```

### 4. Exécuter les tests

```bash
dotnet test
```

### 5. Exécuter l'API

```bash
cd src/App
dotnet run
```

L'API sera disponible à `http://localhost:5179` ou `https://localhost:7170`.

## Configuration du Quality Workflow

### Installation de pre-commit

```bash
pip install pre-commit
pre-commit install
```

Les hooks suivants seront exécutés automatiquement avant chaque commit :
- `dotnet format --verify-no-changes` : Vérifie le formatage du code
- `dotnet test` : Exécute les tests unitaires

### Exécuter les hooks manuellement

```bash
pre-commit run --all-files
```

### Formatage du code

Pour formater automatiquement votre code :

```bash
dotnet format
```

Pour vérifier le formatage sans modifier les fichiers :

```bash
dotnet format --verify-no-changes
```

## GitHub Codespaces

Ce projet est configuré pour fonctionner avec GitHub Codespaces. Ouvrez simplement le dépôt dans Codespaces et l'environnement sera configuré automatiquement avec :
- .NET 10 SDK
- Python 3.12
- pre-commit installé et configuré
- Extensions VS Code recommandées

## CI/CD GitHub Actions

Le workflow CI s'exécute sur chaque push et pull request vers la branche `main` et effectue :
1. Restauration des dépendances (`dotnet restore`)
2. Compilation du projet (`dotnet build`)
3. Exécution des tests (`dotnet test`)
4. Vérification du formatage (`dotnet format --verify-no-changes`)

## Configuration

### .editorconfig

Le fichier `.editorconfig` définit les conventions de codage pour garantir la cohérence du code :
- Indentation avec espaces (4 pour C#)
- Style de code C# avec règles de nommage
- Préférences pour l'utilisation de `var`, les expressions, etc.
- Règles d'analyse du code .NET

### Analyzeurs

Les projets utilisent `Microsoft.CodeAnalysis.NetAnalyzers` pour l'analyse statique du code et l'application des meilleures pratiques .NET.

## Contribuer

1. Créez une branche pour votre fonctionnalité
2. Assurez-vous que tous les tests passent
3. Assurez-vous que le code est formaté correctement
4. Soumettez une pull request

Les hooks pre-commit garantissent que le code respecte les standards avant le commit, et le CI vérifie que tout fonctionne correctement avant la fusion.
