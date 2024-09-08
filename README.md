# Pipeline Sécurisé avec SonarQube et Jenkins

Ce projet implémente un pipeline CI/CD sécurisé pour l'analyse automatisée du code source en utilisant Jenkins et SonarQube. L'objectif est de garantir la qualité du code, identifier les vulnérabilités et s'assurer de la conformité aux bonnes pratiques de développement.

# Architecture du Pipeline

Le pipeline inclut les étapes suivantes :

    Clonage du dépôt Git : Le code source est extrait du dépôt Git.
    Compilation et Tests : Le code est compilé et les tests unitaires sont exécutés.
    Analyse avec SonarQube : Le code est soumis à une analyse statique par SonarQube pour détecter les bugs, vulnérabilités, et mauvaises pratiques.
    Reporting et Validation : SonarQube génère un rapport de qualité. Si des seuils critiques sont dépassés, le pipeline échoue.
