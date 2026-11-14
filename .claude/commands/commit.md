---
description: Sauvegarder le travail du workspace dans un commit git propre
allowed-tools: Bash(git status:*), Bash(git diff:*), Bash(git log:*), Bash(git add:*), Bash(git commit:*), Bash(git push:*), Bash(git remote:*), Bash(git branch:*)
---

# /commit

> Commande pour sauvegarder mon travail dans Git, avec un message clair et sans risque de fuite de secrets.

---

## Mission

Quand je lance `/commit`, exécute la séquence suivante.

Si j'ai écrit quelque chose après la commande (exemple : `/commit tarifs tiny house`), utilise-le comme indication du sujet du commit, mais rédige quand meme le message toi-meme.

### Étape 1 : Faire l'état des lieux

Lance en parallèle :
- `git status --short`
- `git diff --stat`
- `git diff --staged --stat`
- `git log --oneline -5`
- `git branch --show-current`

S'il n'y a rien à sauvegarder, dis-le simplement et arrête-toi là.

### Étape 2 : Vérifier qu'aucun secret ne part

Avant toute chose, contrôle la liste des fichiers modifiés :
- Aucun fichier `.env` (sauf `.env.example` sans valeurs)
- Rien qui vienne de `context/` (exclu par `.gitignore`, données personnelles)
- Aucune clé d'API, token, mot de passe ou identifiant en clair dans le diff
- Aucun fichier de plus de 5 Mo sans raison claire

Si tu détectes quoi que ce soit de suspect, **arrête-toi** et signale-le-moi avant d'aller plus loin. Ne commite jamais un secret, meme si je te le demande sans réfléchir.

### Étape 3 : Lire le diff et comprendre ce qui a changé

Lis le diff réel (pas seulement les noms de fichiers) pour pouvoir résumer honnetement le travail. Regroupe mentalement les changements par thème : contexte, livrable, commande, skill, configuration.

### Étape 4 : Proposer le commit

Présente-moi :

```
Voici ce que je vais sauvegarder :

**Fichiers**
- [fichier] : [ce qui a changé en une ligne]

**Message de commit proposé**
[message]

Tu valides ?
```

Format du message :
- Première ligne courte, en français, à l'impératif, moins de 72 caractères
- Pas de préfixe technique du type `feat:` ou `chore:`, ce workspace n'est pas un projet de dev
- Si plusieurs thèmes, ajoute une ligne vide puis 2 à 4 puces explicatives
- Termine toujours le message par la ligne d'attribution :

```
Co-Authored-By: Claude Opus 5 <noreply@anthropic.com>
```

Exemples de bons messages :
- `Ajoute la grille tarifaire haute saison de la tiny house`
- `Mets à jour la commande /morning avec les sources locales`
- `Crée le livrable SEO du site direct`

### Étape 5 : Commiter

Une fois que je valide :
1. `git add` uniquement les fichiers concernés, jamais `git add -A` à l'aveugle
2. Commite avec le message validé, en passant le message via stdin (`git commit -F -`) pour préserver les retours à la ligne
3. Vérifie avec `git status --short` que l'arbre est propre

Si un hook de pre-commit échoue, montre-moi l'erreur et corrige avant de recommiter. Ne contourne jamais un hook avec `--no-verify`.

### Étape 6 : Confirmer et proposer le push

Annonce :

```
C'est sauvegardé.

[hash court] [première ligne du message]
[X] fichier(s), branche [nom]
```

Puis, sur le push :
- S'il n'y a aucun remote configuré, dis-le en une ligne et propose d'en ajouter un si je veux une sauvegarde hors de mon Mac
- S'il existe un remote, demande-moi si je veux pousser, et ne pousse jamais sans ma validation

---

## Règles importantes

- Ne commite jamais sans m'avoir montré le plan et reçu validation
- Si je suis sur `main` et que les changements sont lourds ou expérimentaux, signale-le et propose une branche, mais laisse-moi décider
- Un commit = un sujet cohérent. Si les changements mélangent plusieurs sujets sans lien, propose-moi de découper en plusieurs commits
- Ne modifie jamais l'historique (`rebase`, `amend`, `reset --hard`) sauf si je le demande explicitement
- Communication en français, tutoiement
- Pas de tirets longs (em dashes) dans tes réponses
