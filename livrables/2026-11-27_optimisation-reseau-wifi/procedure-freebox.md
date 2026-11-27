# Procédure Freebox Ultra, réglages à appliquer

Diagnostic du 27 novembre 2026. Box identifiée : Freebox v9 (r1), Freebox Ultra, Freebox OS API 16.1.

## Accès à l'interface

Depuis un appareil connecté au réseau `Freebox-79B748` :

```
http://192.168.1.254
```

L'adresse `mafreebox.freebox.fr` fonctionne aussi, mais elle passe par les
serveurs DNS de Free avant de revenir chez toi. L'adresse IP est plus directe
et plus fiable.

Les réglages Wi-Fi sont dans **Paramètres de la Freebox** puis **Wi-Fi**.

---

## 1. Séparer les noms de réseau 2,4 GHz et 5 GHz

**Pourquoi.** Ta Freebox diffuse aujourd'hui le même nom, `Freebox-79B748`, sur
les deux bandes. Résultat observé pendant le diagnostic : le Mac s'est d'abord
associé en 2,4 GHz, parce que cette bande portait un signal très légèrement
plus fort (-55 contre -59 dBm), avant de basculer en 5 GHz au bout de quelques
dizaines de secondes. Pendant ce laps de temps, le débit descendant était
plafonné à 39 Mbps au lieu de plusieurs centaines.

Avec deux noms distincts, tu choisis explicitement la bande rapide, et tu ne
dépends plus de l'arbitrage automatique.

**Comment.** Dans la section Wi-Fi, cherche l'option qui regroupe les deux
bandes sous un seul nom. Selon la version de Freebox OS, elle s'intitule
« Diffuser le même SSID sur les deux bandes », « SSID unique » ou
« Wi-Fi unifié ». Désactive-la, puis renomme la bande 5 GHz, par exemple :

| Bande | Nom à donner |
|---|---|
| 2,4 GHz | `Freebox-79B748` (inchangé) |
| 5 GHz | `Freebox-79B748-5G` |

Garde le même mot de passe sur les deux, tu éviteras d'avoir à le ressaisir
partout.

**Si l'option n'existe pas** dans ton Freebox OS, le repli consiste à réduire
la puissance d'émission de la bande 2,4 GHz à 50 %. Le 5 GHz devient alors
systématiquement le plus fort à proximité de la box.

---

## 2. Fixer le canal 2,4 GHz sur 11

**Pourquoi.** Les seuls canaux qui ne se chevauchent pas en 2,4 GHz sont 1, 6
et 11. Ton voisin `Freebox-AFB36B` occupe le canal 6 et il est très puissant
chez toi, mesuré à -47 dBm en soirée. Ta Freebox est actuellement sur le canal
11, ce qui est le bon choix, mais en mode automatique elle peut dériver vers 8
ou 9 et se retrouver à cheval sur le canal du voisin.

**Comment.** Dans les réglages de la bande 2,4 GHz :

| Paramètre | Valeur |
|---|---|
| Canal | 11, en manuel et non en automatique |
| Largeur de canal | 20 MHz |

La largeur de 40 MHz en 2,4 GHz est une fausse bonne idée : elle double
l'encombrement spectral dans une bande déjà saturée et provoque plus de pertes
qu'elle n'apporte de débit.

---

## 3. Laisser le 5 GHz en automatique

La bande 5 GHz est quasiment libre autour de chez toi. Le seul réseau détecté
est `Livebox-C980` sur le canal 100, à -90 dBm, c'est-à-dire inaudible.
Aucune raison de forcer un canal.

Laisse la largeur de canal au maximum proposé. Ton Mac n'exploitera que 80 MHz,
c'est sa limite matérielle, mais tes téléphones et tablettes récents iront
au-delà.

---

## 4. Le répéteur : ne pas le débrancher, le remplacer

**Ce que c'est.** Le boîtier qui diffusait `Freebox-79B748_EXT2G` et
`Freebox-79B748_EXT5G`, joignable sur `192.168.10.1`. Son interface annonce
un firmware génériques d'entrée de gamme (`lighttpd`, page « Wi-Fi APP Login »,
mode `opmode = 3`), et son horloge système est restée bloquée au 1er janvier
1970, donc il n'a aucune synchronisation horaire.

**Ce qu'il te coûtait.**

- Il fonctionnait en mode routeur, ce qui créait un second réseau
  `192.168.10.0/24` derrière celui de la Freebox. Double traduction d'adresses,
  un saut réseau de plus, et toute redirection de port à configurer deux fois.
- Il supprimait complètement l'IPv6. Aucune adresse IPv6 n'était disponible
  sur le Mac tant qu'il était dans le chemin.
- Il distribuait un serveur DNS, `192.168.1.254`, situé hors de son propre
  sous-réseau.
- Il bridait la liaison à 802.11n, un seul flux, 20 MHz, soit 72 Mbps
  théoriques, là où la Freebox offre 867 Mbps au même Mac.
- Il émettait sur le canal 9, à cheval sur le canal 6 du voisin et sur le canal
  11 de ta propre Freebox. Il se parasitait lui-même.
- Le ping vers la Freebox renvoyait des paquets dupliqués, signe d'une boucle
  de diffusion entre le répéteur et la box.

## ⚠️ CORRECTION DU 27 NOVEMBRE 2026, EN FIN DE SESSION

**Ce répéteur ne doit pas être débranché.** L'information est arrivée après la
rédaction initiale de ce document.

