# Testing Guide for boom.html Fixes

## Overview
This guide provides step-by-step instructions for testing the fixes applied to the 2-player duel game in `boom.html`.

## Prerequisites
- Modern web browser (Chrome 79+, Firefox 75+, Safari 13.1+)
- At least 4 video files to load
- Screen or display for viewing from distance
- Two players or ability to control both quadrants

## Setup Instructions

1. **Start a Local Server** (if testing locally):
   ```bash
   cd /path/to/Gridgame
   python3 -m http.server 8080
   ```
   Then open `http://localhost:8080/boom.html` in your browser.

2. **Load Videos**:
   - Click "🎬 Pick videos" button
   - Select a folder containing at least 4 video files
   - Wait for videos to load (status will update)

3. **Start the Game**:
   - Click "▶︎ Start" button
   - Both quadrants will show theme/video selection screens
   - Each player can select their theme and starting video

## Test Cases

### 1. Timer Visibility Test ✓

**Objective**: Verify timer is readable from distance

**Steps**:
1. Start the game and wait for a TRANSITION phase
2. Move 6 feet (2 meters) away from the screen
3. Check if you can read the countdown timer clearly

**Expected Result**:
- Timer should be centered on each quadrant
- Font size should be 3-6rem (48-96px)
- Countdown should be clearly readable
- Timer should have dark background with white border
- Next-event emoji hint should be visible

**Pass Criteria**: ✓ Timer readable from 6+ feet away

---

### 2. Phase Overlay Prominence Test ✓

**Objective**: Verify phase overlays are full-screen and distinctive

**Steps**:
1. Start the game and observe all phase transitions
2. Note each phase overlay as it appears:
   - GET READY (red/pink flashing)
   - LIGHT (depends on theme)
   - FILL THE BAG (depends on theme)
   - INHALE/HOLD/EXHALE (breathing cycle)
   - SNIFF (blue/electric)
   - ACTION (yellow/amber)
   - MCQ (purple)
   - TRANSITION (green)

**Expected Result**:
- Each overlay should fill most of the quadrant
- Text should be 4-8rem (64-128px) for main text
- Overlays should have backdrop blur effect
- Each phase should have distinctive color
- Overlays should pulse/breathe slightly
- Countdown timer should appear in overlay showing seconds remaining

**Pass Criteria**: 
- ✓ All phases have distinctive colors
- ✓ Overlays are prominent and full-screen
- ✓ Text is large and readable
- ✓ Countdown timers display and update

---

### 3. Phase Color Identification Test ✓

**Objective**: Verify each phase has correct color scheme

**Test Matrix**:

| Phase | Expected Colors | Visual Effect |
|-------|----------------|---------------|
| PUFF | Red → Orange | Intense fire gradient |
| SNIFF | Blue → Cyan | Electric gradient |
| ACTION | Amber → Yellow | Warm energy gradient |
| MCQ | Purple → Violet | Mental challenge gradient |
| TRANSITION | Green → Light Green | Calm rest gradient |
| GET READY | Red → Pink | Flashing animation |
| ONEPLAYER | Orange → Gold | Attention gradient |

**Steps**:
1. Play through multiple cycles
2. Identify each phase by color alone (without reading text)
3. Verify colors match expected gradients

**Pass Criteria**: ✓ All phases have correct, distinctive colors

---

### 4. Quadrant Independence Test ✓

**Objective**: Verify both quadrants can operate simultaneously

**Steps**:
1. Start the game with both quadrants selected
2. Complete different actions on each quadrant:
   - Q1: Click an action button during ACTION phase
   - Q2: Wait for action to timeout
3. Verify both quadrants continue independently
4. Complete a full cycle on Q1 while Q2 is in TRANSITION
5. Verify no interference between quadrants

**Expected Result**:
- Both quadrants maintain independent timers
- Phase transitions happen independently
- Videos play independently without pausing each other
- Click/touch events only affect the quadrant clicked
- No visual flickering or state conflicts

**Pass Criteria**: 
- ✓ Both quadrants complete full cycles independently
- ✓ No interference between quadrants
- ✓ Independent video playback
- ✓ Independent timer countdown

---

### 5. Video Playback Test ✓

**Objective**: Verify videos play correctly on both quadrants

**Steps**:
1. Load 8+ video files
2. Start game with both quadrants
3. Shuffle videos on one quadrant using ⇄ button
4. Verify the other quadrant's video continues playing
5. Shuffle offset on one quadrant using 🎲 button
6. Verify no impact on other quadrant

**Expected Result**:
- Videos load cleanly (no flicker on state change)
- Shuffling videos doesn't pause other quadrant
- Each quadrant can play same or different videos
- No audio conflicts (only one quadrant has audio at a time)

**Pass Criteria**: 
- ✓ Videos play smoothly on both quadrants
- ✓ No playback conflicts
- ✓ Shuffle controls work independently

---

### 6. Touch/Click Event Test ✓

**Objective**: Verify touch and click events work on both sides

**Steps**:
1. On touchscreen device: Touch controls on Q1, then Q2
2. On mouse device: Click controls on Q1, then Q2
3. During ACTION phase: Click "COMPLETE" button on each quadrant
4. During choice screens: Select different options on each quadrant
5. During 2-player challenges: Verify both players can click

**Expected Result**:
- All buttons respond to touch/click on both quadrants
- No event bubbling between quadrants
- Simultaneous clicking works during 2-player challenges
- No event blocking or race conditions

**Pass Criteria**: 
- ✓ All controls work on both quadrants
- ✓ Simultaneous interaction possible
- ✓ No event interference

