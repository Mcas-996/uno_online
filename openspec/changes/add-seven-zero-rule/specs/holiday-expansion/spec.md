## MODIFIED Requirements

### Requirement: Players can select the Holiday deck
The setup screen SHALL offer Standard and Holiday deck variants, SHALL default to Holiday, and SHALL use the 112-card Standard deck containing two zero cards in each color.

#### Scenario: Start a default match
- **WHEN** a player starts a match without changing the deck field
- **THEN** the system deals from the 122-card Holiday deck

#### Scenario: Select standard play
- **WHEN** a player selects Standard and starts a match
- **THEN** the system deals from the 112-card Standard deck

### Requirement: Holiday decks contain the specified expansion cards
The Holiday deck SHALL add two Draw Eight cards in each of the four colors and two Wild Draw Sixteen cards to the 112-card Standard deck.

#### Scenario: Construct a Holiday deck
- **WHEN** the system constructs the Holiday deck
- **THEN** it contains 122 cards including eight colored zero cards, eight colored Draw Eight cards, and two Wild Draw Sixteen cards
