# Code Maintenance Guide

This guide helps maintainers understand and manage the shared code between `index.html` and `newq.html`.

## Overview

Both `index.html` and `newq.html` share approximately 90% of their code:
- **51+ identical JavaScript functions**
- **Similar HTML structure**
- **Common game logic and mechanics**

## Why Not Extract to Shared Files?

We've chosen **not** to extract common code into separate JS/CSS files for these reasons:

1. **Self-contained files**: Each HTML file works independently without external dependencies
2. **No build process**: The project intentionally has no build system
3. **Deployment simplicity**: Single-file deployment is easier
4. **Function dependencies**: Many functions depend on DOM elements and global variables specific to each file
5. **Version variants**: The two versions serve different purposes (full vs. simplified)

## Maintaining Code Across Files

When making changes that should apply to both files:

### Step 1: Make Changes in index.html
Make your changes in `index.html` first (the full-featured version).

### Step 2: Identify if Changes Apply to newq.html
Determine if the changes should also be in `newq.html`:
- ✅ **Apply to both**: Core game logic, bug fixes, security updates, API changes
- ❌ **Only index.html**: New visual effects, animations, advanced features

### Step 3: Replicate Changes in newq.html
If changes apply to both:
1. Open `newq.html`
2. Find the corresponding section (use line numbers as a rough guide)
3. Apply the same changes
4. Test both files

### Step 4: Test Both Versions
Always test both files after making changes:
```bash
# Test index.html
python3 -m http.server 8000
# Open http://localhost:8000/index.html

# Test newq.html
# Open http://localhost:8000/newq.html
```

## Common Functions Reference

These functions are **identical** in both files and should be kept in sync:

### Core Utilities
- `parseEmojis()` - Converts emoji to Twemoji images
- `updateGeminiStatus()` - Updates API key status message
- `loadGeminiKey()` - Loads API key from localStorage
- `persistGeminiKey()` - Saves API key to localStorage
- `decodeHTMLEntities()` - Decodes HTML entities in text

### Game Mechanics
- `resetChallengeGameState()` - Resets game state
- `advanceChallengeTurn()` - Advances to next player's turn
- `renderChallengeHud()` - Updates player turn indicator
- `markTaskComplete()` - Awards squares to players
- `markTaskFailed()` - Handles failed challenges
- `updateMainScore()` - Updates main score display
- `startScoreDecay()` - Starts score decay timer
- `stopScoreDecay()` - Stops score decay timer

### API Integration
- `callGemini()` - Calls Gemini AI API
- `fetchTriviaQuestions()` - Fetches trivia from API

### Challenge Setup Functions
- `setupAiChallengeTask()`
- `setupAudioAnagramTask()`
- `setupBingoBuilderTask()`
- `setupBlowbackTask()`
- `setupMatchPairsTask()`
- `setupMemoryGameTask()`
- `setupReflexTestTask()`
- `setupTrivia1Task()`
- `setupTrivia3Task()`

### Modal and UI
- `openTask()` - Opens challenge modal
- `closeTaskModal()` - Closes challenge modal
- `showWinLossScreen()` - Shows challenge result
- `makeDraggable()` - Makes elements draggable

### Story Maker (Video) Functions
- `startStoryMakerGame()`
- `loadStoryMakerScene()`
- `populateStoryMakerClipGrid()`
- `finishScene()`
- `renderArrangementPhase()`
- `playFinalMovie()`
- `finalizeMovie()`

### Trivia Game Functions
- `startPlayerTurn()`
- `displayTriviaQuestion()`
- `endTriviaGame()`
- `setupScores()`
- `updateScore()`
- `renderScores()`
- `speak()` - Text-to-speech

## Key Differences to Preserve

### In index.html ONLY (DO NOT add to newq.html):
1. **CSS Animations**:
   - `@keyframes gradientBG`
   - `@keyframes strobe`
   - `@keyframes float`

2. **Video Effects**:
   - `.video-full-screen` styles
   - `.video-strobe`, `.video-bw`, `.video-sepia`, `.video-invert`, `.video-reversed`

3. **Responsive Media Queries**:
   - Touch device optimizations (`@media (pointer: coarse)`)
   - Mobile-specific button sizes

4. **Advanced Features**:
   - Pressure Front Challenge (`setupPressureFrontTask()`)
   - On-screen tally overlay

### In newq.html ONLY (Simplifications):
- Static gradient background (no animation)
- No video effect filters
- No touch optimizations
- Fewer challenge types

## Anti-Patterns to Avoid

❌ **Don't** make changes in only one file without considering the other
❌ **Don't** add new features to newq.html that should only be in index.html
❌ **Don't** remove features from index.html without documenting why
❌ **Don't** forget to test both files after changes

## Bug Fixes and Security Updates

**ALWAYS** apply these to both files:
- Security vulnerabilities
- API changes
- Bug fixes in core game logic
- Data handling issues
- Memory leaks
- Performance improvements

## Version Control Best Practices

When committing changes:
1. **Separate commits**: One for index.html, one for newq.html
2. **Clear messages**: "Fix scoring bug in index.html" and "Fix scoring bug in newq.html"
3. **Or combine**: "Fix scoring bug in both Cloud 9 versions"
4. **Reference both**: In PR descriptions, always mention if changes affect both files

## Future Refactoring Ideas

If the duplication becomes unmanageable, consider:

1. **Build System**: Add a build process to generate both files from a single source
2. **Feature Flags**: Use configuration to toggle features instead of separate files
3. **Shared Module**: Extract truly independent utilities to `js/game-common.js`
4. **Template System**: Use a templating system to generate variants
5. **Consolidation**: Merge into a single file with runtime feature detection

## Questions?

When in doubt:
- Check `CLOUD9_VERSIONS.md` for version differences
- Review git history to see how similar changes were made previously
- Test both files thoroughly before committing
