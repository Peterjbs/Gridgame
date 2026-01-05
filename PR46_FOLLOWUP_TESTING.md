# PR #46 Follow-up Testing Guide

## Overview
This document provides comprehensive testing instructions for the 5 minigame fixes completed as follow-up to PR #46.

## Testing Environment Setup

### Required
- **Desktop browsers**: Chrome, Firefox, Safari (macOS)
- **iPad**: iPad with Safari (iOS 13+) for iPad-specific testing
- **Test videos**: At least 8 video files of varying lengths (30 seconds to 2+ minutes recommended)

### Setup Steps
1. Open `index.html` in your test browser
2. Click "Choose video folder" and select your test video directory
3. Verify videos load in the background video player
4. Ready to test minigames!

---

## Test 1: Avatar Sequence Memory 🧠

### What Changed
- Animation speed reduced from 1000ms to 500ms (50% faster)
- Highlight duration reduced from 500ms to 250ms

### Test Steps
1. Click on a challenge tile
2. If it's not Avatar Sequence, keep trying until you get it
3. Click "Start" to begin the minigame
4. **Observe**: The 3x3 grid tiles should flash in sequence
5. **Expected**: Each tile highlights for ~0.5 seconds (was 1 second)
6. **Expected**: Total sequence display time is faster than before

### Pass Criteria
- ✅ Sequence animates at faster pace (500ms per tile)
- ✅ Tiles highlight briefly (250ms)
- ✅ Gameplay still playable and not too fast
- ✅ Player can click tiles in correct order to win

### Test Results
- **Chrome/Firefox/Safari**: ___________
- **iPad Safari**: ___________

---

## Test 2: Timestamp Match ⏱️

### What Changed
- Removed 20-minute video requirement (now accepts 30+ seconds)
- Simplified jump logic (10 seconds or 10% of duration)
- Increased tolerance from 0.5s to 1.0s
- Extended view time from 2s to 3s
- Added proper URL cleanup

### Test Steps
1. Start Timestamp Match challenge
2. **Test with short video** (30 seconds - 2 minutes)
3. Watch the 3-second target clip
4. Observe video jumping around every 2 seconds
5. Click "Click when it matches!" when you think you see the target
6. Check result message

### Pass Criteria
- ✅ Works with videos as short as 30 seconds
- ✅ No error about "must be 20 minutes long"
- ✅ Target clip shows for 3 seconds
- ✅ Video jumps at least 10 seconds away
- ✅ Success threshold is 1 second (not 0.5)
- ✅ No memory leaks (check browser DevTools)

### Test Results
- **Chrome/Firefox/Safari**: ___________
- **iPad Safari**: ___________

---

## Test 3: Higher or Lower 📊

### What Changed
- Redesigned layout from vertical to horizontal
- Previous item (left) - Current item (center) - Buttons (right)
- Added color-coded boxes (blue for previous, yellow for current)
- Improved button styling with emojis

### Test Steps
1. Start Higher or Lower challenge
2. **Observe layout**:
   - Blue box on LEFT: Previous item with view count
   - Yellow box in CENTER: Current item with "???"
   - Buttons on RIGHT: "📈 Higher" and "📉 Lower" vertically stacked
3. Make a guess
4. Check feedback message
5. Continue for 5 rounds or until wrong

### Pass Criteria
- ✅ Horizontal layout (not vertical stacking)
- ✅ Previous item clearly shows views on left
- ✅ Current item in center with "???"
- ✅ Higher/Lower buttons on right
- ✅ Color coding makes distinction clear
- ✅ Layout is responsive (works on narrow screens)

### Test Results
- **Chrome/Firefox/Safari**: ___________
- **iPad Safari**: ___________

---

## Test 4: Bingo & Mini Bingo 🎲🎯

### What Changed
- Exactly 15 random prompts shown (was 12 or all)
- Increased font sizes throughout:
  - Instructions: 1.1rem
  - Prompt items: 1.05rem
  - Card preview: 1.05rem
  - Headings: 1.2rem
- Mini Bingo cells: 70px minimum height (was 60px)

### Test Steps - Bingo
1. Start Bingo challenge
2. Click "Start Building"
3. **Count prompts in list**: Should be exactly 15
4. **Check font sizes**: Should be noticeably larger than default
5. Select 6 prompts (click to toggle selection)
6. Click "Create Card"
7. Mark tiles on floating card
8. Mark all 6 to complete

### Test Steps - Mini Bingo
1. Start Mini Bingo challenge
2. Click "Start Building"
3. **Count prompts in list**: Should be exactly 15
4. **Check font sizes**: Should be larger
5. Select 4 prompts
6. Click "Create Card"
7. Mark all 4 tiles to complete

### Pass Criteria
- ✅ Exactly 15 prompts displayed (count them!)
- ✅ Font sizes visibly larger than before
- ✅ Text is readable on iPad without zooming
- ✅ Card preview updates as you select
- ✅ Completion awards tile correctly

### Test Results
- **Bingo - Chrome/Firefox/Safari**: ___________
- **Bingo - iPad Safari**: ___________
- **Mini Bingo - Chrome/Firefox/Safari**: ___________
- **Mini Bingo - iPad Safari**: ___________

