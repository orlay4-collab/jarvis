# Bilan des mesures, réseau Wi-Fi

Diagnostic et optimisation du 27 novembre 2026, entre 19h50 et 20h07.
Poste de mesure : MacBook sous macOS 12.7.6, interface `en0`, carte Broadcom
802.11 a/b/g/n/ac.

## Contexte

Abonnement : **Freebox Ultra**, Freebox v9 (r1), modèle `fbxgw9-r1`.
Débit souscrit : 8 Gbit/s descendant et 8 Gbit/s montant.

## Avant et après

| Indicateur | Avant, via répéteur | Pire point mesuré | Après, direct Freebox |
|---|---|---|---|
| Réseau | `Freebox-79B748_EXT2G` | idem | `Freebox-79B748` |
| Bande et canal | 2,4 GHz, canal 9 | idem | 5 GHz, canal 40 |
| Largeur de canal | 20 MHz | 20 MHz | 80 MHz |
| Norme | 802.11n | 802.11n | **802.11ac** |
| Flux spatiaux | 1 | 1 | **2** |
| Débit radio négocié | 52 Mbps | 39 Mbps | **468 à 585 Mbps** |
| Plafond radio | 72 Mbps | 72 Mbps | **867 Mbps** |
| Signal | -67 dBm | -74 dBm | -61 dBm |
| Marge signal/bruit | 34 dB | 21 dB | 34 dB |
| **Débit descendant** | 28,8 Mbps | 14,4 Mbps | **163,6 Mbps** |
| **Débit montant** | 19,4 Mbps | 3,7 Mbps | **238,3 Mbps** |
| Latence moyenne | 30,9 ms | 101,6 ms | **16,3 ms** |
| Latence maximale | 130,0 ms | 330,2 ms | **22,5 ms** |
| Écart-type latence | 33,1 ms | 106,8 ms | **1,5 ms** |
| Réactivité montante | 58 RPM, Low | 119 RPM, Low | **547 RPM, Medium** |
| Réactivité descendante | 354 RPM, Medium | 169 RPM, Low | **389 RPM, Medium** |
| Sauts jusqu'à Internet | 3, double NAT | 3 | **2** |
| IPv6 | absent | absent | **opérationnel, 4,3 ms** |
| Perte de paquets | 0 % | 0 % | 0 % |

Résolution DNS après bascule : 10 à 30 ms sur `google.com`, `airbnb.fr`,
`booking.com` et `smoobu.com`.

## Gains obtenus

- Débit descendant multiplié par **5,7** par rapport à l'état initial, et par
  **11,4** par rapport au point le plus dégradé.
- Débit montant multiplié par **12,3**, et par **63,6** par rapport au pire
  point.
- Latence maximale divisée par **5,8**, instabilité divisée par **22**.
- Double traduction d'adresses supprimée, IPv6 rétabli.

## Ce qui a été fait sur le Mac

1. Suppression de 9 réseaux obsolètes de la liste des réseaux mémorisés :
   `freeboxRPNQNN5Ghz`, `freeboxRPNQNN 5Ghz_EXT5G`, `freeboxRPNQNN 5Ghz_EXT2G`,
   `freeboxRPNQNN`, `freebox_RPNQNN_5Ghz`, `freebox_RPNQNN`,
   `freeboxRPNQNN 5Ghz`, `Meross_SW_0DF5`, `HUAWEI_honor 5C_3A10`.
2. Suppression de `Freebox-79B748_EXT2G` de la liste, qui y occupait la
   première position et captait donc toutes les connexions automatiques.
3. Bascule de l'interface sur `Freebox-79B748`, qui passe en 5 GHz 802.11ac.

Liste des réseaux mémorisés restants : `Freebox-79B748`, `Family Andrieux`,
`Livebox-C980`, `Livebox-7C90`. Les trois derniers ont été conservés, à
confirmer ou supprimer.

## Ce qui reste à faire

Voir `procedure-freebox.md`. Les deux actions à plus fort rendement :

1. **Débrancher le répéteur**, boîtier joignable sur `192.168.10.1`.
2. **Séparer les noms de réseau 2,4 et 5 GHz** dans Freebox OS, pour que les
   appareils ne retombent plus en 2,4 GHz.

## Marge restante

Le Mac plafonne à 867 Mbps en radio, c'est une limite matérielle de sa carte
Wi-Fi 5. Même parfaitement réglé, il n'exploitera jamais plus de 5 % de
l'abonnement 8 Gbit/s. Pour les usages où le débit compte vraiment, un
adaptateur Ethernet sur le port Thunderbolt du Mac, relié à un port de la
Freebox Ultra, contournerait entièrement le Wi-Fi.
