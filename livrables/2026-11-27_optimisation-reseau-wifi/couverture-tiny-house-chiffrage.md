# Couverture Internet de la tiny house et de l'institut, chiffrage des options

Établi le 27 novembre 2026, après le diagnostic réseau du même jour.

> **Avertissement sur les montants.** Ce sont des ordres de grandeur de prix
> publics constatés, destinés à arbitrer entre les options. Ce ne sont pas des
> devis. Les montants exacts dépendent de la distance réelle, de la nature du
> sol et de ce que tu fais toi-même.

---

## ⚠️ RÉVISION : TROIS POINTS À DESSERVIR, PAS UN

Information arrivée en fin de session, qui change le périmètre du chantier.

Le répéteur ne couvre pas seulement la tiny house. Il couvre aussi
**l'institut de Nadia, où se trouve son appareil LPG, qui est son outil de
travail**, parce que le signal de la Freebox ne porte pas jusque là.

| Point | Usage | Criticité |
|---|---|---|
| Maison | usage personnel, poste de travail | résolu le 27 novembre 2026 |
| Tiny house | voyageurs, dont travailleurs nomades | revenus locatifs, risque d'avis |
| **Institut** | **appareil LPG de Nadia** | **activité professionnelle** |

### Trois conséquences

**1. Le répéteur ne se débranche pas, il se remplace.** Toute coupure arrête
l'institut. L'infrastructure de remplacement s'installe d'abord, le répéteur
part ensuite.

**2. Le projet change de nature.** Ce n'était qu'un sujet de confort voyageur,
c'est désormais une dépendance d'activité professionnelle. Un appareil LPG
communique pour ses mises à jour, la validation de ses droits d'usage et la
télémaintenance. Le double NAT actuel est particulièrement hostile à la
télémaintenance, et un lien à 3,7 Mbps montant avec des pointes à 330 ms peut
faire échouer une validation en pleine séance cliente. **À vérifier aussi : la
date affichée par l'appareil LPG.** Le répéteur a son horloge bloquée au
1er janvier 1970, et une date fausse fait refuser les connexions sécurisées.

**3. L'appareil LPG partage aujourd'hui son réseau avec les voyageurs.** Sans
aucune isolation. Un équipement professionnel ne devrait pas se trouver sur le
même segment que des inconnus de passage. C'est le second argument, après la
protection de tes données personnelles, en faveur du réseau invités.

### Ce que cela change au chiffrage

L'infrastructure devient une desserte à trois branches. Deux architectures
possibles :

**Architecture en étoile.** Une liaison depuis la maison vers chaque point.
Simple à comprendre, mais deux tranchées.

**Architecture en chaîne**, généralement préférable. Une seule liaison vers le
point le plus proche, un petit commutateur réseau sur place, puis une seconde
liaison vers le point suivant. Une seule tranchée si l'institut et la tiny
house sont dans la même direction, et un commutateur coûte 25 à 60 €.

Dans les deux cas, **la gaine en diamètre 40 avec un fil d'aiguillage devient
indispensable** : tu passeras probablement un second câble un jour.

Le surcoût par rapport au chiffrage ci-dessous, pour desservir le troisième
point : une longueur de câble supplémentaire, un commutateur à 25 à 60 €, et
une seconde borne d'accès si l'institut en a besoin, soit 70 à 250 €. Compte
**200 à 500 € de plus** selon la distance entre les deux points éloignés.

---

## ✅ SECONDE RÉVISION : L'INSTITUT EST UN PROBLÈME BIEN MOINS CHER QUE PRÉVU

Précisions apportées par Philippe : **l'institut est accolé ou très proche de
la maison, à moins de 30 m de la Freebox**, et aucun dysfonctionnement n'a été
signalé sur l'appareil LPG à ce jour.

Le dossier se scinde donc en deux chantiers de nature et de coût très
différents.

| Chantier | Difficulté | Ordre de grandeur |
|---|---|---|
| **Institut**, moins de 30 m, accolé | faible | **0 à 60 €** |
| **Tiny house**, sous les chênes, distance inconnue | réelle | 300 à 750 € |

### L'hypothèse à tester avant de dépenser un euro

Ta liste de réseaux mémorisés contenait **sept variantes d'une ancienne
Freebox nommée `freeboxRPNQNN`**. Ce répéteur a donc très probablement été
installé à l'époque de cette box.

