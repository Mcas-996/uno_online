## Why

The local game already embraces optional house-rule play, but it lacks UNO's popular 7-0 variant for exchanging and rotating hands. Adding a per-match toggle makes that interaction available without forcing it on players who prefer the current rules.

## What Changes

- Add a default-enabled 7-0 house-rule toggle to local match setup for both deck variants.
- Increase each color's zero cards from one to two in every match so zero effects appear as often as other number ranks.
- Require a player who plays a 7 to choose another player and exchange their remaining hands.
- Rotate every remaining hand in the current play direction when a 0 is played.
- Preserve same-number multi-discard behavior, resolve the selected 7 or 0 only once, and keep immediate victory when the play empties the hand.
- Add legal AI target selection, bilingual target-selection UI, help text, validation errors, and event logs.

## Capabilities

### New Capabilities

- `seven-zero-rule`: Configurable 7 hand swaps and 0 directional hand rotation across the rules engine, local AI, and TUI.

### Modified Capabilities

- `holiday-expansion`: Standard contains 112 cards and Holiday contains 122 cards after doubling each colored zero.

## Impact

The change affects the game action and event types, deck composition, game construction and hand mutation, AI action selection, setup and overlay state, bilingual copy, shared rendering, and automated tests. It adds no dependencies, persistence format, networking behavior, or CLI options.
