# Chess.Football — Spielregeln

> Rundenbasiertes Strategiespiel für zwei Spieler, das die Bewegung der Schachfiguren mit dem Ziel des Fußballs kombiniert: mehr Tore als der Gegner zu erzielen, indem man den Ball gegen dessen König schießt.

---

## 1. Überblick

- **Spieler**: 2 (Weiß und Schwarz).
- **Ziel**: mehr Tore als der Gegner erzielen. Ein Tor wird erzielt, wenn ein Pass das Feld des gegnerischen Königs erreicht.
- **Züge**: abwechselnd. In jedem Zug verfügt der aktive Spieler über eine bei der Spielerstellung konfigurierbare Anzahl an **Aktionspunkten (AP)** (zwischen **1 und 5**; Standard ist 5).

---

## 2. Das Spielfeld

Das Spielfeld ist rechteckig: **9 Spalten (A–I) × 12 Reihen (1–12)**, insgesamt 108 Felder.

<img src="../assets/gameboard.png" alt="Chess.Football-Spielfeld" width="400">

### Die Strafräume

Jede Mannschaft hat einen **Strafraum von 5×2 Feldern** in ihrer Spielhälfte:

- **Weißer Strafraum**: Spalten C–G, Reihen 1–2.
- **Schwarzer Strafraum**: Spalten C–G, Reihen 11–12.

Regeln zu den Strafräumen:

1. Der **König darf sich nur innerhalb seines eigenen Strafraums bewegen**. Er darf ihn niemals verlassen, auch nicht mit dem Ball.
2. **Keine andere Figur derselben Mannschaft darf in ihren eigenen Strafraum**.
3. Gegnerische Figuren **dürfen** den gegnerischen Strafraum frei betreten.
4. Der **König ist unantastbar**: keine gegnerische Figur darf sein Feld betreten. Nur der Ball (durch einen Pass) kann ihn erreichen.

---

## 3. Die Figuren

Jede Mannschaft verfügt über **8 Figuren** mit vom Schach inspirierten Bewegungen:

| Figur          | Anzahl | Startposition (Weiß) | Rolle                      |
|----------------|--------|----------------------|----------------------------|
| König (K)      | 1      | E2                   | Tor / Ziel                 |
| Dame (Q)       | 1      | E6                   | Mittelfeldspieler          |
| Turm (R)       | 2      | A2, I2               | Außenverteidiger           |
| Läufer (B)     | 2      | D3, G5               | Innenverteidiger           |
| Springer (N)   | 2      | C5, F3               | Stürmer                    |

Die schwarzen Figuren werden spiegelbildlich in ihrer Hälfte aufgestellt.

### Bewegungen

| Figur     | Bewegung                                          | Springt über Figuren? | Strafraumbeschränkung           |
|-----------|---------------------------------------------------|------------------------|---------------------------------|
| König     | 1 Feld in beliebige Richtung                      | Nein                   | **Nur im eigenen Strafraum**    |
| Dame      | Unbegrenzte Felder in beliebige Richtung          | Nein                   | Darf eigenen Strafraum nicht betreten |
| Turm      | Unbegrenzte Felder horizontal oder vertikal       | Nein                   | Darf eigenen Strafraum nicht betreten |
| Läufer    | Unbegrenzte Felder diagonal                       | Nein                   | Darf eigenen Strafraum nicht betreten |
| Springer  | L-förmig (2+1)                                    | **Ja**                 | Darf eigenen Strafraum nicht betreten |

Zusätzliche Regeln:

- **Blockierung**: alle Figuren außer dem Springer werden von anderen Figuren auf ihrem Weg blockiert. Der Springer springt über jede Figur.
- **Du darfst nicht auf ein Feld ziehen, das von einer eigenen Figur besetzt ist.**
- **Du darfst nur dann auf das Feld einer gegnerischen Figur ziehen, wenn diese den Ball trägt** (Tackling) — **außer dem gegnerischen König, der unantastbar ist**.

---

## 4. Zugaufbau

In jedem Zug erhält der aktive Spieler die bei der Spielerstellung festgelegten **Aktionspunkte (AP)** — ein Wert zwischen **1 und 5** (Standard 5). Jede Aktion kostet 1 AP.

### Anstoß

Wer den Anstoß im ersten Zug ausführt, hängt vom Spielmodus ab:

- **Online-Spiel (PvP)**: **Weiß** stößt immer an.
- **Training (gegen KI)**: die vom Spieler bei der Spielerstellung **gewählte Seite** stößt an.

