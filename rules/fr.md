# Chess.Football — Règles du jeu

> Jeu de stratégie au tour par tour pour deux joueurs qui combine le mouvement des pièces d'échecs avec l'objectif du football : marquer plus de buts que l'adversaire en lançant le ballon contre son roi.

---

## 1. Vue d'ensemble

- **Joueurs** : 2 (blancs et noirs).
- **Objectif** : marquer plus de buts que l'adversaire. Un but est marqué lorsqu'une passe atteint la case du roi adverse.
- **Tours** : alternés. À chaque tour, le joueur actif dispose d'un nombre de **Points d'Action (PA)** configurable à la création de la partie (entre **1 et 5** ; par défaut, 5).

---

## 2. Le plateau

Le plateau est rectangulaire : **9 colonnes (A–I) × 12 lignes (1–12)**, soit 108 cases au total.

<img src="../assets/gameboard.png" alt="Plateau de Chess.Football" width="400">

### Les surfaces

Chaque équipe possède une **surface de 5×2 cases** dans son camp :

- **Surface blanche** : colonnes C–G, lignes 1–2.
- **Surface noire** : colonnes C–G, lignes 11–12.

Règles concernant les surfaces :

1. Le **roi ne peut se déplacer que dans sa propre surface**. Il ne peut jamais en sortir, même en conduisant le ballon.
2. **Aucune autre pièce de la même équipe ne peut entrer dans sa propre surface**.
3. Les pièces adverses **peuvent** entrer librement dans la surface opposée.
4. Le **roi est intouchable** : aucune pièce adverse ne peut occuper sa case. Seul le ballon (par une passe) peut l'atteindre.

---

## 3. Les pièces

Chaque équipe dispose de **8 pièces** aux mouvements inspirés des échecs :

| Pièce         | Quantité | Position initiale (blancs)  | Rôle                       |
|---------------|----------|-----------------------------|----------------------------|
| Roi (K)       | 1        | E2                          | But / cible                |
| Dame (Q)      | 1        | E6                          | Milieu de terrain          |
| Tour (R)      | 2        | A2, I2                      | Défenseurs latéraux        |
| Fou (B)       | 2        | D3, G5                      | Défenseurs centraux        |
| Cavalier (N)  | 2        | C5, F3                      | Attaquants                 |

Les pièces noires sont placées en miroir dans leur camp.

### Mouvements

| Pièce     | Mouvement                                          | Saute les pièces ? | Restriction de surface         |
|-----------|----------------------------------------------------|--------------------|--------------------------------|
| Roi       | 1 case dans n'importe quelle direction             | Non                | **Uniquement dans sa surface** |
| Dame      | Cases illimitées dans n'importe quelle direction   | Non                | Ne peut entrer dans sa surface |
| Tour      | Cases illimitées en horizontal ou vertical         | Non                | Ne peut entrer dans sa surface |
| Fou       | Cases illimitées en diagonale                      | Non                | Ne peut entrer dans sa surface |
| Cavalier  | En forme de L (2+1)                                | **Oui**            | Ne peut entrer dans sa surface |

Règles supplémentaires :

- **Blocage** : toutes les pièces sauf le cavalier sont bloquées par les autres pièces sur leur chemin. Le cavalier saute par-dessus toute pièce.
- **Tu ne peux pas te déplacer sur une case occupée par ta propre pièce.**
- **Tu peux te déplacer sur la case d'une pièce adverse uniquement si elle a le ballon** (tacle) — **sauf le roi adverse, qui est intouchable**.

---

## 4. Structure du tour

À chaque tour, le joueur actif reçoit les **Points d'Action (PA)** définis à la création de la partie — une valeur configurable entre **1 et 5** (5 par défaut). Chaque action coûte 1 PA.

### Coup d'envoi

Qui effectue le coup d'envoi du premier tour dépend du mode de jeu :

- **Partie en ligne (PvP)** : les **blancs** engagent toujours.
- **Entraînement (vs IA)** : engage la couleur **choisie par le joueur** à la création de la partie.

