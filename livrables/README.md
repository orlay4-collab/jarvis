# livrables/

Ce dossier contient tout ce que Claude produit pour moi.

## La règle d'or

| Type | Dossier | Exemples |
|---|---|---|
| **Inputs**, les documents que je fournis à Claude | `context/import/` | PDF, exports Smoobu, captures, notes, contrats |
| **Outputs**, ce que Claude produit pour moi | `livrables/` | sites, scripts, briefs, rapports, présentations |

On ne mélange jamais les deux. Un document que je fournis ne va pas dans `livrables/`, et un livrable produit par Claude ne va pas dans `context/import/`.

## Organisation

| Sous-dossier | Contenu |
|---|---|
| `sites-web/` | Sites internet, pages, maquettes, code injecté |
| `applications/` | Outils, scripts, automatisations |
| `tiny-house/` | Exploitation de La Parenthèse : tarifs, rentabilité, fiscalité, voyageurs, offres avec Nadia |
| `instagram/` | Reels, captions, carrousels, stories et plans de publication pour @tinyhousebba_ |

Si un livrable ne rentre dans aucune catégorie, on en parle avant de créer un nouveau sous-dossier.

## Convention de nommage des projets

Chaque projet a son propre dossier dans le sous-dossier thématique :

```
AAAA-MM-JJ_nom-du-projet/
```

- **Date de création** au format ISO, pour que les projets se trient dans l'ordre chronologique
- **Nom en minuscules**, mots séparés par des tirets, sans accents, sans espaces
- **Un README.md à l'intérieur** pour les projets de plus d'un fichier : objectif, état, comment l'utiliser

Exemples :

```
livrables/sites-web/2026-11-13_page-offre-directe/
livrables/applications/2026-11-20_export-smoobu-mensuel/
livrables/tiny-house/2027-01-05_grille-tarifaire-2027/
livrables/instagram/2026-11-14_reel-pas-a-deux/
```

Les versions successives d'un même fichier se suffixent `-v1`, `-v2`, etc. Pas de `final`, `final2` ni `definitif`.

## Sécurité

Aucune clé d'API, aucun mot de passe ni aucun code d'accès en clair dans un livrable. Les secrets vivent uniquement dans `.env` à la racine du workspace.
