## ADDED Requirements

### Requirement: Matches configure the 7-0 house rule
The system SHALL offer a 7-0 house-rule setting for Standard and Holiday matches, and the local setup SHALL enable it by default.

#### Scenario: Start with the default setting
- **WHEN** a player starts a match without changing the 7-0 setting
- **THEN** the match enables 7 hand swaps and 0 hand rotation

#### Scenario: Disable the rule
- **WHEN** a player disables 7-0 before starting either deck variant
- **THEN** 7 and 0 behave as ordinary number cards

### Requirement: Seven exchanges remaining hands
When 7-0 is enabled, the system SHALL require a player who plays a 7 to choose another current player and SHALL exchange their complete remaining hands.

#### Scenario: Play a seven
- **WHEN** a player legally plays a 7 and chooses another player
- **THEN** the two players exchange their remaining hands and play advances normally

#### Scenario: Reject an invalid target
- **WHEN** a 7 play omits its target or targets the acting, unknown, or non-current player
- **THEN** the action is rejected without changing game state

### Requirement: Zero rotates hands in the play direction
When 7-0 is enabled, the system SHALL pass every complete remaining hand to the next player in the current play direction after a 0 is played.

#### Scenario: Rotate clockwise
- **WHEN** a player plays a 0 while direction is clockwise
- **THEN** each player's former hand is received by the next clockwise player

#### Scenario: Rotate counter-clockwise
- **WHEN** a player plays a 0 while direction is counter-clockwise
- **THEN** each player's former hand is received by the next counter-clockwise player

### Requirement: 7-0 composes with number multi-discard and victory
The system SHALL remove all matching number cards under the existing multi-discard rule before evaluating victory and SHALL resolve at most one 7-0 effect from the selected top card.

#### Scenario: Multiple sevens remain non-winning
- **WHEN** a selected 7 removes multiple sevens but leaves other cards in the acting hand
- **THEN** the selected target exchange occurs exactly once

#### Scenario: Multi-discard empties the hand
- **WHEN** a selected 7 or 0 removes the acting player's final cards
- **THEN** that player wins immediately and no hand exchange or rotation occurs

### Requirement: Local players and AI can complete seven plays
The system SHALL provide legal target selection for human and AI players without exposing private opponent cards.

#### Scenario: Human selects a target
- **WHEN** a human attempts to play a 7 with the rule enabled
- **THEN** a cancellable bilingual picker lists the other players by public name and hand count before submitting the play

#### Scenario: AI selects a target
- **WHEN** an AI plays a 7
- **THEN** Easy chooses a legal target randomly while higher difficulties choose among players with the fewest cards

### Requirement: 7-0 effects are observable
The system SHALL describe enabled 7-0 behavior in bilingual help and SHALL record completed swaps and rotations in the event log.

#### Scenario: Complete a hand effect
- **WHEN** a 7 swap or 0 rotation resolves
- **THEN** the visible event text identifies the effect and relevant target or direction
