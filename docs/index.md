# Plan de Cours Détaillé : UCC121

# 1. UCC121-1 : Shells, Scripting, and Data Management

## Fiche Signalétique
- **Titre :** Shells, Scripting, and Data Management
- **Code :** UCC121-1
- **Prérequis :** Maîtrise de la ligne de commande Linux de base (UCC111 ou équivalent).
- **Durée :** 12 heures (8 sessions de 1h30).
- **Objectifs :**
    - Maîtriser les outils avancés de la ligne de commande.
    - Créer des scripts shell robustes et modulaires pour l'automatisation.
    - Manipuler des données textuelles et interagir avec une base de données simple.
- **Évaluation :** Contrôles continus (TP), projet de scripting, examen final.

## Déroulement des 8 Sessions

### Session 1 : Maîtrise de l'Environnement Shell
- **Leçon :** Fondamentaux du shell Bash, personnalisation du `.bashrc`, gestion des alias, des fonctions et des variables d'environnement (`PATH`, `PS1`).
- **TP/CC :** Créer des alias utiles, écrire une fonction pour automatiser une tâche simple (ex: `mkcd`), personnaliser son prompt.

### Session 2 : Outils de Traitement de Texte : `grep`, `sed`, `awk`
- **Leçon :** Introduction aux expressions régulières. Utilisation de `grep` pour la recherche, `sed` pour la substitution, et `awk` pour l'extraction de colonnes.
- **TP/CC :** Extraire toutes les adresses IP d'un fichier de log. Remplacer une chaîne de caractères dans une série de fichiers de configuration.

### Session 3 : Fondamentaux du Scripting Bash
- **Leçon :** Anatomie d'un script (shebang, permissions), variables, lecture de l'entrée utilisateur (`read`), gestion des paramètres (`$1`, `$@`), substitution de commande `$(...)`.
- **TP/CC :** Écrire un script qui prend un nom de fichier en paramètre et en affiche les 3 premières lignes.

### Session 4 : Logique et Structures de Contrôle
- **Leçon :** Conditions `if/elif/else`, tests sur fichiers et chaînes `[[ ... ]]`. Logique `case`. Gestion des codes de retour (`$?`).
- **TP/CC :** Écrire un script qui vérifie si un utilisateur existe dans `/etc/passwd`.

### Session 5 : Les Boucles et l'Itération
- **Leçon :** Boucles `for` (sur des listes, des séquences, des fichiers), `while` (pour lire un fichier ligne par ligne), et `until`.
- **TP/CC :** Écrire un script qui renomme en masse tous les fichiers `.jpeg` d'un dossier en `.jpg`.

### Session 6 : Fonctions et Modularité
- **Leçon :** Déclarer et appeler des fonctions, portée des variables (locales/globales), passer des arguments et retourner des valeurs. Sourcer des fichiers de fonctions.
- **TP/CC :** Transformer un script monolithique en un script modulaire utilisant des fonctions.

### Session 7 : Introduction à la Gestion de Données avec SQL
- **Leçon :** Principes des BDD relationnelles. Utilisation de `sqlite3` pour `CREATE TABLE`, `INSERT`, `SELECT`, `UPDATE`, `DELETE`.
- **TP/CC :** Créer une base de données simple pour un inventaire et écrire un script shell pour l'interroger.

### Session 8 : Gestion des Processus et Automatisation avec `cron`
- **Leçon :** Gestion des tâches de fond (`&`, `jobs`, `fg`, `bg`, `nohup`). Planification de tâches avec `cron`.
- **TP/CC :** Lancer un script en tâche de fond. Planifier un script de sauvegarde pour qu'il s'exécute toutes les nuits.

