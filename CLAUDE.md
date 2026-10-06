# chess.football — Spec canónica de las reglas de Chess.Football

## PASO 0 (bloqueante): actualizar `agents/`

Antes de cualquier tarea, inicializa el submódulo de agentes y llévalo al último
commit remoto:

```bash
git submodule update --init --recursive
git submodule update --remote agents
```

Si falla, para y avisa: no trabajes con estándares desactualizados.

## Instrucciones de agentes

- Lee SIEMPRE `agents/ARCHITECTURE-INDEX.md` primero.
- Lee SIEMPRE las reglas de oro comunes (`agents/standards/01-golden-rules.md`) y
  las de tu lado (`01.x-golden-rules-*.md`) según el índice.
- Lee `agents/standards/00-writing-in-spanish.md` si vas a escribir en español.
- Lee SOLO lo que el índice indique para tu tarea. NUNCA leas todo `agents/`.

## PASO 0.1 (bloqueante): ¿queda la estructura anterior en este equipo?

Si este repo no está dentro de la carpeta raíz `chess-football-bmad/` junto a
`chess-football-docs/`, o quedan restos de la estructura anterior a 2026-10-06 (repo
`chess-football-bmad` con `_bmad/` dentro, memorias de Claude Code con rutas antiguas,
skills locales del proyecto), **para** y sigue con el usuario el apartado «Migrar un
equipo con la estructura anterior» de `chess-football-docs/GUIDE.md`. No borres nada sin
confirmación.

## Qué es este repo

Repositorio **público** con las reglas oficiales del juego: `rules/es.md` es la versión
canónica y el resto de ficheros de `rules/` son sus traducciones (11 idiomas). No hay
código. Lado: repo de especificación (solo reglas de oro comunes).

Vive como carpeta hermana dentro de la carpeta raíz `chess-football-bmad/`. La
documentación del proyecto está en `chess-football-docs/docs/` (empieza por
`index.md`) y las convenciones propias en `chess-football-docs/docs/technical/conventions.md`.

## Reglas

- Un cambio de reglas empieza aquí: se actualiza `rules/es.md` y **todas** las
  traducciones afectadas en la misma PR. Después se implementa en
  `chess-football-engine` y se publica.
- El README y las reglas son públicos y van dirigidos a la comunidad: el README está en
  inglés.
- Siempre rama + PR; nunca merge local a `main`.
