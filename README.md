# Gridgame

A collection of interactive video-based grid games for 2 players.

## 🎮 Game Modes

### 1. Cloud 9 Video Player (Classic)
**File:** `index.html` (full version), `newq.html` (simplified version)

The original grid-based challenge game featuring:
- 2-player turn-based gameplay
- Multiple mini-games and challenges
- Video integration with local video selection
- Score tracking and tile ownership
- Various challenge types: Trivia, Match Pairs, Reflex Test, Bingo, and more

**Recent Updates:**
- ✅ Removed broken game modes: Splash Click, Clip Sequencer, Memory Challenge
- ✅ Updated "Don't Blink" challenge to "Watch Closely"
- ✅ Fixed emoji rendering with Twemoji library
- ✅ Repositioned API key input box to top-right

### 2. Quadrant Timers - Full Ferocity (NEW)
**File:** `boom.html`

An intense two-quadrant video-based game mode with:
- Dual video quadrants with synchronized timers
- Event-based challenges (bulge, strobe, overlays)
- Theme customization (8 different visual themes)
- Tally tracking system
- Grid choice challenges with 2x2 video selection

**How to Use:**
1. Open `boom.html` in a browser
2. Select a local video folder using the folder picker
3. Choose which quadrants to activate (tap to play)
4. Select your preferred theme (Velvet, Noir, Crimson, etc.)
5. Watch as timed events trigger across quadrants

### 3. Word Color Blocks (NEW)
**File:** `word-color-blocks.html`

A brand new two-player word + color matching game featuring:
- **4x4 grid** (16 tiles) for turn-based tile capture
- **Video clips** with word and color overlays
- Players must identify if word + color combinations are CORRECT or INCORRECT
- **Special "YOU GOT BLOCKED" tiles** with host-judged challenges
- **Block challenges** include tasks like:
  - Tell a joke
  - Do jumping jacks
  - Name countries
  - Sing songs
  - And more!
- **Host controls** (tick ✓ or cross ✗) to judge block challenge success
- **Turn-based gameplay** with automatic player switching
- **Win condition:** Player with most tiles wins when all tiles are claimed

**Game Rules:**
1. Players take turns selecting tiles from the 4x4 grid
2. For normal tiles:
   - Watch the video clip with word + color overlay
   - Decide if the combination is correct (word matches color) or incorrect
   - Correct answer = win the tile
   - Incorrect answer = lose turn
3. For blocked tiles (🚫):
   - Complete a special challenge
   - Host judges success with tick or cross
   - Success = win the tile
   - Failure = lose turn
4. Game ends when all tiles are owned
5. Player with most tiles wins!

## 🚀 Getting Started

### Quick Start (No Installation Required)

All games run entirely in the browser with no build process needed!

1. **Clone or download** this repository
2. **Open any HTML file** directly in your web browser:
   - For game selection menu: `game-selector.html`
   - For classic challenges: `index.html`
   - For quadrant timers: `boom.html`
   - For word color blocks: `word-color-blocks.html`

### Video Setup

All games require local video files:
1. Prepare a folder with video files (MP4, WebM, etc.)
2. When prompted, use the file/folder picker to select your videos
3. The game will load and use these videos for challenges

### Deployment (GitHub Pages)

This repository is configured for GitHub Pages deployment:
1. Push changes to the main branch
2. GitHub Pages automatically serves the HTML files
3. Access via: `https://[username].github.io/Gridgame/`

**Direct Links:**
- Game Selector: `/game-selector.html`
- Classic Mode: `/index.html`
- Boom Mode: `/boom.html`
- Word Color Blocks: `/word-color-blocks.html`

## 📋 Recent Changes

### December 2024 - Major Update

#### Removed Broken Game Modes
- ❌ Splash Click (non-functional)
- ❌ Clip Sequencer (pool never appears at end)
- ❌ Memory Challenge (selection step broken)

#### Added New Features
- ✅ **Word Color Blocks** - Brand new 2-player game
- ✅ **Boom.html Integration** - Quadrant timers fully deployed
- ✅ **Game Selector** - Landing page for easy game selection
- ✅ **Wording Updates** - Changed "Don't Blink" to "Watch Closely"

#### Bug Fixes & Improvements
- ✅ Emoji rendering with Twemoji (cross-platform consistency)
- ✅ API key box repositioned to top-right
- ✅ 2-player functionality verified and working
- ✅ All HTML files validated and balanced

## 🎯 Game Files Overview

| File | Description | Players | Status |
|------|-------------|---------|--------|
| `game-selector.html` | Landing page with game selection | - | ✅ New |
| `index.html` | Main Cloud 9 game (full version) | 2 | ✅ Active |
| `newq.html` | Cloud 9 simplified version (no animations) | 2 | ✅ Active |
| `boom.html` | Quadrant Timers mode | 1-2 | ✅ New |
| `word-color-blocks.html` | Word + Color matching game | 2 | ✅ New |

## 🛠️ Technical Details

### Technologies Used
- **HTML5** with semantic markup
- **CSS3** with animations and gradients
- **Vanilla JavaScript** (no frameworks)
- **Tailwind CSS** (via CDN)
- **Twemoji** for emoji rendering
- **Tone.js** for audio synthesis (in classic mode)

### Browser Compatibility
- ✅ Chrome/Edge (recommended)
- ✅ Firefox
- ✅ Safari
- ⚠️ Mobile browsers (touch controls supported, but desktop recommended)

### File Picker API
Uses the modern File System Access API for local video selection:
- Folder picker: `webkitdirectory` attribute
- Video filtering: `accept="video/*"`
- No uploads - all processing is client-side

## 📝 For Developers

### Project Structure
```
Gridgame/
├── game-selector.html      # Landing page
├── index.html              # Main game (full version)
├── newq.html              # Simplified version
├── boom.html              # Quadrant timers
├── word-color-blocks.html # Word color game
├── images/                # Challenge tile images (1.png - 25.png)
├── README.md              # This file
└── CLOUD9_VERSIONS.md     # Version comparison guide
```

### No Build Process
- Pure HTML/CSS/JS
- All dependencies loaded via CDN
- No npm, webpack, or compilation needed
- Just open in browser to test

### Adding New Game Modes
1. Create new HTML file
2. Include necessary CDN links (Tailwind, etc.)
3. Implement game logic in embedded `<script>` tag
4. Add entry to `game-selector.html`

## 🔒 Security

- ✅ No server-side code
- ✅ No data uploaded or stored
- ✅ All video processing is local/client-side
- ✅ No external API calls (except CDN resources)

## 📄 License

This project is part of Peterjbs/Gridgame repository.

## 🤝 Contributing

Feel free to open issues or submit pull requests for:
- Bug fixes
- New game modes
- UI/UX improvements
- Documentation updates

---

**Enjoy the games! 🎮**