**Ta Freebox Ultra n'a rien à voir avec elle.** Plus d'antennes, plus de
puissance, Wi-Fi 7. Il est très possible que son signal natif atteigne
aujourd'hui l'institut sans aucun équipement supplémentaire, et que ce
répéteur ne soit plus qu'un vestige qui dégrade au lieu d'aider.

**Le test, gratuit et à faire en premier.** Avec un téléphone, va dans
l'institut, à l'endroit exact de l'appareil LPG. Connecte-toi non pas au
réseau du répéteur mais à **`Freebox-79B748`**, celui de la box. Puis regarde
si tu as du signal, et lance un test de débit.

- **Si tu as du signal correct** : le répéteur est inutile pour l'institut. Il
  suffit de brancher l'appareil LPG sur le réseau de la Freebox. **Coût : zéro.**
- **Si tu n'as rien ou presque** : passe aux options ci-dessous.

### Si le test est négatif, trois solutions à moins de 30 m

**Solution 1, un câble à travers un mur. 20 à 60 €, et c'est la meilleure.**

Si l'institut est accolé à la maison, tu n'as pas besoin de tranchée. Un
percement, un câble Ethernet catégorie 6 de 10 ou 20 m, une prise à chaque
bout. L'appareil LPG se retrouve en filaire, sur le réseau de la Freebox, sans
Wi-Fi, sans double NAT, sans répéteur.

Pour un outil de travail professionnel, **le filaire est toujours le bon
choix**. Ni feuillage, ni voisin, ni météo, ni temps d'antenne partagé. C'est
aussi ce qui débloquerait la télémaintenance.

**Solution 2, un Répéteur Wi-Fi Freebox. Quelques euros par mois.**

À moins de 30 m, un répéteur officiel fonctionne très bien. Contrairement au
boîtier actuel, il reste en mode pont, ne crée pas de second réseau, conserve
l'IPv6 et s'administre depuis Freebox OS. À vérifier dans ton espace abonné
Free pour le tarif exact de ton contrat.

**Solution 3, courant porteur en ligne. 60 à 120 €.**

Si l'institut est accolé, il est probablement sur le même compteur, ce qui est
la condition de réussite. À moins de 30 m, le débit est généralement bon.
Achète chez un revendeur qui reprend sous quinze jours, teste, renvoie si
c'est mauvais.

### Recommandation pour l'institut

**Solution 1, le câble à travers le mur.** C'est le moins cher, le plus fiable,
et le seul qui convienne vraiment à un équipement professionnel. Mais fais le
test gratuit d'abord : il se peut que tu n'aies rien à faire du tout.

### Ce que cela change pour la suite

Les chapitres qui suivent, tranchées, fibre optique, architecture en chaîne,
**ne concernent plus que la tiny house**. L'institut sort du périmètre coûteux.

La donnée qui manque maintenant est **la distance entre la Freebox et la tiny
house**. C'est elle, et elle seule, qui décide du budget restant.

---

## 💰 CHIFFRAGE FINAL : TINY HOUSE À 40 M

Distance confirmée par Philippe : **environ 40 m entre la Freebox et la tiny
house**. Tu es confortablement sous la limite des 100 m du cuivre, donc toutes
les options restent ouvertes et tu peux arbitrer sur le mérite, pas sur la
contrainte.

### ⚠️ À LIRE AVANT DE CREUSER : COORDONNE AVEC LE BAIN NORDIQUE

C'est le point le plus rentable de tout ce document.

Ton projet numéro 2 est l'installation d'un bain nordique Harvia, devis Spaleaz
en LOA, avec **une résistance électrique de 3 kW**. Cet équipement devra être
alimenté, et il sera selon toute vraisemblance installé à côté de la tiny
house, donc **au bout de la même tranchée de 40 m**.

**Creuser deux fois coûte deux fois.** Et la seconde tranchée se fera dans un
sol déjà remanié, en contournant la première gaine, sous les mêmes racines de
chênes.

**Fais une seule tranchée, avec plusieurs gaines :**

| Gaine | Usage | Remarque |
|---|---|---|
| Gaine 1, Ø40 rouge | alimentation électrique du bain nordique | section de câble à dimensionner par un électricien pour 3 kW sur 40 m |
| Gaine 2, Ø40 rouge | réseau, fibre optique | avec un fil d'aiguillage laissé dedans |
| Gaine 3, Ø40 vide | réserve | eau, seconde tiny house, éclairage de cheminement |

