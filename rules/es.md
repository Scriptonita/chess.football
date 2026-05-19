# Chess.Football — Reglas del juego

> Juego de estrategia por turnos para dos jugadores que combina el movimiento de las piezas de ajedrez con el objetivo del fútbol: marcar más goles que el rival lanzando el balón contra su rey.

---

## 1. Visión general

- **Jugadores**: 2 (blancas y negras).
- **Objetivo**: marcar más goles que el rival. Se marca un gol cuando un pase alcanza la casilla del rey contrario.
- **Turnos**: alternos. En cada turno se dispone de **5 Puntos de Acción (PA)**.

---

## 2. El tablero

El tablero es rectangular: **9 columnas (A–I) × 12 filas (1–12)**, en total 108 casillas.

```
12  · · · · · · · · ·   ← fondo negro
11  R · · · K · · · R   ← Área negra (defendida por el rey negro)
10  · · · B · B · · ·
 9  · · · · · · · · ·
 8  · · N · · · N · ·
 7  · · · · Q · · · ·   ← centro
 6  · · · · Q · · · ·   ← centro
 5  · · N · · · N · ·
 4  · · · · · · · · ·
 3  · · · B · B · · ·
 2  R · · · K · · · R   ← Área blanca (defendida por el rey blanco)
 1  · · · · · · · · ·   ← fondo blanco
    A B C D E F G H I
```

### Las áreas

Cada equipo tiene un **área de 5×2 casillas** en su lado del campo:

- **Área blanca**: columnas C–G, filas 1–2.
- **Área negra**: columnas C–G, filas 11–12.

Reglas sobre las áreas:

1. El **rey solo puede moverse dentro de su propia área**. Nunca puede salir, ni siquiera llevando el balón.
2. Las **demás piezas del mismo equipo no pueden entrar en su propia área**.
3. Las piezas rivales **sí pueden entrar** libremente en el área contraria.
4. El **rey es intocable**: ninguna pieza rival puede pisar su casilla. Solo el balón (mediante un pase) puede alcanzarla.

---

## 3. Las piezas

Cada equipo dispone de **8 piezas** con movimientos inspirados en el ajedrez:

| Pieza        | Cantidad | Posición inicial (blancas) | Rol                        |
|--------------|----------|----------------------------|----------------------------|
| Rey (K)      | 1        | E2                         | Portería / objetivo        |
| Dama (Q)     | 1        | E6                         | Mediocampista              |
| Torre (R)    | 2        | A2, I2                     | Defensas laterales         |
| Alfil (B)    | 2        | D3, F3                     | Defensas centrales         |
| Caballo (N)  | 2        | C5, G5                     | Delanteros                 |

Las piezas negras se sitúan en una posición espejo en su lado del campo.

### Movimientos

| Pieza   | Movimiento                                          | ¿Salta piezas? | Restricción de área           |
|---------|-----------------------------------------------------|----------------|-------------------------------|
| Rey     | 1 casilla en cualquier dirección                    | No             | **Solo dentro de su área**    |
| Dama    | Casillas ilimitadas en cualquier dirección          | No             | No puede entrar en su área    |
| Torre   | Casillas ilimitadas en horizontal o vertical        | No             | No puede entrar en su área    |
| Alfil   | Casillas ilimitadas en diagonal                     | No             | No puede entrar en su área    |
| Caballo | En forma de L (2+1)                                 | **Sí**         | No puede entrar en su área    |

Reglas adicionales:

- **Bloqueo**: todas las piezas excepto el caballo se ven bloqueadas por otras piezas en su camino. El caballo salta por encima de cualquier pieza.
- **No puedes moverte a una casilla ocupada por una pieza propia.**
- **Puedes moverte a la casilla de una pieza rival únicamente si esa pieza lleva el balón** (entrada o *tackle*) — **salvo el rey rival, que es intocable**.

---

## 4. Estructura del turno

Cada turno, el jugador activo recibe **5 Puntos de Acción (PA)**. Cada acción cuesta 1 PA.

### Acciones disponibles

1. **Mover** — desplazar una pieza propia a una casilla válida.
   - Cada pieza solo puede moverse **una vez por turno**.
   - Si la pieza lleva el balón, este se desplaza con ella (*conducción*).

2. **Pasar** — la pieza que tiene el balón lo lanza a una casilla destino.
   - La pieza no se mueve, solo viaja el balón.
   - El balón vuela siguiendo el patrón direccional de la pieza.
   - Los pases **no son bloqueados por las piezas del recorrido** salvo cuando se produce una intercepción.

3. **Terminar turno** — finalizar el turno voluntariamente cediendo los PA restantes.

### Cuándo termina el turno

- Al llegar a 0 PA.
- Cuando el jugador termina el turno voluntariamente.
- Al producirse una **intercepción** o un **gol** (final forzado).

### Restricciones

- Una pieza que ya se ha movido en este turno no puede volver a moverse.
- Una pieza **sí puede moverse y pasar en el mismo turno** (2 PA en total).
- Puedes mover varias piezas distintas en el mismo turno.
- Solo puedes hacer un pase si una de tus piezas tiene el balón.

