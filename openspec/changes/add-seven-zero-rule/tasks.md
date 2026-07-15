## 1. Core Rules

- [x] 1.1 Add house-rule configuration, target-bearing play actions, hand-effect events, and localized validation errors
- [x] 1.2 Implement deterministic 7 swaps and directional 0 rotations with number multi-discard and immediate-win ordering
- [x] 1.3 Add core tests for enabled, disabled, invalid-target, direction, two-player, multi-discard, and victory behavior

## 2. AI and Application Flow

- [x] 2.1 Update AI action construction and implement difficulty-aware legal 7 target selection with deterministic tests
- [x] 2.2 Add the default-enabled setup toggle and pass house rules through both Standard and Holiday game constructors
- [x] 2.3 Add a cancellable human target-selection state for keyboard and command plays, including AI/image suspension and selection normalization

## 3. Presentation and Verification

- [x] 3.1 Add bilingual setup, help, picker, validation, swap, and rotation copy plus shared renderer support
- [x] 3.2 Add application, view, and screen tests for setup navigation, target interaction, dual controls, command flow, logs, and image suppression
- [x] 3.3 Run formatting, full tests, Clippy with warnings denied, and Cargo check

## 4. Zero Availability

- [x] 4.1 Specify and implement two zero cards per color in the shared Standard base deck, with Holiday inheriting the new composition
- [x] 4.2 Update bilingual deck counts and add construction and refill regression coverage
- [x] 4.3 Run formatting, full tests, Clippy with warnings denied, and Cargo check after the deck update
