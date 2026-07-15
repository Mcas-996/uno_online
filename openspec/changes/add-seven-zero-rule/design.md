## Context

The authoritative `core` module currently resolves a play atomically, including the house rule that removes every matching number from the acting hand. `ai` chooses from legal actions, while `app`, `i18n`, `view`, and `screen` own local interaction and presentation. Wild cards already demonstrate a pre-submit choice overlay, but a 7 needs a player target and both 7 and 0 mutate multiple private hands.

## Goals / Non-Goals

**Goals:**

- Keep 7-0 validation and hand mutation authoritative in `core`.
- Make the rule configurable per match and enabled by default in the local setup.
- Preserve deterministic AI tests, hidden-hand boundaries, number multi-discard, and both terminal frontends.
- Surface target selection and effects in bilingual UI and event logs.
- Make zero cards as frequent as the other colored number ranks in both deck variants.

**Non-Goals:**

- Persisting setup preferences or adding CLI flags.
- Removing or redesigning the existing number multi-discard rule.
- Adding animation, networking, scoring, or UNO declaration rules.

## Decisions

### Represent house rules explicitly

Add a public `HouseRules` value containing `seven_zero`, defaulting to enabled, and thread it through game construction. Keep compatibility constructors and add variants that accept house rules, including the existing Holiday draw-rule path. This avoids tying rules to deck variants or UI state.

### Keep a play atomic and target-bearing

Extend `Action::Play` with an optional `swap_target`. When 7-0 is enabled, legal actions for a 7 contain one action per other player; core rejects missing, self, unknown, or unexpected targets. This keeps AI and UI on the same validation path and avoids adding a partially resolved turn phase.

### Resolve multi-discard before one 7-0 effect

The selected number remains the top discard while all same-number cards leave the hand. If that empties the acting hand, the existing immediate-win rule ends the round. Otherwise a selected 7 swaps the two remaining hands once, and a selected 0 passes every hand to the next player in the current direction once. Player identities, current index, direction, and draw-rule counters do not move with hands.

### Describe the effect on the play event

Add an optional `HandEffect` to `CardPlayed` instead of emitting a second action result. The effect records either the swap target or rotation direction, allowing the existing single-event application flow to produce a complete localized log entry.

### Reuse the overlay interaction pattern

Add a pending-seven target picker parallel to the wild color picker. It supports the current human's left/right controls, Enter, and Esc, and suppresses images and AI ticks while open. Playing by index from command mode enters the same picker.

### Select AI targets by difficulty

Easy chooses uniformly from legal targets. Normal, Hard, and Extreme choose among opponents with the fewest cards, using the supplied RNG for ties. Card scoring and wild color choice remain unchanged.

### Double zero cards in the shared base deck

Add a second zero for each color to the Standard deck, increasing it from 108 to 112 cards. Holiday continues to extend that base with ten expansion cards, increasing it from 118 to 122 cards. The composition applies regardless of the 7-0 toggle and to complete-deck refills; shuffling remains random and does not guarantee a zero in any specific hand.

## Risks / Trade-offs

- [Adding a field to `Action::Play` touches many call sites] -> Update constructors and tests together and centralize helpers where useful.
- [Hand rotation can accidentally reverse direction] -> Test exact player-to-player ownership for clockwise, counter-clockwise, and two-player games.
- [Setup gains another row within a fixed layout] -> Reuse the available row inside the existing 70 x 26 minimum and add render coverage.
- [A target overlay could leak AI cards] -> Display only public names and hand counts already exposed by `PublicGameState`.
- [Changing the base deck invalidates displayed counts and refill assumptions] -> Update bilingual deck labels and assert exact zero multiplicity for construction and refills.
