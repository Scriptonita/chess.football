# Chess.Football — Regole del gioco

> Gioco di strategia a turni per due giocatori che combina il movimento dei pezzi degli scacchi con l'obiettivo del calcio: segnare più gol dell'avversario lanciando la palla contro il suo re.

---

## 1. Panoramica

- **Giocatori**: 2 (bianchi e neri).
- **Obiettivo**: segnare più gol dell'avversario. Si segna un gol quando un passaggio raggiunge la casella del re avversario.
- **Turni**: alternati. In ogni turno il giocatore attivo dispone di un numero di **Punti Azione (PA)** configurabile alla creazione della partita (tra **1 e 5**; predefinito 5).

---

## 2. Il tabellone

Il tabellone è rettangolare: **9 colonne (A–I) × 12 righe (1–12)**, per un totale di 108 caselle.

<img src="../assets/gameboard.png" alt="Tabellone di Chess.Football" width="400">

### Le aree

Ogni squadra ha un'**area di 5×2 caselle** nella propria metà campo:

- **Area bianca**: colonne C–G, righe 1–2.
- **Area nera**: colonne C–G, righe 11–12.

Regole sulle aree:

1. Il **re può muoversi solo all'interno della propria area**. Non può mai uscirne, nemmeno conducendo la palla.
2. **Nessun altro pezzo della stessa squadra può entrare nella propria area**.
3. I pezzi avversari **possono** entrare liberamente nell'area opposta.
4. Il **re è intoccabile**: nessun pezzo avversario può occupare la sua casella. Solo la palla (tramite un passaggio) può raggiungerlo.

---

## 3. I pezzi

Ogni squadra dispone di **8 pezzi** con movimenti ispirati agli scacchi:

| Pezzo         | Quantità | Posizione iniziale (bianchi) | Ruolo                      |
|---------------|----------|------------------------------|----------------------------|
| Re (K)        | 1        | E2                           | Porta / obiettivo          |
| Donna (Q)     | 1        | E6                           | Centrocampista             |
| Torre (R)     | 2        | A2, I2                       | Difensori laterali         |
| Alfiere (B)   | 2        | D3, G5                       | Difensori centrali         |
| Cavallo (N)   | 2        | C5, F3                       | Attaccanti                 |

I pezzi neri vengono disposti specularmente nella metà campo opposta.

### Movimenti

| Pezzo    | Movimento                                          | Salta pezzi? | Restrizione di area           |
|----------|----------------------------------------------------|--------------|-------------------------------|
| Re       | 1 casella in qualsiasi direzione                   | No           | **Solo nella propria area**   |
| Donna    | Caselle illimitate in qualsiasi direzione          | No           | Non può entrare nella propria area |
| Torre    | Caselle illimitate in orizzontale o verticale      | No           | Non può entrare nella propria area |
| Alfiere  | Caselle illimitate in diagonale                    | No           | Non può entrare nella propria area |
| Cavallo  | A forma di L (2+1)                                 | **Sì**       | Non può entrare nella propria area |

Regole aggiuntive:

- **Blocco**: tutti i pezzi tranne il cavallo vengono bloccati dagli altri pezzi sul loro cammino. Il cavallo salta sopra qualsiasi pezzo.
- **Non puoi muoverti su una casella occupata da un tuo pezzo.**
- **Puoi muoverti sulla casella di un pezzo avversario solo se quel pezzo ha la palla** (tackle) — **tranne il re avversario, che è intoccabile**.

---

## 4. Struttura del turno

In ogni turno, il giocatore attivo riceve i **Punti Azione (PA)** definiti alla creazione della partita — un valore configurabile tra **1 e 5** (5 di default). Ogni azione costa 1 PA.

### Calcio d'inizio

Chi effettua il calcio d'inizio del primo turno dipende dalla modalità di gioco:

- **Partita online (PvP)**: i **bianchi** danno sempre il via.
- **Allenamento (vs IA)**: dà il via la fazione **scelta dal giocatore** alla creazione della partita.

