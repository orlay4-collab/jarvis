# Audit et refonte de la plaquette commerciale VGsoluce

**Date :** 27 novembre 2026
**Contexte :** un ami de Philippe lance VGsoluce (visibilité Google, avis clients, plaques NFC pour commerces locaux) et demande un avis sur sa plaquette commerciale.

## Contenu du dossier

| Fichier | Rôle |
|---|---|
| `AUDIT.md` | L'audit complet : ce qui fonctionne, les incohérences bloquantes, les manques de l'argumentaire, et le détail de ce qui a été corrigé. |
| `Plaquette-VGsoluce-2026-11.pdf` | **Le livrable.** Nouvelle plaquette, 2 pages A4, imprimable recto-verso. |
| `plaquette.html` | Le source. C'est ce fichier qu'on modifie pour mettre la plaquette à jour. |
| `qr.svg` | Le QR code vers `vgsoluce.fr`, intégré dans le HTML. |

## Régénérer le PDF après modification

```bash
cd "livrables/2026-11-27_audit-plaquette-vgsoluce"
"/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" \
  --headless --disable-gpu --no-pdf-header-footer \
  --print-to-pdf="Plaquette-VGsoluce-2026-11.pdf" \
  "file://$PWD/plaquette.html"
```

Pour changer l'adresse du QR code, modifier l'URL puis régénérer :

```bash
python3 -c "
import qrcode
q=qrcode.QRCode(error_correction=qrcode.constants.ERROR_CORRECT_M,border=1)
q.add_data('https://vgsoluce.fr'); q.make(fit=True)
m=q.get_matrix(); n=len(m); parts=[]
for y,row in enumerate(m):
    x=0
    while x<n:
        if row[x]:
            x2=x
            while x2<n and row[x2]: x2+=1
            parts.append('M%d %dh%dv1h-%dz'%(x,y,x2-x,x2-x)); x=x2
        else: x+=1
print('<svg xmlns=\"http://www.w3.org/2000/svg\" viewBox=\"0 0 %d %d\" shape-rendering=\"crispEdges\"><path fill=\"#1d1d1f\" d=\"%s\"/></svg>'%(n,n,''.join(parts)))
" > qr.svg
```

puis remplacer le bloc `<svg>` dans `plaquette.html` à l'intérieur de `<div class="box">`.

## Avant diffusion : quatre champs à remplir

Dans `plaquette.html`, page 2 :

1. `[06 XX XX XX XX]` → le vrai numéro
2. `SIRET [à compléter]` → le vrai SIRET
3. Créer réellement l'adresse `contact@vgsoluce.fr` (elle figure dans le PDF à la place de l'adresse Gmail)
4. Vérifier que `vgsoluce.fr` est en ligne avant de diffuser le QR code

La liste complète est à la fin de `AUDIT.md`, section 6.

## Décisions prises avec Philippe

- **Grille tarifaire corrigée** plutôt que reprise à l'identique : l'originale rendait la formule « Liberté » strictement perdante. Nouveaux montants proposés : Essentiel 39 €/mois sans engagement, Sérénité 59 €/mois tout compris. **À valider par le porteur du projet.**
- **Phase de lancement, zéro client** : toute la preuve sociale inventée a été retirée et remplacée par quatre engagements écrits.
- **Format 2 pages A4**, même volume d'information que l'original mais hiérarchisé.