---

## 5. El balón

El balón siempre está en una casilla del tablero. Puede estar **suelto** o **en posesión** de una pieza.

### Cómo ganar la posesión

- **Captura en el camino**: si una pieza lineal (rey, dama, torre o alfil) se mueve y el balón está en su recorrido, lo recoge automáticamente.
- **Captura en el destino**: cualquier pieza (incluido el caballo) que termine su movimiento en la casilla del balón suelto, lo recoge.
- **Entrada (*tackle*)**: al moverte a la casilla de una pieza rival que lleva el balón, le robas la posesión y la pieza rival es desplazada a una casilla ortogonal adyacente libre.
  - **No se puede entrar al rey rival.**
  - Si la pieza rival está rodeada por las cuatro casillas ortogonales (sin sitio libre para ser desplazada), la entrada **no está permitida**.

### Conducción

Cuando una pieza con el balón se mueve, el balón viaja con ella. El coste es 1 PA, igual que un movimiento normal. El rey puede conducir el balón, pero **sigue sin poder salir de su área**.

### Pasar

- La pieza con balón lo lanza a una casilla válida sin moverse.
- Los destinos del pase siguen el mismo patrón direccional que el movimiento de la pieza, pero los pases **no son bloqueados** por las piezas del camino.
- Coste: 1 PA.

### Intercepción

Cuando una pieza **no caballo** realiza un pase, el balón viaja en línea recta. Si una pieza rival (que no sea su rey) se encuentra en ese camino:

- La pieza rival **más cercana al pasador** intercepta el balón.
- El turno del jugador que pasó **termina inmediatamente** (los PA se ponen a 0).

> **Importante**: los pases del caballo **no pueden ser interceptados**. El balón "salta" hasta el destino exacto.

---

## 6. Cómo marcar un gol

Se marca gol cuando un **pase** alcanza la casilla del rey rival:

- **Pases lineales** (dama, torre, alfil, rey): el balón viaja por el camino. La primera pieza rival que se encuentra:
  - Si es el **rey rival** → **¡GOL!** (el balón se detiene en la casilla del rey y el turno termina).
  - Si es **otra pieza rival** → intercepción.
- **Pases de caballo**: solo importa la casilla exacta de destino. Si el destino es el rey rival → **¡GOL!**

> Truco táctico: un pase dirigido **más allá del rey** en línea recta también es gol — el balón se detiene en el rey al ser la primera pieza rival del camino.

---

## 7. Después de un gol

1. El marcador se actualiza (+1 para el equipo que marcó).
2. El tablero se reinicia a la formación inicial.
3. El equipo **que ha encajado** saca: su dama empieza con el balón en el centro.
4. El equipo que ha encajado juega el primer turno tras el gol.

---

## 8. Reglas especiales del rey

### 8a. El rey no puede retener el balón más de un turno

El rey puede recibir el balón y conservarlo durante ese turno, pero **debe soltarlo antes de que termine su siguiente turno**.

- Si el rey termina el turno con el balón, queda marcada la condición *el rey debe soltar*.
- En el **siguiente turno** de ese equipo, el rey está obligado a pasar el balón.
- Si el jugador no ha pasado con el rey al llegar al último PA, el sistema **suelta el balón automáticamente** a una casilla ortogonal adyacente libre (consumiendo ese último PA).
- El indicador del último PA activo se transforma en una corona (👑) avisando al jugador.

**Motivo**: evita que un jugador que va ganando aparque el balón con su rey para alargar el tiempo.

### 8b. Cesión al portero

Una vez que el rey suelta el balón (de forma voluntaria o automática), **ninguna pieza del mismo equipo puede devolverle el balón al rey** hasta que una pieza rival lo toque.

- Cuando el rey pasa, queda bloqueado como receptor.
- La casilla del rey queda excluida de los destinos válidos de pase para sus compañeros.
- El bloqueo se levanta cuando una **pieza rival toca el balón** (mediante intercepción, entrada o gol).

**Motivo**: refleja la regla de cesión al portero en el fútbol — evita que el equipo pase repetidamente al rey para perder tiempo.

---

## 9. Glosario rápido

- **PA (Puntos de Acción)**: 5 por turno; cada acción cuesta 1 PA.
- **Conducir**: mover una pieza llevando el balón.
- **Pasar**: lanzar el balón sin mover la pieza.
- **Entrada / Tackle**: moverte a la casilla de un rival con balón para robárselo.
- **Intercepción**: pieza rival que captura un pase en su recorrido; el turno del pasador termina.
- **Gol**: pase que alcanza la casilla del rey rival.
- **Área**: zona de 5×2 casillas en cada extremo del campo; solo el rey defensor puede pisarla.

---

*Esta documentación es la versión humana de las reglas del juego. Para la especificación técnica utilizada por la inteligencia artificial del juego, consulta el repositorio principal de la aplicación.*