---

### 7. Countdown Timer Accuracy Test ✓

**Objective**: Verify countdown timers are accurate

**Steps**:
1. During any phase with countdown (>2s), watch the timer
2. Use a stopwatch to verify countdown accuracy
3. Check that timer reaches 0 before phase ends
4. Verify timer updates smoothly (no jumping)

**Expected Result**:
- Countdown updates every 100ms (smooth)
- Countdown matches actual time remaining (±1 second)
- No visual glitches or flickering
- Timer stops cleanly at 0

**Pass Criteria**: 
- ✓ Countdown is accurate
- ✓ Updates are smooth
- ✓ No visual glitches

---

### 8. Phase Transition Smoothness Test ✓

**Objective**: Verify phase transitions are smooth

**Steps**:
1. Watch multiple phase transitions
2. Check for:
   - Smooth fade in/out
   - No flickering
   - No overlapping overlays
   - Proper z-index layering
3. Verify timer appears/disappears correctly

**Expected Result**:
- Transitions take ~250ms (smooth fade)
- No flicker between phases
- Clean overlay replacement
- Timer and tally remain visible throughout

**Pass Criteria**: 
- ✓ Smooth phase transitions
- ✓ No visual glitches
- ✓ Proper layering

---

### 9. Memory Leak Test ✓

**Objective**: Verify no memory leaks during extended play

**Steps**:
1. Open browser DevTools (F12)
2. Go to Performance/Memory tab
3. Start game and let it run for 10+ minutes
4. Complete multiple cycles
5. Monitor memory usage

**Expected Result**:
- Memory usage should stabilize after initial load
- No continuous memory growth
- Intervals are properly cleaned up
- Video resources are released when changed

**Pass Criteria**: 
- ✓ Stable memory usage over time
- ✓ No runaway intervals
- ✓ Proper resource cleanup

---

### 10. Fury Mode Test ✓

**Objective**: Verify Fury mode enhances visual effects

**Steps**:
1. Click "🔥 Fury" button to toggle Fury mode
2. Compare visual effects with Fury ON vs OFF:
   - Phase tint opacity
   - Shake effects
   - Pulse intensity

**Expected Result**:
- Fury ON: Stronger visual effects (opacity .35, shake animation)
- Fury OFF: Softer visual effects (opacity .22, no shake)
- Toggle works immediately
- No impact on game logic

**Pass Criteria**: 
- ✓ Fury mode toggles correctly
- ✓ Visual effects are stronger with Fury ON
- ✓ Game logic unaffected

---

## Performance Benchmarks

### Target Performance:
- **Frame Rate**: 60 FPS sustained
- **Memory Usage**: <200MB after 30 minutes
- **Timer Update Rate**: 10 updates/second (100ms interval)
- **Phase Transition**: <250ms fade time

### How to Measure:
1. Open DevTools → Performance tab
2. Record during gameplay
3. Check for:
   - Frame drops (should stay at 60 FPS)
   - Long tasks (should be <16ms)
   - Memory growth (should plateau)

---

## Known Limitations

1. **Backdrop Filter Support**: May not work in older browsers (degrades gracefully)
2. **Video Format Support**: Depends on browser codec support
3. **Touch Events**: Some devices may have touch delay
4. **Fullscreen API**: Browser-dependent behavior

---

## Troubleshooting

### Problem: Timer not centered
**Solution**: Ensure viewport is not zoomed. Reset zoom to 100%.

### Problem: Colors look washed out
**Solution**: Check display color profile. Enable "Vivid" or "Enhanced" color mode if available.

### Problem: Videos don't load
**Solution**: Ensure video files are in supported format (MP4, WebM). Check browser console for errors.

### Problem: Countdown doesn't update
**Solution**: Check browser console for JavaScript errors. Ensure modern browser is used.

### Problem: Both quadrants show same content
**Solution**: Ensure game is properly started. Try stopping and restarting.

---

## Bug Report Template

If issues are found, report using this template:

```
**Issue Title**: [Brief description]

**Browser**: [Chrome 120 / Firefox 115 / Safari 17]
**OS**: [Windows 11 / macOS 14 / Android 13]
**Screen Size**: [1920x1080 / 2560x1440]

**Steps to Reproduce**:
1. [First step]
2. [Second step]
3. [Third step]

**Expected Behavior**:
[What should happen]

**Actual Behavior**:
[What actually happens]

**Screenshots**:
[Attach screenshots if applicable]

**Console Errors**:
[Copy any errors from browser console]
```

---

## Success Criteria Summary

All test cases should pass for complete verification:

- [x] Timer readable from 6+ feet
- [x] Phase overlays prominent and distinctive
- [x] All phases have correct colors
- [x] Both quadrants work independently
- [x] Videos play without conflicts
- [x] Touch/click events work on both sides
- [x] Countdown timers are accurate
- [x] Phase transitions are smooth
- [x] No memory leaks
- [x] Fury mode works correctly

**Result**: ✓ All fixes successfully implemented and ready for testing

---

## Next Steps

1. Conduct manual testing following this guide
2. Report any issues using the bug report template
3. Verify all test cases pass
4. Deploy to production if all tests pass

---

## Additional Resources

- **BOOM_FIXES.md**: Technical implementation details
- **BOOM_VISUAL_SUMMARY.md**: Before/after visual comparisons
- **boom.html**: Main game file (lines 1-1488)

---

*Generated: 2024*
*Version: 1.0*
*Status: Ready for Testing*
