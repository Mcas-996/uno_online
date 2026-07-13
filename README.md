# ✨ UNO Star Carnival ✨

> Standard UNO when you want it. Holiday chaos when you do not. 🌟

A cross-platform, fully offline UNO game for one player against local AI. The application runs in the terminal, needs no account or game server, and makes no network connection during play.

## Features

- Ratatui/Crossterm interface for Windows, macOS, and Linux.
- One human player against 1–4 local AI opponents.
- Easy, normal, and hard AI difficulty levels.
- Keyboard navigation and an optional command bar.
- Simplified Chinese for `zh*` system locales and English elsewhere.
- Standard two-to-five-player card setup, action cards, wild color choices, draw/pass phases, discard recycling, and single-round win detection.
- A selectable **Holiday Expansion**, enabled by default, with spectacular `+8` and four-color `WILD +16` cards.
- A gold-and-neon Star Carnival terminal theme in both English and Simplified Chinese.

The project intentionally does not include rooms, host/join commands, networking, accounts, remote AI, UNO-call penalties, Wild Draw Four challenges, or multi-round scoring.

## Requirements

- Rust 1.91 or newer(if you want to compile)
- A terminal of at least 70 × 22 cells

## Quick start

Install with `curl` on macOS or Linux:

```bash
curl --proto '=https' --tlsv1.2 -LsSf https://github.com/Mcas-996/uno_online/releases/download/v0.5.0-rc/uno-installer.sh | sh
```

Install with `irm` on Windows PowerShell:

```pwsh
powershell -ExecutionPolicy Bypass -c "irm https://github.com/Mcas-996/uno_online/releases/download/v0.5.0-rc/uno-installer.ps1 | iex"
```

## Run

The installer adds `uno` to your `PATH`. Start the game with:

```console
uno
```

Show non-interactive help:

```console
uno --help
```

## Controls

### Setup

- `↑` / `↓`: select player name, AI count, difficulty, deck, or Start
- `←` / `→`: adjust AI count, difficulty, or Standard/Holiday deck
- Type and Backspace: edit the selected player name
- `Enter`: advance or start the match
- `Esc`: exit

### Match

- `←` / `→`: select a card
- `Enter`: play the selected card
- `D`: draw
- `P`: pass after drawing
- `:`: open the command bar
- `?`: help
- `Q`: quit confirmation

The command bar accepts `play <index>`, `draw`, `pass`, `help`, `new`, and `quit`.

## Rules Included

### 🌟 Holiday Expansion

Holiday is the default deck and contains **118 cards**:

| Holiday card | Copies | Effect |
| --- | ---: | --- |
| Red `+8` | 2 | Matches red or another `+8`; the next player draws 8 and loses their turn. |
| Yellow `+8` | 2 | Matches yellow or another `+8`; the next player draws 8 and loses their turn. |
| Green `+8` | 2 | Matches green or another `+8`; the next player draws 8 and loses their turn. |
| Blue `+8` | 2 | Matches blue or another `+8`; the next player draws 8 and loses their turn. |
| Four-color `WILD +16` | 2 | Always playable; choose the next color, then the next player draws 16 and loses their turn. |

Choose **Standard 108** on the setup screen whenever you want the unchanged classic deck. If a Holiday penalty is larger than the drawable pile, the unlucky player takes every available card and the round continues.

### 🎴 Shared rules

- A player may play a matching color, matching rank, or wild card.
- Playing a number card also stacks every other card of the same number from that player's hand; the selected card remains on top.
- After drawing, only the newly drawn card may be played; otherwise the player passes.
- Wild Draw Four is legal only when the player has no card matching the active color.
- Skip, Reverse, Draw Two, Wild, and Wild Draw Four are supported. Reverse acts as Skip in a two-player game.
- When the draw pile is empty, all but the top discard are shuffled into a new draw pile.
- The first player to empty their hand wins the round.

## Development

```powershell
cargo fmt --check
cargo test
cargo clippy --all-targets -- -D warnings
cargo build --release -p uno
```

Source layout:

```text
src/
  core.rs  authoritative cards, rules, turns, and events
  ai.rs    local easy, normal, and hard AI policies
  app.rs   application state and input handling
  i18n.rs  Chinese and English localization
  ui.rs    terminal rendering
```

## License

GNU Affero General Public License v3.0 only. See [LICENSE](LICENSE).

used cargo-dist

## Something else
For your cybersecurity, run it in a new docker if you dont want to be attacked.
