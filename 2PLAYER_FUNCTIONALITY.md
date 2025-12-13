# 2-Player Challenge Game Functionality

## Overview
The challenge game supports 2-player mode with turn-based gameplay where players compete to complete tasks on a 5x5 grid.

## Player Configuration
Two players are pre-configured:
- **Player 1**: Blue color (#3498db), badge "P1"
- **Player 2**: Red color (#e74c3c), badge "P2"

## Turn-Based Mechanics

### Turn Advancement
- Players alternate turns after each task attempt (success or failure)
- Current player is tracked via `currentChallengePlayerIndex`
- Turn advances automatically via `advanceChallengeTurn()` function
- Uses modulo operator to cycle between players: `(currentChallengePlayerIndex + 1) % challengePlayers.length`

### Visual Indicators
- Active player's card is highlighted with:
  - `active` CSS class
  - Upward translation (4px)
  - Colored box shadow matching player color
- Turn indicator displays: "{Player Name}'s turn"
- Turn indicator border and text color match active player

### Task Completion
When a player completes a task:
1. Tile is assigned to the player (`data-owner` attribute)
2. Player's badge (P1/P2) appears on the tile
3. Player's score increments by 1
4. Score multiplier increases by 0.25
5. HUD updates to show new scores
6. Turn advances to next player
7. Modal closes after 500ms

### Task Failure
When a player fails a task:
1. Tile is marked as failed temporarily (60 seconds)
2. ✖ symbol appears on the tile
3. Turn advances to next player
4. Tile becomes available again after timeout

## Score Tracking
- Each player's score is tracked in `challengeScores` array
- Scores displayed in real-time on player cards
- Score persists throughout the game session
- Reset via `resetChallengeGameState()` function

## Tile Ownership
- Completed tiles display owner's badge (P1 or P2)
- Owner indicated by colored border matching player color:
  - Player 1: Blue border (3px solid #3498db)
  - Player 2: Red border (3px solid #e74c3c)
- Owned tiles cannot be re-attempted

## Win Conditions
The game continues until all tiles are completed or failed. Players compete for the highest score by completing the most tasks.

## Implementation Details
- **Player setup**: Lines 1757-1769 in index.html
- **Turn management**: Lines 1865-1868 (advanceChallengeTurn)
- **HUD rendering**: Lines 1834-1857 (renderChallengeHud)
- **Task completion**: Lines 3092-3113 (markTaskComplete)
- **Task failure**: Lines 3115-3139 (markTaskFailed)
- **Tile ownership styling**: Lines 1366-1374 (CSS)