Les gaines se posent côte à côte dans la même tranchée, **avec un écart de
20 cm minimum entre l'électrique et le réseau**. Le surcoût de la troisième
gaine vide est de 70 à 115 €. C'est l'assurance la moins chère de ce dossier,
sachant que ton projet 8 est l'étude d'une seconde tiny house.

**Conséquence sur le calendrier.** Si le bain nordique se décide dans les mois
qui viennent, et le devis Spaleaz est de toute façon à faire réémettre, alors
il faut soit attendre pour creuser une seule fois, soit creuser maintenant en
posant dès à présent les gaines pour les deux usages. La seconde option est la
bonne : les gaines ne coûtent presque rien, et la tranchée est le poste cher.

**Un mot sur la saison.** Fin novembre est un bon moment pour creuser dans les
Bouches-du-Rhône. L'argile provençale en août se travaille comme du béton. Le
sol humide d'hiver est nettement plus facile.

### Les deux scénarios filaires, à 40 m

**Scénario A, fibre optique enterrée**

| Poste | Fourchette |
|---|---|
| Câble fibre optique préconnectorisé extérieur, 50 m | 100 à 150 € |
| Deux convertisseurs de média fibre vers Ethernet | 60 à 120 € |
| Gaine TPC annelée Ø40, 45 m | 70 à 115 € |
| Grillage avertisseur rouge, 45 m | 15 à 25 € |
| Borne d'accès Wi-Fi 6 alimentée par le câble réseau | 100 à 180 € |
| Injecteur d'alimentation sur câble réseau | 25 à 40 € |
| Coffret étanche et connectique | 30 à 60 € |
| Protection parafoudre réseau | **non nécessaire** |
| **Total matériel** | **400 à 690 €** |

**Scénario B, cuivre enterré**

| Poste | Fourchette |
|---|---|
| Câble Ethernet catégorie 6 extérieur gelé, 50 m | 60 à 90 € |
| Gaine TPC annelée Ø40, 45 m | 70 à 115 € |
| Grillage avertisseur rouge, 45 m | 15 à 25 € |
| Borne d'accès Wi-Fi 6 alimentée par le câble réseau | 100 à 180 € |
| Injecteur d'alimentation sur câble réseau | 25 à 40 € |
| Connectique et prises étanches, outillage de sertissage | 40 à 70 € |
| **Protection parafoudre réseau, aux deux extrémités** | **60 à 120 €** |
| **Total matériel** | **370 à 640 €** |

Dans les deux cas, ajoute la tranchée : **150 à 250 €** de location de machine
pour une journée si tu la fais toi-même, ou **600 à 1 200 €** si tu la fais
faire.

### Le verdict est net

**À 40 m, la fibre coûte le même prix que le cuivre, pour environ 30 € d'écart
au milieu de fourchette. Et elle est strictement meilleure.**

La raison est simple : la fibre économise exactement ce qu'elle coûte en plus.
Elle n'a pas besoin de parafoudre, à 60 à 120 €, et le câble fibre
préconnectorisé revient moins cher au mètre qu'un bon câble cuivre extérieur
gelé.

**Et elle apporte trois choses que le cuivre n'a pas :**

1. **Aucune conductivité.** Sous des chênes centenaires, qui sont les points
   hauts de ton terrain, un câble cuivre enterré entre deux bâtiments est un
   chemin pour la foudre. La fibre supprime le risque au lieu de le filtrer.
2. **Aucune limite de distance.** Si tu installes un jour une seconde tiny
   house plus loin, la même gaine et la même technologie suivent.
3. **Aucune sensibilité aux perturbations électriques**, ce qui compte quand
   une gaine d'alimentation de 3 kW court à côté.

**Recommandation finale : scénario A, fibre optique, en posant les trois gaines
en une seule tranchée.**

### Budget consolidé

| Poste | Fourchette |
|---|---|
| Institut, après test gratuit | 0 à 60 € |
| Tiny house, matériel fibre | 400 à 690 € |
| Tranchée, en la faisant toi-même | 150 à 250 € |
| Gaine de réserve supplémentaire | 70 à 115 € |
| Réseau invités Freebox | 0 € |
| Réglages Freebox OS | 0 € |
| **Total, pose personnelle** | **620 à 1 115 €** |
| Variante avec tranchée réalisée par un tiers | 1 070 à 2 065 € |

