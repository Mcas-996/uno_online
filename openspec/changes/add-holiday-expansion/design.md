## Context

The application is a single Rust binary with authoritative rules in `core`, heuristic AI in `ai`, reducer-like input state in `app`, centralized bilingual copy in `i18n`, and Ratatui rendering in `ui`. The standard deck is currently hard-coded, all wild cards use one color picker path, and the game loop already redraws every 50 ms. Source files are UTF-8 as required by Rust, but the requested source-character repertoire is limited to characters representable by GBK; README is exempt.

## Goals / Non-Goals

**Goals:**

- Preserve standard play while adding a default-selectable 118-card Holiday variant.
- Resolve colored Draw Eight and unrestricted Wild Draw Sixteen through the authoritative rules engine.
- Keep AI actions legal and give the stronger cards explicit strategic weights.
- Apply a coherent star-carnival treatment across the full TUI using terminal-native styling.
- Keep all Rust source characters GBK-representable and document the variant prominently.

**Non-Goals:**

- Penalty stacking, challenges, animations, sound, graphical assets, new dependencies, persistence, or networking.
- Changing the existing rule that a winning final action card does not resolve its penalty.
- Changing Rust files from UTF-8 encoding to a legacy byte encoding.

## Decisions

### Select a deck variant at game construction

Introduce `DeckVariant` and pass it through setup into game construction. Standard remains exactly 108 cards; Holiday extends it with two Draw Eight cards per color and two Wild Draw Sixteen cards. Keeping the variants explicit makes standard behavior testable and avoids global configuration.

### Extend ranks instead of adding a separate effect type

Add `DrawEight` and `WildDrawSixteen` to `Rank`, and extend `Card::is_wild`, legality, color-choice validation, and effect resolution. This follows the existing compact model and lets same-rank Draw Eight cards match across colors automatically.

Wild Draw Sixteen is unrestricted and always requires a color. Draw penalties skip the target. If a penalty exceeds all drawable and recyclable cards, the target draws every available card and play continues; this prevents a large penalty from leaving partially mutated game state behind an error.

### Reuse wild selection and structured card styling

The existing human and AI wild-selection flows will recognize Wild Draw Sixteen. Rendering moves from one styled string per card to a shared span-producing helper: Draw Eight receives color plus gold accents, while Wild Draw Sixteen receives four colored segments. Text labels remain present for accessibility.

### Use a GBK-safe source palette

The themed UI uses Ratatui colors, bold/reversed modifiers, Chinese or ASCII text, and source-safe characters such as `*`, `+`, `=`, `[`, and `]`. Existing source characters that fail a GBK encode audit are replaced. README alone may use arbitrary Unicode decoration. Comments gain sparse ASCII carnival section banners rather than decorative noise on every statement.

### Give AI explicit high-card weights

Normal and hard AI use base weights 12 for Draw Eight and 15 for Wild Draw Sixteen. Under hard-mode opponent pressure they receive bonuses 18 and 22 respectively. Wild preservation and dominant-color behavior remain unchanged.

## Risks / Trade-offs

- [Ten high-penalty cards can make Holiday games highly volatile] -> Keep Standard selectable and label the variant clearly.
- [Wide decorated labels can wrap in small terminals] -> Preserve the existing minimum-size gate and keep inline card labels compact.
- [Terminal color support varies] -> Include textual card names and ASCII ornaments in addition to color.
- [GBK repertoire checks are platform-sensitive] -> Add a deterministic script-based audit using a strict GBK encoder over Rust source characters.
- [Large draws can exhaust all available cards] -> Draw as many as exist and advance the turn without error.

## Migration Plan

Add the OpenSpec artifacts, implement and verify the new variant, then release the binary normally. There is no stored data or network protocol to migrate. Rollback is a source revert; Standard games remain behaviorally compatible.

## Open Questions

None.