Dans les deux cas, le coup d'envoi est donné par la **dame** du camp qui engage, qui commence avec le ballon sur sa case centrale. Les coups d'envoi **après un but** suivent la règle de la [section 7](#7-après-un-but) (engage l'équipe qui a encaissé).

### Actions disponibles

1. **Déplacer** — bouger une de tes pièces vers une case valide.
   - Chaque pièce ne peut se déplacer qu'**une fois par tour**.
   - Si la pièce a le ballon, celui-ci se déplace avec elle (*conduite*).

2. **Passer** — la pièce qui a le ballon le lance vers une case de destination.
   - La pièce ne bouge pas, seul le ballon voyage.
   - Le ballon vole en suivant le schéma directionnel de la pièce.
   - Les **pièces de ton équipe** sur le trajet **n'affectent pas la passe** : le ballon vole au-dessus d'elles.
   - Une **pièce adverse** sur la trajectoire **intercepte la passe** (ou c'est un **but** si cette pièce adverse est le roi). Les passes du **cavalier** sont l'exception : elles sautent par-dessus tout, seule la case de destination compte.

3. **Terminer le tour** — finir le tour volontairement en cédant les PA restants.

### Quand le tour se termine

- En atteignant 0 PA.
- Quand le joueur termine le tour volontairement.
- Lorsqu'une **interception** ou un **but** se produit (fin forcée).

### Restrictions

- Une pièce qui a déjà bougé pendant ce tour ne peut pas bouger à nouveau.
- Une pièce **peut bouger et passer dans le même tour** (2 PA au total).
- Tu peux déplacer plusieurs pièces différentes dans le même tour.
- Tu ne peux faire une passe que si une de tes pièces a le ballon.

---

## 5. Le ballon

Le ballon est toujours sur une case du plateau. Il peut être **libre** ou **en possession** d'une pièce.

### Comment obtenir la possession

- **Capture sur le chemin** : si une pièce linéaire (roi, dame, tour ou fou) se déplace et que le ballon est sur son trajet, elle le récupère automatiquement.
- **Capture à la destination** : toute pièce (y compris le cavalier) qui termine son mouvement sur la case du ballon libre le récupère.
- **Tacle** : en te déplaçant sur la case d'une pièce adverse qui a le ballon, tu lui voles la possession et la pièce adverse est déplacée vers une case orthogonale adjacente libre.
  - **Tu ne peux pas tacler le roi adverse.**
  - Le déplacement suit une **priorité fixe** : droite → gauche → haut → bas. La pièce adverse occupe la première case orthogonale libre dans cet ordre.
  - La case que l'attaquant **vient de quitter** compte comme libre pour le déplacement : si les 4 autres orthogonales sont occupées mais que l'attaquant venait de l'une d'elles, l'adverse y atterrit.
  - Si après application de ce qui précède **il ne reste aucune case libre** pour la pièce déplacée, le tacle **n'est pas autorisé** (mouvement illégal).

### Conduite

Quand une pièce avec le ballon se déplace, le ballon voyage avec elle. Le coût est de 1 PA, comme un mouvement normal. Le roi peut conduire le ballon, mais **il ne peut toujours pas quitter sa surface**.

### Passer

- La pièce avec le ballon le lance vers une case valide sans se déplacer.
- Les destinations de la passe suivent le même schéma directionnel que le mouvement de la pièce. Les pièces sur le trajet **n'éliminent pas de cases de la liste des destinations** (tu peux viser n'importe quelle case du rayon directionnel), mais si une pièce adverse se trouve sur la trajectoire elle **interceptera la passe** — ou, si cette pièce adverse est le roi, ce sera **but**. Voir [Interception](#interception) et [Comment marquer un but](#6-comment-marquer-un-but).
- Coût : 1 PA.

### Interception

Quand une pièce **autre que le cavalier** effectue une passe, le ballon voyage en ligne droite. Si une pièce adverse (autre que son roi) se trouve sur ce chemin :

- La pièce adverse **la plus proche du passeur** intercepte le ballon.
- Le tour du joueur qui a passé **se termine immédiatement** (les PA sont mis à 0).

> **Important** : les passes du cavalier **ne peuvent pas être interceptées**. Le ballon « saute » jusqu'à la destination exacte.

---

## 6. Comment marquer un but

On marque un but lorsqu'une **passe** atteint la case du roi adverse :

- **Passes linéaires** (dame, tour, fou, roi) : le ballon voyage le long du chemin. La première pièce adverse rencontrée :
  - Si c'est le **roi adverse** → **BUT !** (le ballon s'arrête sur la case du roi et le tour se termine).
  - Si c'est **une autre pièce adverse** → interception.
- **Passes de cavalier** : seule la case exacte de destination compte. Si la destination est le roi adverse → **BUT !**

> Astuce tactique : une passe dirigée **au-delà du roi** en ligne droite est aussi un but — le ballon s'arrête sur le roi, première pièce adverse du chemin.

---

## 7. Après un but

1. Le score est mis à jour (+1 pour l'équipe qui a marqué).
2. Le plateau est réinitialisé à la formation initiale.
3. L'équipe **qui a encaissé** engage : sa dame commence avec le ballon au centre.
4. L'équipe qui a encaissé joue le premier tour après le but.

---

## 8. Fin du match

Le match se termine lorsqu'une équipe atteint le **nombre de buts cible** défini à la création de la partie.

- L'objectif de buts est **configurable entre 1 et 10** (par défaut, 3).
- Dès qu'une équipe atteint ce nombre, le match se termine immédiatement et cette équipe est déclarée vainqueure.
- **Il n'y a pas de match nul** : puisque l'objectif de buts exige toujours un buteur, il y a toujours un gagnant.

---

## 9. Règles spéciales du roi

### 9a. Le roi ne peut conserver le ballon plus d'un tour

Le roi peut recevoir le ballon et le conserver pendant ce tour, mais **doit le lâcher avant la fin de son tour suivant**.

- Si le roi termine le tour avec le ballon, l'état *le roi doit lâcher* est activé.
- Au **tour suivant** de cette équipe, le roi est obligé de passer le ballon.
- Si le joueur n'a pas passé avec le roi en arrivant au dernier PA, le système **lâche le ballon automatiquement** sur une case **adjacente libre** du roi (consommant ce dernier PA). On essaie d'abord les 4 cases orthogonales et, si toutes sont occupées, les 4 diagonales.
- L'indicateur du dernier PA actif se transforme en couronne (👑) pour avertir le joueur.

**Pourquoi** : empêche un joueur en tête de garer le ballon avec son roi pour gagner du temps.

### 9b. Passe en retrait au gardien

Une fois que le roi a lâché le ballon (volontairement ou automatiquement), **aucune pièce de la même équipe ne peut lui redonner le ballon** jusqu'à ce qu'une pièce adverse le touche.

- Quand le roi passe, il est bloqué en tant que receveur.
- La case du roi est exclue des destinations valides de passe pour ses coéquipiers.
- Le blocage est levé dès qu'une **pièce adverse touche le ballon** (par interception, tacle ou but).

**Pourquoi** : reflète la règle de la passe en retrait au gardien en football — empêche l'équipe de passer à plusieurs reprises au roi pour gagner du temps.

---

## 10. Glossaire rapide

- **PA (Points d'Action)** : configurable entre 1 et 5 à la création de la partie (5 par défaut) ; chaque action coûte 1 PA.
- **Conduire** : déplacer une pièce avec le ballon.
- **Passer** : lancer le ballon sans déplacer la pièce.
- **Tacle** : te déplacer sur la case d'un adversaire avec le ballon pour le lui voler.
- **Interception** : pièce adverse qui capture une passe sur son trajet ; le tour du passeur se termine.
- **But** : passe qui atteint la case du roi adverse.
- **Surface** : zone de 5×2 cases à chaque extrémité du terrain ; seul le roi défenseur peut y poser le pied.

---
