## 1. Holiday Rules

- [x] 1.1 Add deck variants, Holiday ranks, exact 118-card deck construction, and public game construction support
- [x] 1.2 Implement Draw Eight, unrestricted Wild Draw Sixteen, color selection, turn skipping, and safe partial penalties
- [x] 1.3 Add core tests for composition, legality, effects, insufficient cards, and final-card wins

## 2. Application and AI

- [x] 2.1 Add the default-Holiday setup selector and pass its value into new matches
- [x] 2.2 Add bilingual deck and card copy plus Holiday-aware event and help text
- [x] 2.3 Add explicit Holiday card AI weights, color selection, and strategy tests

## 3. Star-Carnival Presentation

- [x] 3.1 Build shared one-color and four-color styled card spans for the hand and discard area
- [x] 3.2 Restyle setup, table, help, color picker, and result screens with GBK-safe star-carnival text and terminal colors
- [x] 3.3 Add TUI tests for setup selection, Holiday labels, card styles, bilingual rendering, and minimum-size behavior

## 4. Documentation and Quality

- [x] 4.1 Expand README with a decorative Holiday overview, deck composition, setup instructions, and rules while preserving existing edits
- [x] 4.2 Add restrained ASCII carnival module/section comments and remove source characters that fail strict GBK encoding
- [x] 4.3 Run the GBK audit, formatting check, tests, Clippy, and OpenSpec verification; resolve all findings