À mettre en regard de ce que ça protège : un outil de travail professionnel,
et la promesse faite à un segment travailleurs nomades sur une fiche notée 4,94
sur Airbnb et 9,5 sur Booking.

### Solution d'attente, si tu veux étaler la dépense

Un **Répéteur Wi-Fi Freebox** officiel, quelques euros par mois, en remplacement
immédiat du boîtier actuel. À 40 m sous les chênes, il retombera probablement
en 2,4 GHz et ne te donnera pas le débit du filaire, mais il corrige dès
maintenant les trois défauts structurels du boîtier actuel : plus de double
NAT, IPv6 conservé, et administration depuis Freebox OS. Tu attends ensuite le
bon moment pour creuser, en une seule fois, avec le bain nordique.

---

## Le problème à résoudre

La tiny house est couverte par un répéteur Wi-Fi tiers, mesuré le 27 novembre
2026 **depuis la maison** à 14,4 Mbps descendant, 3,7 Mbps montant et des
pointes de latence à 330 ms, avec un débit divisé par deux en quinze minutes
quand le voisin rentre chez lui.

**Ces chiffres sont le plancher du plancher.** Ils ont été mesurés à l'endroit
le plus favorable, à portée directe du répéteur. Dans la tiny house, derrière
une paroi et plus loin, le lien est nécessairement moins bon. Il faut y
mesurer avant de choisir.

Deux enjeux, et ils ne sont pas du même ordre :

1. **Le débit et la stabilité.** Tu cibles notamment les travailleurs nomades.
   Une visioconférence professionnelle ne tient pas sur 3,7 Mbps montant avec
   des pointes à 330 ms. C'est un risque d'avis négatif sur une fiche notée
   4,94 sur Airbnb et 9,5 sur Booking, et un frein à la montée d'ADR que tu
   cherches.
2. **L'isolation.** Aujourd'hui les voyageurs sont sur ton réseau. Ils voient
   tes ordinateurs, ton imprimante, tes éventuels disques réseau. Ce point se
   règle gratuitement, voir la dernière section.

---

## La contrainte que personne ne mentionne : tes chênes

Tes chênes centenaires sont ton argument commercial numéro un, et ils sont
aussi la principale contrainte technique de ce chantier.

**Pour le creusement.** Le système racinaire d'un chêne centenaire s'étend
bien au-delà de la projection de sa couronne. Trancher dans les racines
porteuses peut condamner l'arbre à échéance de quelques années, et un chêne
centenaire mort, c'est ton positionnement qui tombe avec lui. Fais passer la
tranchée en dehors de la zone d'aplomb du feuillage, quitte à allonger le
tracé. En cas de doute sur le tracé, un arboriste pour une demi-journée coûte
moins cher qu'un arbre.

**Pour le Wi-Fi.** Le feuillage de chêne est un très mauvais milieu pour le
5 GHz, encore plus quand il est humide. C'est pour cela qu'un répéteur radio,
même excellent, restera médiocre sur ce terrain, et c'est pour cela que
l'option A est la bonne.

---

## Option A1, câble cuivre enterré plus borne d'accès

La solution de référence. Tu obtiens dans la tiny house le même débit que dans
la maison.

### Matériel

| Poste | Ordre de grandeur |
|---|---|
| Câble Ethernet extérieur, catégorie 6, gainé PE et gelé | 0,80 à 1,50 € le mètre |
| Gaine TPC annelée rouge, diamètre 40 mm | 1,50 à 2,50 € le mètre |
| Grillage avertisseur rouge | 0,30 à 0,60 € le mètre |
| Borne d'accès Wi-Fi alimentée par le câble réseau | 70 à 250 € selon le modèle |
| Injecteur ou petit commutateur réseau alimenté | 25 à 60 € |
| Prises et connectique étanches, outillage de sertissage | 50 à 80 € |
| **Protection parafoudre réseau, aux deux extrémités** | 30 à 60 € par extrémité |

### Total matériel estimé, pose comprise si tu la fais toi-même

| Distance maison vers tiny house | Estimation |
|---|---|
| 20 à 30 m | 300 à 450 € |
| 40 à 60 m | 400 à 600 € |
| 70 à 90 m | 500 à 750 € |
| Plus de 100 m | Voir option A2, le cuivre ne passe plus |

