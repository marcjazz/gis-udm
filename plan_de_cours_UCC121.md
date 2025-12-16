# Fiche Signalétique du Cours : UCC121 - Linux Expert

## Titre Complet
**UCC121 : Automatisation et IA pour l'Administration Système (Préparation LPIC-102)**

## Prérequis
- **UCC111** ou connaissances équivalentes : maîtrise de la ligne de commande Linux (navigation, gestion de fichiers, commandes de base).

## Durée Totale
- **12 heures** (8 sessions de 1h30).

## Objectifs Pédagogiques
À l'issue de ce cours, les participants seront capables de :
1.  **Maîtriser le shell Bash** pour créer des scripts d'automatisation complexes.
2.  **Personnaliser leur environnement** de travail pour gagner en efficacité.
3.  Interagir avec des bases de données en utilisant des **commandes SQL fondamentales**.
4.  **Intégrer des outils d'Intelligence Artificielle** pour assister et accélérer les tâches d'administration.
5.  **Analyser des logs** et **générer du code** de manière assistée par l'IA.

## Compétences Visées
- Automatisation de tâches répétitives via des scripts shell (Bash).
- Manipulation de chaînes de caractères, de fichiers et de processus.
- Gestion de données structurées avec SQL via la ligne de commande.
- Utilisation d'assistants IA en ligne de commande pour la résolution de problèmes.
- Conception de solutions de surveillance et d'analyse proactives.

## Mode d’Évaluation
- **Contrôles Continus (CC)** : Évaluation des travaux pratiques à chaque session.
- **Projet Final** : Création d'un script d'administration complet intégrant plusieurs concepts du cours.
- **Examen Final** : QCM et questions courtes sur l'ensemble des matières.

---

# Déroulement des 8 Sessions (1h30 par session)

## Session 1 : Maîtrise de l'Environnement Shell
- **Leçon (45 min)** :
    - Présentation du shell Bash et de son rôle.
    - Personnalisation du `~/.bashrc` et `~/.profile`.
    - Création d'alias pour les commandes fréquentes.
    - Introduction aux fonctions shell simples.
    - Variables d'environnement : `PATH`, `HOME`, `PS1`.
- **TP / CC (45 min)** :
    - Créer des alias pour `ls -la`, `grep --color=auto`, etc.
    - Écrire une fonction qui combine `mkdir` et `cd`.
    - Personnaliser le prompt (PS1) pour afficher le répertoire, l'heure et le nom d'utilisateur.

## Session 2 : Les Fondamentaux du Scripting Shell
- **Leçon (45 min)** :
    - Anatomie d'un script : shebang `#!/bin/bash`, commentaires, permissions (`chmod +x`).
    - Les variables : déclaration, affectation, lecture (`read`).
    - Les guillemets : simples (`'`), doubles (`"`) et `backticks` (``).
    - Substitution de commandes : `$(...)`.
    - Paramètres positionnels : `$1`, `$2`, `$@`, `$#`.
- **TP / CC (45 min)** :
    - Écrire un script qui accepte un nom en paramètre et affiche "Bonjour, [nom]".
    - Créer un script qui demande à l'utilisateur son nom et son âge et les affiche.
    - Script simple de sauvegarde : copier un fichier donné en paramètre vers un dossier `backup/` avec un timestamp.

## Session 3 : Structures de Contrôle et Boucles
- **Leçon (45 min)** :
    - Tests et conditions : `if`, `else`, `elif` et l'opérateur `[[ ... ]]`.
    - Conditions sur les fichiers (`-f`, `-d`) et les chaînes.
    - Logique `case`.
    - Boucles : `for` (sur des listes, des séquences), `while` (lecture de fichiers ligne par ligne), `until`.
- **TP / CC (45 min)** :
    - Améliorer le script de sauvegarde pour vérifier si le fichier source existe avant de le copier.
    - Écrire un script qui parcourt tous les fichiers `.log` d'un répertoire et les archive dans un fichier `tar.gz`.

## Session 4 : Gestion de Données avec SQL
- **Leçon (45 min)** :
    - Introduction aux bases de données relationnelles.
    - Installation et utilisation de `sqlite3` en ligne de commande.
    - Commandes SQL de base :
        - `CREATE TABLE`
        - `INSERT INTO`
        - `SELECT ... FROM ... WHERE`
        - `UPDATE` et `DELETE`
