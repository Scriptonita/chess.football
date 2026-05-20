<p align="center">
  <img alt="Chess.Football" src="./assets/cover.png" />
</p>

<h1 align="center"><a href="https://chess.football">Chess.Football</a> — Official Rules</h1>

<p align="center">
  Public repository with the rules of <strong><a href="https://chess.football">Chess.Football</a></strong>, a turn-based strategy game that blends chess movement with the goal of football: score more goals than your opponent by shooting the ball at the rival king.
</p>

---

## What is this repository?

This repository exists to make the rules of **[Chess.Football](https://chess.football)** **public, versionable and translatable** by the community. Here we publish the canonical source of the rules and their translations into different languages, kept separate from the application's code so anyone can read them, suggest improvements or contribute new localisations without having to work on the game's repository.

## Structure

```
chess.football/
├── assets/         # Images and graphic resources
├── rules/          # Rule translations (one per language)
└── README.md
```

## Available languages

The rules are published as Markdown files inside the [`rules/`](./rules/) folder, with one file per language using the [ISO 639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) code:

- `rules/es.md` — Español
- `rules/en.md` — English
- `rules/it.md` — Italiano
- `rules/fr.md` — Français
- `rules/de.md` — Deutsch
- `rules/pt.md` — Português
- `rules/zh.md` — 中文
- `rules/ja.md` — 日本語
- `rules/ko.md` — 한국어
- `rules/ar.md` — العربية
- `rules/ru.md` — Русский

## How to contribute

Want to translate the rules into your language or fix an existing translation? Open a Pull Request adding or modifying the corresponding file in [`rules/`](./rules/).
