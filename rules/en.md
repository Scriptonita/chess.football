# Chess.Football — Game Rules

> A turn-based strategy game for two players that mixes the movement of chess pieces with the goal of football: score more goals than your opponent by shooting the ball at their king.

---

## 1. Overview

- **Players**: 2 (white and black).
- **Objective**: score more goals than your opponent. A goal is scored when a pass reaches the rival king's square.
- **Turns**: alternating. Each turn, the active player has a number of **Action Points (AP)** configured when the match is created (between **1 and 5**; default is 5).

---

## 2. The board

The board is rectangular: **9 columns (A–I) × 12 rows (1–12)**, 108 squares in total.

```
12  · · · · · · · · ·   ← black baseline
11  R · · · K · · · R   ← Black area (defended by the black king)
10  · · · B · B · · ·
 9  · · · · · · · · ·
 8  · · N · · · N · ·
 7  · · · · Q · · · ·   ← centre
 6  · · · · Q · · · ·   ← centre
 5  · · N · · · N · ·
 4  · · · · · · · · ·
 3  · · · B · B · · ·
 2  R · · · K · · · R   ← White area (defended by the white king)
 1  · · · · · · · · ·   ← white baseline
    A B C D E F G H I
```

### The areas

Each team has a **5×2 area** at its end of the field:

- **White area**: columns C–G, rows 1–2.
- **Black area**: columns C–G, rows 11–12.

Rules about the areas:

1. The **king can only move within its own area**. It may never leave, not even while holding the ball.
2. **No other piece of the same team can enter its own area**.
3. Rival pieces **can** enter the opposite area freely.
4. The **king is untouchable**: no rival piece can step onto its square. Only the ball (through a pass) can reach it.

---

## 3. The pieces

Each team has **8 pieces** with chess-inspired movement:

| Piece        | Count | Starting position (white) | Role                     |
|--------------|-------|---------------------------|--------------------------|
| King (K)     | 1     | E2                        | Goal / target            |
| Queen (Q)    | 1     | E6                        | Midfielder               |
| Rook (R)     | 2     | A2, I2                    | Lateral defenders        |
| Bishop (B)   | 2     | D3, F3                    | Central defenders        |
| Knight (N)   | 2     | C5, G5                    | Strikers                 |

Black pieces are placed mirroring this layout on the opposite side of the board.

### Movement

| Piece   | Movement                                          | Jumps pieces? | Area restriction               |
|---------|---------------------------------------------------|---------------|--------------------------------|
| King    | 1 square in any direction                         | No            | **Only within its own area**   |
| Queen   | Unlimited squares in any direction                | No            | Cannot enter its own area      |
| Rook    | Unlimited squares horizontally or vertically      | No            | Cannot enter its own area      |
| Bishop  | Unlimited squares diagonally                      | No            | Cannot enter its own area      |
| Knight  | L-shape (2+1)                                     | **Yes**       | Cannot enter its own area      |

Additional rules:

- **Blocking**: every piece except the knight is blocked by other pieces in its path. The knight can jump over any piece.
- **You cannot move to a square occupied by your own piece.**
- **You may move to a square occupied by a rival piece only if that piece is holding the ball** (tackle) — **except for the rival king, who is untouchable**.

---

## 4. Turn structure

Each turn, the active player has the **Action Points (AP)** chosen when the match was created — a value configurable between **1 and 5** (5 by default). Every action costs 1 AP.

### Opening kickoff

Who takes the very first kickoff of the match depends on the game mode:

- **Online match (PvP)**: **white** always kicks off.
- **Training (vs AI)**: the side **chosen by the player** when creating the match kicks off.

