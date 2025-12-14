# Copilot Instructions for Gridgame Repository

## Repository Overview

This repository contains a collection of interactive video-based grid games designed for 2-player gameplay. All games run entirely in the browser with no build process or server-side code.

## Project Structure

```
Gridgame/
├── game-selector.html      # Landing page for game selection
├── index.html              # Main Cloud 9 game (full-featured with animations)
├── newg.html              # Cloud 9 alternative version (duplicate of index.html)
├── newq.html              # Cloud 9 simplified version (without animations)
├── boom.html              # Quadrant Timers game mode
├── word-color-blocks.html # Word + Color matching game
├── images/                # Challenge tile images (1.png - 25.png, 250x250px each)
└── *.md                   # Documentation files
```

## Important File Relationships

### Cloud 9 Game Variants
- **index.html**: Full-featured version with animations and all challenges
- **newg.html**: 100% duplicate of index.html (maintained for compatibility)
- **newq.html**: Simplified version without animations

**CRITICAL**: When making changes to Cloud 9 functionality, update ALL THREE files (index.html, newg.html, newq.html) consistently. See `CODE_MAINTENANCE.md` for detailed guidelines on maintaining shared code.

## Code Style and Conventions

### Technology Stack
- **Pure HTML5/CSS3/Vanilla JavaScript** - No frameworks or preprocessors
- **No build process** - Files run directly in browser
- **CDN Dependencies**:
  - Tailwind CSS: https://cdn.tailwindcss.com
  - Twemoji: https://cdn.jsdelivr.net/npm/twemoji@latest/dist/twemoji.min.js
  - Tone.js: https://cdnjs.cloudflare.com/ajax/libs/tone/14.7.77/Tone.js
  - Google Fonts: https://fonts.googleapis.com

### JavaScript Conventions
- Use vanilla JavaScript (ES6+)
- All code is embedded in `<script>` tags within HTML files
- No external JS files
- Use const/let instead of var
- Prefer arrow functions for callbacks
- Use template literals for string interpolation

### Emoji Handling
- **ALWAYS** use Twemoji library to replace emojis with SVG images
- Call `twemoji.parse()` to convert emoji text to images
- Use the `parseEmojis()` helper function for consistent rendering
- Example: `parseEmojis(element)` or `element.innerHTML = twemoji.parse(text)`

### CSS Conventions
- Inline `<style>` tags within HTML files
- Tailwind CSS utility classes for layout
- Custom CSS for game-specific styling
- Use CSS animations for transitions and effects

## 2-Player Game Mechanics