In beiden Fällen wird der Anstoß von der **Dame** der anstoßenden Seite ausgeführt, die mit dem Ball auf ihrem zentralen Feld beginnt. Anstöße **nach einem Tor** folgen der Regel aus [Abschnitt 7](#7-nach-einem-tor) (die Mannschaft, die das Tor kassiert hat, stößt an).

### Verfügbare Aktionen

1. **Bewegen** — eine eigene Figur auf ein gültiges Feld ziehen.
   - Jede Figur kann sich nur **einmal pro Zug** bewegen.
   - Hat die Figur den Ball, bewegt sich dieser mit (*Dribbling*).

2. **Pass** — die Figur mit dem Ball wirft ihn auf ein Zielfeld.
   - Die Figur bewegt sich nicht, nur der Ball fliegt.
   - Der Ball fliegt nach dem Bewegungsmuster der Figur.
   - **Eigene Figuren** auf dem Weg **beeinflussen den Pass nicht**: der Ball fliegt über sie hinweg.
   - Eine **gegnerische Figur** auf der Flugbahn **fängt den Pass ab** (oder es ist ein **Tor**, wenn diese gegnerische Figur der König ist). Pässe des **Springers** sind die Ausnahme: sie springen über alles hinweg, nur das Zielfeld zählt.

3. **Zug beenden** — den Zug freiwillig beenden und die verbleibenden AP verfallen lassen.

### Wann der Zug endet

- Bei Erreichen von 0 AP.
- Wenn der Spieler den Zug freiwillig beendet.
- Bei einer **Abfangaktion** oder einem **Tor** (erzwungenes Ende).

### Einschränkungen

- Eine Figur, die sich in diesem Zug bereits bewegt hat, kann sich nicht erneut bewegen.
- Eine Figur **kann sich im selben Zug bewegen und passen** (insgesamt 2 AP).
- Du kannst im selben Zug mehrere verschiedene Figuren bewegen.
- Du kannst nur passen, wenn eine deiner Figuren den Ball hat.

---

## 5. Der Ball

Der Ball befindet sich immer auf einem Feld. Er kann **frei** oder im **Besitz** einer Figur sein.

### Wie man den Ball erhält

- **Aufnahme auf dem Weg**: bewegt sich eine lineare Figur (König, Dame, Turm oder Läufer) und liegt der Ball auf ihrem Weg, nimmt sie ihn automatisch auf.
- **Aufnahme am Ziel**: jede Figur (auch der Springer), die ihre Bewegung auf dem Feld des freien Balls beendet, nimmt ihn auf.
- **Tackling**: wenn du auf das Feld einer gegnerischen Figur ziehst, die den Ball trägt, stiehlst du ihr den Ball und die gegnerische Figur wird auf ein freies orthogonal angrenzendes Feld verschoben.
  - **Den gegnerischen König darfst du nicht tacklen.**
  - Die Verschiebung folgt einer **festen Priorität**: rechts → links → oben → unten. Die gegnerische Figur belegt das erste freie orthogonale Feld in dieser Reihenfolge.
  - Das Feld, das der Angreifer **gerade verlassen hat**, zählt für die Verschiebung als frei: sind die anderen 4 orthogonalen Felder besetzt, der Angreifer kam aber von einem davon, landet der Gegner dort.
  - Bleibt nach dem oben Genannten **kein freies Feld** für die verschobene Figur, ist das Tackling **nicht erlaubt** (illegaler Zug).

### Dribbling

Wenn eine Figur mit dem Ball zieht, wandert der Ball mit. Die Kosten betragen 1 AP, wie bei einem normalen Zug. Der König kann dribbeln, **darf aber weiterhin seinen Strafraum nicht verlassen**.

### Pässe

- Die ballführende Figur wirft den Ball auf ein gültiges Feld, ohne sich zu bewegen.
- Die Passziele folgen demselben Bewegungsmuster wie die Figur. Figuren auf dem Weg **eliminieren keine Felder aus der Zielliste** (du kannst jedes Feld auf dem Bewegungsstrahl anvisieren), doch befindet sich eine gegnerische Figur auf der Flugbahn, **wird sie den Pass abfangen** — oder, falls diese gegnerische Figur der König ist, gibt es ein **Tor**. Siehe [Abfangen](#abfangen) und [Wie man ein Tor erzielt](#6-wie-man-ein-tor-erzielt).
- Kosten: 1 AP.

### Abfangen

Wenn eine **Nicht-Springer-Figur** einen Pass spielt, fliegt der Ball geradeaus. Liegt eine gegnerische Figur (nicht ihr König) auf diesem Weg:

- Die gegnerische Figur **am nächsten zum Passgeber** fängt den Ball ab.
- Der Zug des passenden Spielers **endet sofort** (AP werden auf 0 gesetzt).

> **Wichtig**: Springer-Pässe **können nicht abgefangen werden**. Der Ball „springt" zum exakten Zielfeld.

---

## 6. Wie man ein Tor erzielt

Ein Tor wird erzielt, wenn ein **Pass** das Feld des gegnerischen Königs erreicht:

- **Lineare Pässe** (Dame, Turm, Läufer, König): der Ball fliegt entlang des Weges. Die erste gegnerische Figur, die getroffen wird:
  - Ist es der **gegnerische König** → **TOR!** (der Ball bleibt auf dem Feld des Königs und der Zug endet).
  - Ist es **eine andere gegnerische Figur** → Abfangen.
- **Springer-Pässe**: nur das exakte L-Zielfeld zählt. Ist das Ziel der gegnerische König → **TOR!**

> Taktischer Trick: ein Pass **über den König hinaus** in gerader Linie ist ebenfalls ein Tor — der Ball stoppt beim König als erster gegnerischer Figur auf dem Weg.

---

## 7. Nach einem Tor

1. Der Spielstand wird aktualisiert (+1 für die torerzielende Mannschaft).
2. Das Spielfeld wird auf die Anfangsformation zurückgesetzt.
3. Die Mannschaft, die das Tor **kassiert** hat, stößt an: ihre Dame beginnt mit dem Ball in der Mitte.
4. Die Mannschaft, die das Tor kassiert hat, spielt den ersten Zug nach dem Tor.

---

## 8. Spielende

Das Spiel endet, wenn eine Mannschaft die **bei der Spielerstellung festgelegte Torzahl** erreicht.

- Das Torziel ist **zwischen 1 und 10 konfigurierbar** (Standard 3).
- Sobald eine Seite diese Zahl erreicht, endet das Spiel sofort und diese Seite wird zum Sieger erklärt.
- **Es gibt kein Unentschieden**: da das Torziel immer einen Torschützen voraussetzt, gibt es immer einen Gewinner.

---

## 9. Sonderregeln für den König

### 9a. Der König darf den Ball nicht länger als einen Zug halten

Der König darf den Ball annehmen und während dieses Zuges behalten, **muss ihn jedoch vor Ende seines nächsten Zuges abgeben**.

- Beendet der König den Zug mit dem Ball, wird die Bedingung *der König muss abspielen* gesetzt.
- Im **nächsten Zug** dieser Mannschaft muss der König den Ball passen.
- Hat der Spieler beim letzten AP noch nicht mit dem König gespielt, **gibt das System den Ball automatisch** auf ein **freies angrenzendes Feld** des Königs ab (verbraucht diesen letzten AP). Zuerst werden die 4 orthogonalen Felder versucht, sind alle besetzt, dann die 4 diagonalen.
- Die Anzeige des letzten aktiven AP verwandelt sich in eine Krone (👑), um den Spieler zu warnen.

**Warum**: verhindert, dass ein führender Spieler den Ball beim eigenen König parkt, um Zeit zu schinden.

### 9b. Rückpass zum Torwart

Sobald der König den Ball abgibt (freiwillig oder automatisch), **darf keine Figur derselben Mannschaft den Ball zurück zum König spielen**, bis eine gegnerische Figur ihn berührt.

- Sobald der König passt, wird er als Empfänger blockiert.
- Das Feld des Königs wird aus den gültigen Passzielen seiner Mitspieler ausgeschlossen.
- Die Sperre wird aufgehoben, sobald eine **gegnerische Figur den Ball berührt** (durch Abfangen, Tackling oder Tor).

**Warum**: bildet die Rückpass-Regel im Fußball nach — verhindert, dass die Mannschaft den Ball wiederholt zum König spielt, um Zeit zu verschwenden.

---

## 10. Schnellglossar

- **AP (Aktionspunkte)**: zwischen 1 und 5 bei der Spielerstellung konfigurierbar (Standard 5); jede Aktion kostet 1 AP.
- **Dribbling**: eine Figur mit dem Ball bewegen.
- **Pass**: den Ball spielen, ohne die Figur zu bewegen.
- **Tackling**: auf das Feld eines ballführenden Gegners ziehen, um ihm den Ball abzunehmen.
- **Abfangen**: gegnerische Figur, die einen Pass auf seinem Weg abfängt; der Zug des Passgebers endet.
- **Tor**: Pass, der das Feld des gegnerischen Königs erreicht.
- **Strafraum**: 5×2-Zone an jedem Ende des Spielfelds; nur der verteidigende König darf ihn betreten.

---