In both cases the kickoff is taken by the **queen** of the serving side, which starts with the ball on its central square. Kickoffs **after a goal** follow the rule in [section 7](#7-after-a-goal) (the conceding team kicks off).

### Available actions

1. **Move** — move one of your pieces to a valid square.
   - Each piece can only move **once per turn**.
   - If the piece is holding the ball, the ball travels with it (*conducting*).

2. **Pass** — the piece holding the ball kicks it toward a destination square.
   - The piece does not move; only the ball travels.
   - The ball follows the piece's directional pattern.
   - **Your own pieces** on the path **do not affect the pass**: the ball flies over them.
   - A **rival piece** on the trajectory **intercepts the pass** (or it is a **goal** if that rival piece is the king). **Knight passes are the exception**: they jump over everything, only the destination square matters.

3. **End turn** — finish the turn voluntarily, forfeiting remaining AP.

### When the turn ends

- When AP reach 0.
- When the player voluntarily ends the turn.
- When an **interception** or a **goal** occurs (forced end).

### Constraints

- A piece that has already moved this turn cannot move again.
- A piece **can move and pass in the same turn** (2 AP total).
- You can move several different pieces in the same turn.
- You can only pass if one of your pieces is holding the ball.

---

## 5. The ball

The ball is always on a square. It can be **loose** or **in possession** of a piece.

### Gaining possession

- **Path capture**: if a linear piece (king, queen, rook or bishop) moves and the ball lies on its path, it picks it up automatically.
- **Destination capture**: any piece (including the knight) that ends its move on the loose ball's square picks it up.
- **Tackle**: when you move to the square of a rival piece holding the ball, you take the ball and the rival piece is displaced to an empty orthogonal adjacent square.
  - **You cannot tackle the rival king.**
  - Displacement follows a **fixed priority**: right → left → up → down. The rival piece is placed on the first orthogonal empty square in that order.
  - The square the attacker has **just vacated** counts as empty for the displacement: if the other four orthogonals are occupied but the attacker came from one of them, the rival lands there.
  - If after applying the above **no empty square remains** for the displaced piece, the tackle **is not allowed** (the move is illegal).

### Conducting

When a piece holding the ball moves, the ball travels with it. The cost is 1 AP, same as a regular move. The king may conduct the ball, but **it still cannot leave its area**.

### Passing

- The piece holding the ball sends it to a valid square without moving itself.
- Pass destinations follow the same directional pattern as the piece's movement. Pieces in the path **do not remove squares from the list of destinations** (you can aim at any square on the piece's directional ray), but if a rival piece lies on the trajectory it **will intercept the pass** — or, if that rival piece is the king, it will be a **goal**. See [Interception](#interception) and [How to score a goal](#6-how-to-score-a-goal).
- Cost: 1 AP.

### Interception

When a **non-knight** piece performs a pass, the ball travels in a straight line. If a rival piece (other than its king) is on that path:

- The rival piece **closest to the passer** intercepts the ball.
- The passing player's turn **ends immediately** (AP set to 0).

> **Important**: knight passes **cannot be intercepted**. The ball "jumps" to its exact destination.

---

## 6. How to score a goal

A goal is scored when a **pass** reaches the rival king's square:

- **Linear passes** (queen, rook, bishop, king): the ball travels along the path. The first rival piece encountered:
  - If it is the **rival king** → **GOAL!** (the ball stops at the king's square and the turn ends).
  - If it is **any other rival piece** → interception.
- **Knight passes**: only the exact L-shaped destination matters. If the destination is the rival king → **GOAL!**

> Tactical trick: a pass aimed **beyond the king** in a straight line is also a goal — the ball stops at the king as the first rival piece in the path.

---

## 7. After a goal

1. The scoreboard updates (+1 for the scoring team).
2. The board resets to the initial formation.
3. The team that **conceded** the goal serves: their queen starts with the ball at the centre.
4. The conceding team plays the first turn after the goal.

---

## 8. End of the match

The match ends when a team reaches the **goal target** set when the match was created.

- The goal target is **configurable between 1 and 10** (default: 3).
- As soon as one side reaches that number, the match ends immediately and that side is declared the winner.
- **There are no draws**: since the goal target always requires a scorer, there is always a winner.

---

## 9. King special rules

### 9a. The king cannot hold the ball for more than one turn

The king may receive the ball and keep it during that turn, but **must release it before its next turn ends**.

- If the king ends the turn holding the ball, the flag *king must release* is set.
- On the **following turn** for that team, the king must pass the ball.
- If the player has not passed with the king by the last AP, the system **auto-releases** the ball to an **empty adjacent square** of the king (consuming that final AP). The 4 orthogonal squares are tried first; if all of them are occupied, the 4 diagonal squares are tried next.
- The indicator of the last active AP turns into a crown (👑) to warn the player.

**Why**: prevents a winning player from parking the ball with their king to stall the game.

### 9b. Backpass to the keeper

Once the king releases the ball (voluntarily or automatically), **no teammate can pass the ball back to the king** until a rival piece touches it.

- When the king passes, it becomes blocked as a receiver.
- The king's square is excluded from valid pass destinations for its teammates.
- The block is lifted as soon as a **rival piece touches the ball** (through interception, tackle or goal).

**Why**: mirrors the football backpass rule — prevents repeatedly passing to the king to waste time.

---

## 10. Quick glossary

- **AP (Action Points)**: configurable from 1 to 5 when creating the match (5 by default); each action costs 1 AP.
- **Conducting**: moving a piece while it is carrying the ball.
- **Passing**: kicking the ball without moving the piece.
- **Tackle**: moving onto a rival piece holding the ball to steal it.
- **Interception**: a rival piece catches a pass in transit; the passer's turn ends.
- **Goal**: a pass that reaches the rival king's square.
- **Area**: 5×2 zone at each end of the board; only the defending king can step on it.

---

*This document is the human-readable version of the rules. For the technical specification used by the in-game AI, see the main application repository.*