- **TP / CC (45 min)** :
    - Créer une base de données `inventaire.db` avec une table `materiel` (id, nom, quantite).
    - Écrire un script shell qui permet d'ajouter un nouvel item, de lister tous les items ou de modifier une quantité en interrogeant la base `sqlite3`.

## Session 5 : Introduction à l'IA en Ligne de Commande
- **Leçon (45 min)** :
    - Concept des assistants IA pour le CLI (ex: GitHub Copilot for CLI, `tldr` amélioré).
    - Comment formuler une bonne question ("prompt engineering" pour le CLI).
    - Cas d'usage : expliquer une commande complexe (`awk`, `sed`, `find`), trouver la bonne commande pour une tâche, générer des `one-liners`.
- **TP / CC (45 min)** :
    - Utiliser un assistant IA pour "traduire" en langage naturel la commande `find . -type f -name "*.tmp" -delete`.
    - Demander à l'IA de générer une commande pour trouver les 10 plus gros fichiers du système.
    - Demander à l'IA d'expliquer la différence entre `grep`, `egrep` et `fgrep`.

## Session 6 : Génération de Scripts et Analyse de Logs Assistées par IA
- **Leçon (45 min)** :
    - Génération de scripts complets à partir d'un prompt détaillé.
    - Itérer avec l'IA pour affiner et corriger un script généré.
    - Analyse de logs : soumettre un extrait de log (`/var/log/auth.log`, log Nginx...) et demander à l'IA de :
        - Détecter les erreurs.
        - Résumer l'activité.
        - Extraire des informations spécifiques (ex: adresses IP uniques).
- **TP / CC (45 min)** :
    - Faire générer par l'IA un script de surveillance qui vérifie l'espace disque et envoie un email si un seuil est dépassé.
    - Fournir un extrait de log Nginx à l'IA et lui demander de lister toutes les erreurs 404.

## Session 7 : Automatisation Avancée et Surveillance Prédictive
- **Leçon (45 min)** :
    - Planification de tâches avec `cron`.
    - Introduction à la surveillance prédictive : comment l'IA peut analyser des séries temporelles (usage CPU, RAM) pour anticiper des pannes. (Conceptuel)
    - Stratégies d'automatisation robustes : gestion des erreurs, logging.
    - **Présentation du projet final**.
- **TP / CC (45 min)** :
    - Planifier (avec `crontab -e`) l'exécution du script de sauvegarde (de la session 3) tous les soirs à 23h.
    - Brainstorming et début de conception du projet final.

## Session 8 : Atelier Projet Final et Révision
- **Leçon (30 min)** :
    - Révision des concepts clés du cours.
    - Session de questions-réponses ouvertes.
    - Bonnes pratiques et prochaines étapes pour devenir un expert Linux.
- **TP / CC (60 min)** :
    - Les étudiants travaillent sur leur projet final.
    - Le formateur passe du temps avec chaque étudiant pour débloquer des problèmes et donner des conseils.
    - Dépôt des projets à la fin de la session.

---

# Idée de Projet Final

**Titre :** Script de Reporting Quotidien Intelligent

**Objectif :** Créer un script Bash unique, `rapport.sh`, qui, lorsqu'il est exécuté, génère un rapport de santé du système et l'envoie par email.

**Fonctionnalités requises :**
1.  **Santé du système :** Le rapport doit inclure :
    - L'espace disque utilisé.
    - L'utilisation de la mémoire RAM.
    - La charge CPU (`uptime`).
2.  **Analyse de sécurité :** Le script doit analyser `/var/log/auth.log` pour lister les 5 dernières tentatives de connexion échouées. **(Utiliser l'IA pour générer la commande `grep`/`awk` appropriée peut faire partie du défi).**
3.  **Base de données :** Le script doit se connecter à la base de données `inventaire.db` (créée en session 4) et lister les items dont la quantité est inférieure à 5.
4.  **Rapport :** Toutes ces informations doivent être formatées dans un fichier texte clair.
5.  **Exécution :** Le script doit être conçu pour être exécuté via une tâche `cron`.
