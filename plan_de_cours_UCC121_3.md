# Plan de Cours Détaillé : UCC121

# 2. UCC121-3 : AI In Administrative Tasks

## Fiche Signalétique
- **Titre :** AI In Administrative Tasks
- **Code :** UCC121-3
- **Prérequis :** **UCC121-1**. Solides compétences en scripting shell.
- **Durée :** 12 heures (8 sessions de 1h30).
- **Objectifs :**
    - Utiliser des assistants IA pour accélérer la résolution de problèmes et la génération de code.
    - Appliquer l'IA à des cas d'usage concrets : analyse de logs, sécurité, surveillance.
    - Comprendre les principes du "prompt engineering" adapté aux tâches système.
- **Évaluation :** Contrôles continus (TP), projet, examen final.

## Déroulement des 8 Sessions

### Session 1 : Introduction à l'IA pour l'Administration Système
- **Leçon :** Qu'est-ce qu'un LLM ? Panorama des outils d'IA pour le CLI. Potentiel, limites et considérations éthiques.
- **TP/CC :** Installation et configuration d'un outil (ex: GitHub Copilot for CLI). Premiers prompts simples.

### Session 2 : Génération et Explication de Commandes
- **Leçon :** L'art du "prompting" : comment traduire un besoin en une requête IA efficace. Cas d'usage : "expliquer cette commande", "trouver la commande pour...".
- **TP/CC :** Série de défis à résoudre en utilisant l'IA pour trouver et comprendre des commandes complexes (`find`, `rsync`, `iptables`).

### Session 3 : Génération de Scripts Assistée par IA
- **Leçon :** De la commande simple au script complet. Comment spécifier à l'IA la logique, la gestion des erreurs et le format de sortie souhaité.
- **TP/CC :** Générer un script qui automatise la création de nouveaux utilisateurs (avec validation des entrées).

### Session 4 : Affinage et Débogage de Code avec l'IA
- **Leçon :** Utiliser l'IA comme un partenaire de "pair programming". Soumettre un script existant pour l'améliorer, le refactoriser ou le déboguer.
- **TP/CC :** Prendre un script simple et demander à l'IA d'y ajouter la journalisation, une meilleure gestion des erreurs, et des commentaires.

### Session 5 : Analyse de Logs Augmentée par l'IA
- **Leçon :** Stratégies pour analyser de grands volumes de logs. Prompts pour la détection d'anomalies, la synthèse d'activité, et la corrélation d'événements.
- **TP/CC :** Analyser un log `auth.log` pour produire un rapport de sécurité (tentatives de brute-force, connexions réussies par utilisateur).

### Session 6 : IA pour la Configuration et la Sécurité
- **Leçon :** Générer des fichiers de configuration (Nginx, Apache, SSH). Auditer une configuration existante avec l'IA pour identifier les failles de sécurité potentielles.
- **TP/CC :** Générer une configuration Nginx sécurisée pour un site web statique. Demander à l'IA d'analyser `sshd_config` et de suggérer des améliorations.

### Session 7 : Concepts de Surveillance Prédictive
- **Leçon :** Introduction à l'AIOps. Comment l'IA peut analyser des métriques (CPU, RAM) pour anticiper des problèmes. Concevoir des alertes intelligentes.
- **TP/CC :** Utiliser l'IA pour écrire le script de collecte de métriques. Discuter avec l'IA des stratégies d'analyse de ces données.

### Session 8 : Projet de Synthèse et Avenir de l'IA
- **Leçon :** Réflexion sur l'évolution du métier d'administrateur système.
- **TP/CC :** Atelier dédié à un projet final combinant scripting et IA (ex: un outil de diagnostic système intelligent) et présentation des résultats.