Si tu fais creuser par un tiers, compte 600 à 1 200 € de main d'œuvre en plus
selon la longueur et la dureté du sol. Tu conduis des engins pour la
Métropole, cette ligne est peut-être celle que tu économises le plus
facilement.

### Règles de pose à respecter

- **Profondeur 60 cm** en zone de passage piéton, **80 cm** sous un passage de
  véhicule.
- **Grillage avertisseur rouge** posé 20 cm au-dessus de la gaine.
- **20 cm d'écart minimum** avec tout câble électrique, et croisement à 90°
  si tu dois en croiser un.
- **Gaine surdimensionnée**, en diamètre 40 plutôt que 25. Le surcoût est
  dérisoire et tu pourras tirer autre chose plus tard sans rouvrir la
  tranchée. Laisse un fil d'aiguillage dedans.
- **Limite absolue de 100 m** pour l'Ethernet cuivre, prises et mou compris.
  Au-delà, le lien ne négociera pas ou tombera à 100 Mbps.

### Le point à ne pas négliger

Un câble cuivre enterré entre deux bâtiments crée un chemin conducteur. Sous
des chênes centenaires, qui sont des points hauts, le risque de surtension
n'est pas théorique. **Une protection parafoudre réseau aux deux extrémités
est obligatoire, pas optionnelle.** Sans elle, un seul orage peut emporter la
borne d'accès et, dans le pire des cas, remonter jusqu'à la Freebox.

---

## Option A2, fibre optique enterrée plus borne d'accès

La même chose en mieux, pour 100 à 200 € de plus.

| Poste | Ordre de grandeur |
|---|---|
| Câble fibre optique préconnectorisé extérieur, longueur sur mesure | 80 à 200 € selon la longueur |
| Deux convertisseurs de média fibre vers Ethernet | 60 à 120 € la paire |
| Reste identique à l'option A1 (gaine, borne, connectique) | voir ci-dessus |

### Pourquoi c'est probablement le meilleur choix chez toi

- **La fibre n'est pas conductrice.** Plus de chemin pour la foudre, plus de
  parafoudre nécessaire, plus de risque pour la Freebox. Compte tenu de tes
  chênes, c'est l'argument décisif.
- **Pas de limite à 100 m.** Si la tiny house est loin, c'est la seule option.
- **Préconnectorisée**, elle se tire comme un câble ordinaire, sans soudure ni
  matériel de fusion. Prévois juste une gaine en diamètre 40 et des rayons de
  courbure larges aux angles.

Le surcoût par rapport au cuivre est de l'ordre de 100 à 200 €. Pour une
installation enterrée qu'on ne rouvre pas, c'est le bon arbitrage.

---

## Option B, Répéteur Wi-Fi Freebox

Le répéteur officiel de Free, qui fonctionne en Wi-Fi 7 avec ton abonnement
Ultra.

**Coût.** De l'ordre de quelques euros par mois en location, parfois inclus
selon l'offre. **À vérifier dans ton espace abonné Free, je ne peux pas te
donner le tarif exact de ton contrat.**

**Ce qu'il apporte par rapport au boîtier actuel.** Tout, en réalité. Il reste
en mode pont, donc pas de double traduction d'adresses. Il conserve l'IPv6. Il
gère l'itinérance proprement. Il est administré depuis Freebox OS.

**Ses limites, et elles sont structurelles.** Un répéteur radio partage son
temps d'antenne entre la box et les clients, ce qui divise le débit utile par
deux dans le meilleur des cas. Et surtout, il doit lui-même capter la Freebox
correctement. À travers des chênes centenaires, le 5 GHz passe mal, le
répéteur retombera en 2,4 GHz, et tu retrouveras une partie des problèmes
d'aujourd'hui.

**Verdict.** Bon compromis si la tiny house est proche et en vue relativement
dégagée. Mauvais choix si elle est loin ou derrière le feuillage.

---

## Option C, courant porteur en ligne

Deux boîtiers qui font passer les données par le câble électrique.

**Coût.** 60 à 120 € la paire pour un modèle correct.

**La condition qui décide de tout.** La tiny house doit être sur **le même
circuit électrique et le même compteur** que la maison. Si elle a son propre
compteur, ou si elle est sur une autre phase, le débit s'effondre ou ne passe
pas du tout.