---

## Test 5: Video Quarter Puzzle 🧩 (CRITICAL iPad Test)

### What Changed
**MAJOR REWRITE**: Replaced 4 simultaneous video elements with canvas-based approach
- 4 `<canvas>` elements instead of 4 `<video>` elements
- 1 hidden `<video>` element shared across all quarters
- Frames drawn to canvas at ~10 fps
- Prevents iPad "X videos failed to load" error

### Test Steps
1. **iPad Safari Test** (MOST IMPORTANT):
   - Open index.html on iPad Safari
   - Start Video Quarter Puzzle challenge
   - Click "Start Puzzle"
   - **CRITICAL**: Check browser console for errors
   - **Expected**: NO "failed to load" errors
   - **Expected**: All 4 quarters show cycling video frames
2. Observe 4 quarters showing different video clips
3. Each quarter cycles through different 5-second clips
4. Click a quarter to lock it (should show green border)
5. Lock all 4 quarters before 60 seconds
6. Check completion message

### Pass Criteria - iPad Safari (CRITICAL)
- ✅ NO "X videos failed to load" error in console
- ✅ NO video playback errors
- ✅ All 4 quarters display cycling video frames
- ✅ Video frames update smoothly (~10 fps is acceptable)
- ✅ Clicking quarters locks them (green border)
- ✅ Timer counts down from 60 seconds
- ✅ Locking all 4 awards tile and points
- ✅ No crashes or freezes

### Pass Criteria - Desktop
- ✅ All 4 quarters show cycling videos
- ✅ Click to lock works correctly
- ✅ Timer works
- ✅ Completion awards tile
- ✅ No console errors

### Test Results
- **Chrome/Firefox/Safari**: ___________
- **iPad Safari** (MOST IMPORTANT): ___________

### Debugging Tips (if iPad test fails)
1. Open Safari DevTools on iPad (Settings > Safari > Advanced > Web Inspector)
2. Connect iPad to Mac and use Safari's Develop menu
3. Check Console tab for errors
4. Check Network tab for video loading issues
5. If quarter shows black/frozen: Check canvas size and video readyState

---

## Overall Integration Test

### Full Gameplay Test
1. Start a new game on iPad
2. Play through multiple challenges including all 5 fixed minigames
3. Verify no regressions in other challenges
4. Check that:
   - Touch targets work correctly
   - Exit buttons function
   - Tiles award properly
   - Score updates correctly
   - Turn switching works
   - No memory leaks (play 10+ challenges)

### Pass Criteria
- ✅ All 5 fixed minigames work on iPad
- ✅ No regressions in other challenges
- ✅ Overall gameplay smooth and responsive
- ✅ No console errors during extended play
- ✅ Memory usage stable (check DevTools Performance)

---

## Browser Compatibility Matrix

| Minigame | Chrome | Firefox | Safari | iPad Safari |
|----------|--------|---------|--------|-------------|
| Avatar Sequence | ☐ | ☐ | ☐ | ☐ |
| Timestamp Match | ☐ | ☐ | ☐ | ☐ |
| Higher or Lower | ☐ | ☐ | ☐ | ☐ |
| Bingo | ☐ | ☐ | ☐ | ☐ |
| Mini Bingo | ☐ | ☐ | ☐ | ☐ |
| Video Quarter Puzzle | ☐ | ☐ | ☐ | ☐ CRITICAL |

Legend: ☑️ Pass | ☐ Not Tested | ❌ Fail

---

## Performance Benchmarks

### Video Quarter Puzzle Performance
Expected performance on iPad:
- Canvas rendering: ~10 fps per quarter
- Video decoding: 1 video at a time (sequential)
- Memory usage: Stable (URLs cleaned up)
- CPU usage: Moderate (acceptable for gameplay)

**If performance is poor**:
- Check iPad model (older iPads may struggle)
- Reduce test video resolution/bitrate
- Check for memory leaks in DevTools

---

## Known Limitations

1. **Video Quarter Puzzle**: Canvas rendering at ~10 fps (not 30 fps like native video)
2. **Avatar Sequence**: Fast animation may be challenging for some players
3. **Timestamp Match**: Requires videos at least 30 seconds long
4. **All minigames**: No automated tests (manual testing required)

---

## Issue Reporting Template

If you find issues, report them with this format:

```
**Minigame**: [Name]
**Browser**: [Browser + Version]
**Device**: [Device model if iPad]
**Issue**: [Description]
**Steps to Reproduce**:
1. [Step 1]
2. [Step 2]
3. [Step 3]
**Expected**: [What should happen]
**Actual**: [What actually happens]
**Console Errors**: [Any errors from DevTools console]
**Screenshots**: [If applicable]
```

---

## Sign-off

**Tester Name**: ___________________
**Date**: ___________________
**Overall Result**: PASS ☐ / FAIL ☐ / PARTIAL ☐

**Critical iPad Safari Test (Video Quarter Puzzle)**:
- PASS ☐ / FAIL ☐
- Notes: ___________________

**Recommendation**:
- ☐ Ready to merge
- ☐ Needs fixes (details above)
- ☐ Needs additional testing

**Signature**: ___________________