Il ne dessert pas seulement la tiny house. Il dessert aussi **l'institut de
Nadia, et notamment son appareil LPG, qui est son outil de travail**, parce que
le signal de la Freebox ne porte pas jusqu'à l'institut.

Le débrancher couperait donc une activité professionnelle. L'ordre des
opérations s'inverse : **on installe d'abord l'infrastructure de remplacement,
on ne retire le répéteur qu'ensuite, et seulement après avoir vérifié que
l'institut et la tiny house sont bien desservis.**

### Ce que cela change à l'analyse

Les défauts du répéteur listés ci-dessus restent tous vrais, et ils sont même
plus graves qu'estimé, puisqu'un équipement professionnel en dépend :

- Un appareil LPG communique pour ses mises à jour, la validation de ses
  droits d'usage et la télémaintenance. Sur un lien mesuré à 3,7 Mbps montant
  avec des pointes de latence à 330 ms, une session de télémaintenance ou une
  validation en ligne peut échouer en pleine séance cliente.
- Le **double NAT** est particulièrement hostile à la télémaintenance. Un
  technicien LPG qui doit atteindre la machine depuis l'extérieur se heurte à
  deux traductions d'adresses successives.
- **L'horloge du répéteur est restée au 1er janvier 1970.** S'il sert aussi de
  référence horaire aux appareils de son réseau, toute connexion sécurisée
  peut être refusée, un certificat étant jugé invalide quand la date de la
  machine est fausse. À vérifier côté appareil LPG.
- L'appareil LPG se trouve aujourd'hui **sur le même réseau que les voyageurs
  de la tiny house**, sans isolation. Un équipement professionnel de santé et
  de bien-être ne devrait pas partager un segment réseau avec des inconnus de
  passage.

### Action révisée

1. **Ne touche à rien sur le répéteur pour l'instant.**
2. Mesure le débit depuis l'institut et depuis la tiny house, pour savoir ce
   que chacun reçoit réellement.
3. Vérifie la date et l'heure affichées par l'appareil LPG.
4. Décide de l'infrastructure de remplacement, voir
   `couverture-tiny-house-chiffrage.md`, qui couvre maintenant trois points de
   desserte et non deux.
5. Installe, vérifie, **puis seulement** retire le répéteur.

---

## 5. Si tu as besoin de couvrir la tiny house

C'est probablement la raison d'être de ce répéteur. Le besoin est légitime,
la solution était mauvaise. Trois options, de la meilleure à la moins bonne.

### Option A, câble Ethernet enterré plus borne d'accès

La seule solution qui tienne sur la distance et sous les chênes. Une gaine, un
câble extérieur en catégorie 6, et une borne Wi-Fi alimentée par le câble
lui-même. Tu obtiens dans la tiny house le même débit que dans la maison, sans
division par deux et sans dépendance à la météo ni au feuillage.

Pertinent pour ton activité : c'est un argument de vente réel pour les
travailleurs nomades, qui est une de tes deux cibles.

### Option B, Répéteur Wi-Fi Freebox

Free propose un répéteur officiel qui, avec l'Ultra, fonctionne en Wi-Fi 7 et
en vrai maillage. Contrairement au boîtier actuel, il reste en mode pont, ne
crée pas de second réseau, conserve l'IPv6 et gère l'itinérance proprement.
Nettement supérieur au boîtier actuel, mais un répéteur radio partage toujours
son temps d'antenne entre la box et les clients.

### Option C, courant porteur en ligne

À n'envisager que si la tiny house est sur le même circuit électrique que la
maison. Si elle est sur un tableau séparé ou une autre phase, le débit
s'effondre. À vérifier avant d'acheter.

---

## 6. Créer un réseau invités pour la tiny house

Indépendamment de la technique de couverture, ne donne jamais aux voyageurs
l'accès à ton réseau principal. Freebox OS propose un Wi-Fi invité avec :

- un nom et un mot de passe distincts
- l'isolation du réseau local, les voyageurs ne voient ni tes ordinateurs, ni
  ton imprimante, ni tes éventuels disques réseau
- une durée de validité, que tu peux calquer sur la durée du séjour
- la possibilité de changer le mot de passe à chaque réservation

Deux bénéfices pour ton activité : tu te protèges juridiquement en séparant
l'usage des voyageurs du tien, et tu peux afficher un nom de réseau propre
plutôt que `Freebox-79B748_EXT2G`.

---

## Ordre d'exécution conseillé

**Révisé en fin de session, après l'information sur l'appareil LPG de Nadia.**

Les trois premières étapes ne touchent pas au répéteur et peuvent être faites
ce soir sans aucun risque pour l'institut.

1. **Séparer les SSID 2,4 et 5 GHz**, puis connecter tes appareils au nom en
   `-5G`. Sans effet sur le répéteur.
2. **Fixer le canal 2,4 GHz sur 11, largeur 20 MHz.** Sans effet sur le
   répéteur, et bénéfique pour lui, puisque cela réduit le brouillage mutuel
   entre ta box et lui.
3. **Créer le réseau invités** pour la tiny house. Sans effet sur le répéteur.
4. **Mesurer** depuis l'institut et depuis la tiny house, et relever la date de
   l'appareil LPG.
5. **Décider et installer** l'infrastructure de remplacement pour les trois
   points de desserte.
6. **Retirer le répéteur**, et seulement après avoir vérifié que l'institut
   fonctionne.
