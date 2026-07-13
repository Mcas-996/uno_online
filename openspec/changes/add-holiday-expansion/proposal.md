## Why

The local UNO game only offers the standard deck and a plain terminal presentation. A selectable Holiday Expansion adds a deliberately chaotic rules variant while giving the whole TUI a distinctive star-carnival identity.

## What Changes

- Add a Holiday deck variant with two Draw Eight cards in each UNO color and two unrestricted Wild Draw Sixteen cards.
- Let players choose Standard or Holiday during setup, with Holiday selected by default.
- Teach the rules engine and local AI how to play and resolve the new cards, including safe handling when fewer penalty cards remain than requested.
- Restyle the complete TUI with a GBK-safe star-carnival treatment and four-color rendering for Wild Draw Sixteen.
- Expand English and Chinese copy, README documentation, tests, and source comments for the new variant.

## Capabilities

### New Capabilities

- `holiday-expansion`: Selectable Holiday deck composition, Draw Eight and Wild Draw Sixteen rules, AI behavior, themed terminal presentation, localization, and character-set compatibility.

### Modified Capabilities

None. The repository has no synchronized main specs; the completed local-UNO change remains historical context.

## Impact

The change affects the card/rules model, game construction, AI scoring, setup state and input, localization, Ratatui rendering, README, and automated tests. No dependencies, persistence formats, networking interfaces, or external services are added.
