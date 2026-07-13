## ADDED Requirements

### Requirement: Players can select the Holiday deck
The setup screen SHALL offer Standard and Holiday deck variants, SHALL default to Holiday, and SHALL preserve the 108-card Standard deck.

#### Scenario: Start a default match
- **WHEN** a player starts a match without changing the deck field
- **THEN** the system deals from the 118-card Holiday deck

#### Scenario: Select standard play
- **WHEN** a player selects Standard and starts a match
- **THEN** the system deals from the unchanged 108-card Standard deck

### Requirement: Holiday decks contain the specified expansion cards
The Holiday deck SHALL add two Draw Eight cards in each of the four colors and two Wild Draw Sixteen cards to the Standard deck.

#### Scenario: Construct a Holiday deck
- **WHEN** the system constructs the Holiday deck
- **THEN** it contains 118 cards including eight colored Draw Eight cards and two Wild Draw Sixteen cards

### Requirement: Draw Eight applies a colored penalty
The system SHALL allow Draw Eight to match the active color or another Draw Eight, and SHALL make the next player draw eight cards and lose their turn.

#### Scenario: Play Draw Eight by color
- **WHEN** the current player plays a Draw Eight matching the active color
- **THEN** the next player draws eight available cards and the following player receives the turn

#### Scenario: Play Draw Eight by rank
- **WHEN** a Draw Eight is on top of the discard pile
- **THEN** a differently colored Draw Eight is a legal play

### Requirement: Wild Draw Sixteen changes color and applies a penalty
The system SHALL allow Wild Draw Sixteen regardless of cards matching the active color, MUST require one of four color choices, and SHALL make the next player draw sixteen cards and lose their turn.

#### Scenario: Play while holding the active color
- **WHEN** a player holds an active-color card and plays Wild Draw Sixteen with a color choice
- **THEN** the play is legal, the chosen color becomes active, and the next player draws sixteen available cards and loses their turn

#### Scenario: Omit the color choice
- **WHEN** a player attempts Wild Draw Sixteen without selecting a color
- **THEN** the system rejects the action without changing the game

### Requirement: Large penalties cannot deadlock the round
The system SHALL draw the full penalty when enough cards are drawable or recyclable, and SHALL draw all available cards without failing when fewer cards remain.

#### Scenario: Fewer cards remain than the penalty
- **WHEN** Draw Eight or Wild Draw Sixteen resolves with fewer drawable cards than requested
- **THEN** the target receives every available card and the turn advances normally

### Requirement: Local AI understands Holiday cards
The AI SHALL select only legal Holiday actions, SHALL choose a color for Wild Draw Sixteen, and SHALL score Draw Eight and Wild Draw Sixteen as high-impact cards.

#### Scenario: AI plays Wild Draw Sixteen
- **WHEN** an AI selects Wild Draw Sixteen
- **THEN** its action includes a legal color choice

### Requirement: The TUI presents a bilingual star-carnival theme
The setup, game table, hand, help, color picker, and result screen SHALL use a coherent star-carnival presentation, SHALL show bilingual Holiday labels, and SHALL render Wild Draw Sixteen with all four UNO colors while retaining readable text.

#### Scenario: Render a Holiday card
- **WHEN** a Draw Eight or Wild Draw Sixteen appears in the hand or discard area
- **THEN** the TUI shows its penalty value, themed ASCII ornament, and appropriate one-color or four-color styling

### Requirement: Rust source uses a GBK-representable character repertoire
All characters under `src/**/*.rs` MUST be encodable as GBK while the files remain UTF-8, and README SHALL be exempt from that character-repertoire restriction.

#### Scenario: Audit source characters
- **WHEN** the completed Rust source is encoded character-by-character with a strict GBK encoder
- **THEN** no source character fails conversion