### Player Configuration
- **Player 1**: Blue color (#3498db), badge "P1"
- **Player 2**: Red color (#e74c3c), badge "P2"
- Players stored in `challengePlayers` array
- Current player tracked via `currentChallengePlayerIndex`

### Turn-Based System
- Players alternate turns after each task attempt
- Use `advanceChallengeTurn()` to switch players
- Turn indicator updates automatically with player colors
- Visual feedback: active player's card highlighted with colored shadow

### Task Completion
- Use `markTaskComplete()` to award tiles and update scores
- Use `closeTaskModal()` to close challenge modals
- Use `updateMainScore()` to update point totals
- Tiles display owner's badge (P1 or P2) with colored border

### Challenge Types
- **AI-dependent**: 'aiChallenge', 'audioAnagram' (require Gemini API key)
- **API-based**: Trivia challenges use Free Trivia DB API (opentdb.com)
- **Standalone**: Most challenges work without external APIs

## API Integration

### Gemini API
- Optional API key for AI-powered challenges
- Stored in `geminiApiKey` variable
- Key input box positioned at top-right (top: 1rem, right: 1rem, z-index: 210)
- Use `AI_REQUIRED_CHALLENGES` Set to check if challenge needs API
- `callGemini()` returns null gracefully on errors

### Free Trivia DB
- Fallback for trivia challenges when Gemini unavailable
- Endpoint: https://opentdb.com/api.php
- See `fetchTriviaQuestions()` function

## Testing Approach

### No Automated Tests
- No test framework or automated testing infrastructure
- Testing is manual and browser-based

### Manual Testing Process
1. Open HTML file directly in browser
2. Use browser DevTools console for debugging
3. Test with local video files (requires folder selection)
4. Verify functionality across browsers:
   - Chrome/Edge (recommended)
   - Firefox
   - Safari

### Browser Compatibility
- Use modern APIs (File System Access API)
- Graceful degradation where possible
- Desktop browsers recommended (mobile supported)

## Common Development Tasks

### Adding New Challenges
1. Create challenge function (e.g., `setupNewChallengeTask()`)
2. Call `markTaskComplete()` on success
3. Call `updateMainScore()` to add points
4. Use `parseEmojis()` for emoji rendering
5. Call `closeTaskModal()` to dismiss modal

### Modifying UI Elements
- Use Tailwind utility classes for layout
- Maintain responsive design principles
- Test z-index layering (modals use z-index 200+)
- Ensure mobile compatibility

### Working with Videos
- Videos loaded via File System Access API
- Use `webkitdirectory` for folder selection
- Filter for `accept="video/*"`
- All video processing is client-side

## Security Considerations

- No server-side code or data uploads
- All processing happens client-side
- No sensitive data stored or transmitted
- API keys stored only in browser memory (not persisted)
- Use CDN resources from trusted sources

## Documentation Files

- **README.md**: Main project documentation
- **2PLAYER_FUNCTIONALITY.md**: Detailed 2-player mechanics
- **CODE_MAINTENANCE.md**: Guidelines for maintaining shared code
- **DEPLOYMENT_CHECKLIST.md**: Deployment verification steps
- **CLOUD9_VERSIONS.md**: Comparison of Cloud 9 variants

## Key Implementation Details

### Score System
- Each player has score in `challengeScores` array
- Score multiplier increases by 0.25 per completion
- Scores displayed in real-time on player cards
- Use `renderChallengeHud()` to update display

### Tile Management
- 5x5 grid (25 tiles) for Cloud 9 challenges
- 4x4 grid (16 tiles) for Word Color Blocks
- Tiles track ownership via `data-owner` attribute
- Failed tiles have 60-second cooldown
- Owned tiles display player badge and colored border

### Modal System
- Challenges open in modal overlays
- Use `closeTaskModal()` for proper cleanup
- Modals auto-close after task completion (500ms delay)
- Z-index: 200+ for modal overlays

## Common Pitfalls to Avoid

1. **Don't add build tools** - Keep everything pure HTML/CSS/JS
2. **Don't forget Twemoji** - Always convert emojis to SVG images
3. **Update all three files** - Changes to Cloud 9 need to be in index.html, newg.html, AND newq.html
4. **Test in browser** - No automated tests, must verify manually
5. **Respect z-index layers** - API box (210), modals (200+), game elements (lower)
6. **Client-side only** - No server-side code or external data storage

## Deployment

- GitHub Pages is used for hosting
- Push to main branch to deploy
- All HTML files accessible directly
- No build or compilation step required
- CDN dependencies must be available

## Best Practices

1. **Minimal changes**: Prefer surgical edits over large refactors
2. **Consistency**: Maintain consistent code style with existing code
3. **Documentation**: Update relevant .md files when changing functionality
4. **Browser testing**: Always test in at least Chrome and Firefox
5. **Memory management**: Clean up event listeners and intervals
6. **Error handling**: Handle API failures gracefully
7. **Accessibility**: Maintain semantic HTML and ARIA labels where appropriate

## Quick Reference

### Key Functions
- `markTaskComplete()`: Award tile to player (lines ~3092-3113 in index.html)
- `advanceChallengeTurn()`: Switch to next player (lines ~1865-1868)
- `renderChallengeHud()`: Update player score display (lines ~1834-1857)
- `parseEmojis(element)`: Convert emojis to SVG (lines ~1771-1779)
- `callGemini(prompt)`: Call Gemini API (lines ~1888-1952)
- `fetchTriviaQuestions()`: Get trivia from API (lines ~1992-2029)

### Key Variables
- `challengePlayers`: Array of player objects
- `currentChallengePlayerIndex`: Active player index (0 or 1)
- `challengeScores`: Array of player scores
- `geminiApiKey`: Optional Gemini API key
- `AI_REQUIRED_CHALLENGES`: Set of challenges requiring API key

### Image Assets
- Challenge tiles: `images/1.png` through `images/25.png`
- All images are 250x250 pixels, PNG format, RGBA

## Getting Help

- Check existing documentation files for detailed information
- Review similar code in the same file for patterns
- Test changes manually in browser before committing
- Use browser DevTools console for debugging