**Vérifie avant d'acheter**, et achète chez un revendeur qui reprend sous
quinze jours. C'est un test de dix minutes : tu branches, tu mesures, tu
renvoies si c'est mauvais.

**Autres réserves.** Le débit varie selon ce qui est branché sur le circuit, et
se dégrade avec la longueur de câble. Un chargeur de voiture électrique ou un
variateur de lumière suffit à perturber la liaison. Ce n'est pas une solution
sur laquelle bâtir une promesse commerciale.

---

## Option D, pont Wi-Fi directionnel point à point

À garder en réserve si creuser s'avère impossible, par exemple à cause des
racines.

Deux antennes directionnelles qui se regardent, 120 à 200 € la paire, et tu
tiens plus de 100 Mbps sur plusieurs centaines de mètres.

**La condition.** Il faut une **vue directe** entre les deux antennes. Tes
chênes sont exactement ce qui l'empêche. À n'envisager que si tu trouves un
axe dégagé, par exemple de pignon à pignon au-dessus du feuillage bas.

---

## Tableau de décision

| Si la tiny house est... | Choisis |
|---|---|
| à moins de 30 m, en vue dégagée | Option B, le répéteur Freebox, suffit |
| à moins de 100 m, creusement possible | **Option A2, fibre enterrée** |
| à plus de 100 m | **Option A2, fibre enterrée**, seule option |
| sur le même compteur, test possible | Tester l'option C avant tout, c'est la moins chère |
| creusement impossible, vue dégagée | Option D |
| creusement impossible, pas de vue | Option B, en acceptant le résultat |

**Recommandation par défaut**, à confirmer avec les distances et des mesures
prises dans la tiny house et dans l'institut : **option A2, fibre optique
enterrée, en architecture en chaîne**, pour la neutralité face à la foudre sous
tes chênes et l'absence de limite de distance.

Le fait qu'un outil de travail professionnel dépende de cette liaison tranche
l'arbitrage. Les options B, C et D reposent toutes sur un support dont la
qualité varie avec le feuillage, l'humidité, les appareils branchés ou le
voisinage. Pour l'appareil de Nadia, il faut un support dont la performance ne
dépend de rien.

---

## Le réseau invités, à faire dans tous les cas et tout de suite

Celui-ci ne coûte rien et ne dépend d'aucune des options ci-dessus.

Dans Freebox OS, **Paramètres de la Freebox** puis **Wi-Fi**, section
**Wi-Fi invités** :

| Réglage | Valeur |
|---|---|
| Nom du réseau | `La Parenthese Bel-Air` |
| Mot de passe | un par séjour, ou un fixe simple à dicter |
| Isolation du réseau local | **activée**, c'est le point essentiel |
| Durée de validité | calée sur la durée du séjour |

Trois bénéfices concrets :

1. **Protection de tes données.** Les voyageurs n'atteignent plus tes
   appareils personnels.
2. **Protection juridique.** L'usage des voyageurs est séparé du tien, ce qui
   compte si l'un d'eux fait n'importe quoi depuis ta connexion.
3. **Cohérence du positionnement.** Un voyageur qui paie un séjour éco-luxe et
   qui doit se connecter à `Freebox-79B748_EXT2G`, ce n'est pas le même produit
   qu'un réseau nommé `La Parenthese Bel-Air`. C'est gratuit et ça se voit dans
   les trente premières secondes du séjour.

---

## Ce qu'il me faut pour affiner

1. **Les distances**, même approximatives : Freebox vers tiny house, Freebox
   vers institut, et tiny house vers institut. Cette dernière décide de
   l'architecture en chaîne ou en étoile.
2. **La position relative** des trois points. L'institut et la tiny house sont
   ils dans la même direction depuis la maison, ou de part et d'autre ?
3. **Le compteur électrique** : tiny house et institut sont ils sur le compteur
   de la maison, ou sur le leur ?
4. **Deux mesures de débit**, prises depuis un téléphone connecté au réseau du
   répéteur, l'une dans la tiny house, l'autre dans l'institut à côté de
   l'appareil LPG.
5. **La date et l'heure affichées par l'appareil LPG**, et s'il est relié au
   répéteur par câble ou en Wi-Fi.
6. **Les besoins réseau de l'appareil LPG**, si tu as sa documentation : a t'il
   besoin d'une connexion permanente, seulement pour les mises à jour, ou pour
   valider des droits d'usage à chaque séance ?