In entrambi i casi il calcio d'inizio è eseguito dalla **donna** della squadra che batte, che inizia con la palla nella sua casella centrale. I calci d'inizio **dopo un gol** seguono la regola della [sezione 7](#7-dopo-un-gol) (batte la squadra che ha subito gol).

### Azioni disponibili

1. **Muovere** — spostare un proprio pezzo su una casella valida.
   - Ogni pezzo può muoversi **una sola volta per turno**.
   - Se il pezzo ha la palla, questa si sposta con lui (*conduzione*).

2. **Passare** — il pezzo che ha la palla la lancia verso una casella di destinazione.
   - Il pezzo non si muove, viaggia solo la palla.
   - La palla segue lo schema direzionale del pezzo.
   - I **pezzi propri** sul percorso **non influenzano il passaggio**: la palla vola sopra di loro.
   - Un **pezzo avversario** sulla traiettoria **intercetta il passaggio** (o è **gol** se quel pezzo avversario è il re). I passaggi del **cavallo** sono l'eccezione: saltano sopra tutto, conta solo la casella di destinazione.

3. **Terminare il turno** — concludere il turno volontariamente cedendo i PA rimanenti.

### Quando termina il turno

- Al raggiungere 0 PA.
- Quando il giocatore termina il turno volontariamente.
- Al verificarsi di un'**intercettazione** o di un **gol** (fine forzata).

### Restrizioni

- Un pezzo che si è già mosso in questo turno non può muoversi di nuovo.
- Un pezzo **può muoversi e passare nello stesso turno** (2 PA in totale).
- Puoi muovere più pezzi diversi nello stesso turno.
- Puoi passare solo se uno dei tuoi pezzi ha la palla.

---

## 5. La palla

La palla è sempre su una casella del tabellone. Può essere **libera** o **in possesso** di un pezzo.

### Come ottenere il possesso

- **Cattura nel cammino**: se un pezzo lineare (re, donna, torre o alfiere) si muove e la palla si trova sul suo percorso, la raccoglie automaticamente.
- **Cattura alla destinazione**: qualsiasi pezzo (incluso il cavallo) che termina il movimento sulla casella della palla libera la raccoglie.
- **Tackle**: muovendoti sulla casella di un pezzo avversario che ha la palla, gli rubi il possesso e il pezzo avversario viene spostato su una casella ortogonale adiacente libera.
  - **Non puoi fare tackle al re avversario.**
  - Lo spostamento segue una **priorità fissa**: destra → sinistra → sopra → sotto. Il pezzo avversario occupa la prima casella ortogonale libera in quell'ordine.
  - La casella che l'attaccante **ha appena lasciato** conta come libera per lo spostamento: se le altre 4 ortogonali sono occupate ma l'attaccante proveniva da una di esse, l'avversario finisce lì.
  - Se dopo aver applicato quanto sopra **non resta alcuna casella libera** per il pezzo spostato, il tackle **non è permesso** (mossa illegale).

### Conduzione

Quando un pezzo con la palla si muove, la palla viaggia con lui. Il costo è 1 PA, come un movimento normale. Il re può condurre la palla, ma **continua a non poter uscire dalla propria area**.

### Passare

- Il pezzo con la palla la lancia su una casella valida senza muoversi.
- Le destinazioni del passaggio seguono lo stesso schema direzionale del movimento del pezzo. I pezzi sul percorso **non eliminano caselle dalla lista delle destinazioni** (puoi mirare a qualsiasi casella del raggio direzionale), ma se un pezzo avversario si trova sulla traiettoria **intercetterà il passaggio** — o, se quel pezzo avversario è il re, sarà **gol**. Vedi [Intercettazione](#intercettazione) e [Come segnare un gol](#6-come-segnare-un-gol).
- Costo: 1 PA.

### Intercettazione

Quando un pezzo **non cavallo** effettua un passaggio, la palla viaggia in linea retta. Se un pezzo avversario (diverso dal suo re) si trova su quel cammino:

- Il pezzo avversario **più vicino al passatore** intercetta la palla.
- Il turno del giocatore che ha passato **termina immediatamente** (i PA vengono azzerati).

> **Importante**: i passaggi del cavallo **non possono essere intercettati**. La palla "salta" fino alla destinazione esatta.

---

## 6. Come segnare un gol

Si segna un gol quando un **passaggio** raggiunge la casella del re avversario:

- **Passaggi lineari** (donna, torre, alfiere, re): la palla viaggia lungo il cammino. Il primo pezzo avversario incontrato:
  - Se è il **re avversario** → **GOL!** (la palla si ferma sulla casella del re e il turno termina).
  - Se è **un altro pezzo avversario** → intercettazione.
- **Passaggi del cavallo**: conta solo l'esatta casella di destinazione. Se la destinazione è il re avversario → **GOL!**

> Trucco tattico: un passaggio diretto **oltre il re** in linea retta è comunque gol — la palla si ferma sul re essendo il primo pezzo avversario sul cammino.

---

## 7. Dopo un gol

1. Il punteggio si aggiorna (+1 per la squadra che ha segnato).
2. Il tabellone si reimposta sulla formazione iniziale.
3. La squadra **che ha subito** il gol batte: la sua donna inizia con la palla al centro.
4. La squadra che ha subito gol gioca il primo turno dopo il gol.

---

## 8. Fine della partita

La partita termina quando una squadra raggiunge il **numero di gol obiettivo** definito alla creazione della partita.

- L'obiettivo di gol è **configurabile tra 1 e 10** (predefinito 3).
- Appena una squadra raggiunge quel numero, la partita finisce immediatamente e quella squadra è dichiarata vincitrice.
- **Non esistono pareggi**: poiché l'obiettivo di gol richiede sempre un marcatore, c'è sempre un vincitore.

---

## 9. Regole speciali del re

### 9a. Il re non può trattenere la palla per più di un turno

Il re può ricevere la palla e conservarla durante quel turno, ma **deve liberarla prima della fine del suo turno successivo**.

- Se il re termina il turno con la palla, viene impostata la condizione *il re deve liberare la palla*.
- Nel **turno successivo** di quella squadra, il re è obbligato a passare la palla.
- Se il giocatore non ha passato con il re al raggiungere l'ultimo PA, il sistema **libera la palla automaticamente** su una casella **adiacente libera** del re (consumando quell'ultimo PA). Si provano prima le 4 caselle ortogonali e, se sono tutte occupate, le 4 diagonali.
- L'indicatore dell'ultimo PA attivo si trasforma in una corona (👑) per avvisare il giocatore.

**Motivo**: evita che un giocatore in vantaggio parcheggi la palla con il proprio re per allungare i tempi.

### 9b. Retropassaggio al portiere

Una volta che il re libera la palla (volontariamente o automaticamente), **nessun pezzo della stessa squadra può ripassargliela** finché un pezzo avversario non la tocca.

- Quando il re passa, viene bloccato come ricevitore.
- La casella del re viene esclusa dalle destinazioni valide di passaggio per i suoi compagni.
- Il blocco si solleva quando un **pezzo avversario tocca la palla** (tramite intercettazione, tackle o gol).

**Motivo**: riflette la regola del retropassaggio al portiere nel calcio — evita che la squadra passi ripetutamente al re per perdere tempo.

---

## 10. Glossario rapido

- **PA (Punti Azione)**: configurabile tra 1 e 5 alla creazione della partita (5 di default); ogni azione costa 1 PA.
- **Condurre**: muovere un pezzo portando la palla.
- **Passare**: lanciare la palla senza muovere il pezzo.
- **Tackle**: muoverti sulla casella di un avversario con la palla per rubargliela.
- **Intercettazione**: pezzo avversario che cattura un passaggio sul suo percorso; il turno del passatore termina.
- **Gol**: passaggio che raggiunge la casella del re avversario.
- **Area**: zona di 5×2 caselle a ciascuna estremità del campo; solo il re difensore può calpestarla.

---
