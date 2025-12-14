# boom.html - Validation Checklist

## Two-Player Ready Flow
- [ ] **Both players ready gate displays on Start**
  - Ready gate overlay appears with Player 1 and Player 2 sections
  - Each player has independent "READY" button
  - Status shows "NOT READY" initially
  
- [ ] **Ready button toggles work correctly**
  - Clicking READY button toggles state (READY ✓ / NOT READY)
  - Button changes color when ready (green)
  - Player panel highlights when ready (green border/glow)
  - Each player can toggle independently
  
- [ ] **Start game button appears only when both ready**
  - START GAME button hidden initially
  - Button appears with pulse animation when both players ready
  - Button is large and touch-friendly (pulsing green)
  
- [ ] **Game starts immediately when START GAME clicked**
  - Both players can begin selecting theme/video simultaneously
  - No arbitrary timer delay
  - Video selection overlays appear on both quadrants
  
- [ ] **Both players' guides show simultaneously**
  - Initial video selection grid visible on both sides
  - Theme selection works on both quadrants
  - No single-player-only loading state

## Overlay Non-Overlap & Styling
- [ ] **Overlays use minimal transparent design**
  - No heavy backgrounds or borders
  - Large text with strong drop shadows
  - No blur effects or opaque boxes
  - Text is primary focus
  
- [ ] **Phase overlays stay within quadrants**
  - Player 1 overlays only in left quadrant
  - Player 2 overlays only in right quadrant
  - No cross-quadrant overlap
  - Each overlay constrained to parent quadrant
  
- [ ] **Z-index layering is correct**
  - Confetti: z-index 999
  - Ready gate: z-index 1000
  - Load round: z-index 1000
  - First click: z-index 300
  - Action choice: z-index 250
  - Overlays: z-index 200
  - Timer: z-index 150
  - Phase tint: z-index 50
  
- [ ] **Text is readable and non-obtrusive**
  - Large text sizes (4rem-8rem for main, 2rem-3.5rem for secondary)
  - Strong text shadows prevent video bleed-through
  - Simple uppercase formatting
  - No distracting animations on text

## Seamless Video Transitions
- [ ] **No TRANSITION label/overlay appears**
  - During transition periods, no overlay text displayed
  - Only subtle phase tint visible
  - Video remains in focus and unobstructed
  
- [ ] **Videos transition immediately**
  - Next video starts as soon as current phase ends
  - No pause or downtime between videos
  - Smooth handoff between clips
  
- [ ] **Timer continues showing countdown**
  - Timer displays remaining seconds during transition
  - Next event emoji preview shows
  - No "TRANSITION" text label
  
- [ ] **Both players transition independently**
  - Each quadrant transitions on its own schedule
  - No synchronized lockstep required
  - Parallel operation maintained

## Touch-First iPad UX
- [ ] **All buttons meet minimum touch target size**
  - Dock buttons: 44px+ min-height/width
  - Ready buttons: 60px+ height, 200px+ width
  - Action complete: 60px+ height, 150px+ width
  - First click button: 70px+ height, 200px+ width
  - Load/shuffle buttons: 60px+ height
  - Quadrant controls: 44px+ min-height/width
  
- [ ] **Touch feedback on all interactive elements**
  - Grid choice items: scale down on touch (0.97x)
  - Action choice items: scale down on touch (0.97x)
  - Buttons: visual feedback on press
  - No hover-only interactions
  
- [ ] **Controls are reachable on iPad**
  - Quadrant controls in corners (easily tappable)
  - Main buttons in dock at top
  - Ready gate buttons centered and large
  - No elements require precise cursor positioning
  
- [ ] **No hover dependencies**
  - All :hover styles have :active alternatives
  - Touch interactions work without hover
  - Visual feedback immediate on touch
  
- [ ] **Both players can operate in parallel**
  - No single busy state blocking other player
  - Each quadrant maintains independent state
  - Simultaneous button presses work correctly
  - No race conditions or conflicts

## Celebratory Effects
- [ ] **Confetti appears on wins**
  - First-click challenge winner gets confetti
  - Random confetti (50% chance) on task completions
  - Confetti uses multiple colors
  - Animation lasts ~3 seconds then removes
  
- [ ] **Flash effect on successes**
  - Green flash animation on completions
  - Quick .5s duration
  - Subtle inset shadow effect
  - Doesn't obstruct gameplay
  
- [ ] **Effects don't clutter UI**
  - Confetti stays within quadrant boundaries
  - Effects are brief and non-intrusive
  - No performance impact from effects
  - Video playback continues smoothly

## Gameplay Reliability
- [ ] **No deadlocks or bottlenecks**
  - Both players can progress independently
  - Ready gate doesn't block indefinitely
  - Video selection proceeds normally
  - Challenge overlays don't freeze game
  
- [ ] **Video loading is robust**
  - 3-second timeout on video metadata loading
  - Fallback seek positions if primary fails
  - Explicit play() calls after seek
  - No stuck loading states
  
- [ ] **State management is clean**
  - Each quadrant has isolated state
  - No shared mutable state causing conflicts
  - Timers and intervals properly cleaned up
  - Memory leaks prevented

## Browser/Device Compatibility
- [ ] **iPad Safari (primary target)**
  - Ready gate displays correctly
  - Touch targets all work
  - Video playback smooth
  - Confetti animates properly
  
- [ ] **Desktop Chrome/Firefox**
  - All features functional
  - Mouse clicks work as expected
  - Overlays display correctly
  
- [ ] **Mobile devices**
  - Touch interactions responsive
  - Video performance acceptable
  - Layout adapts to screen size

## Performance
- [ ] **60fps during gameplay**
  - Confetti doesn't cause frame drops
  - Video transitions smooth
  - Overlay animations fluid
  
- [ ] **No memory leaks**
  - Confetti elements removed after animation
  - Event listeners cleaned up
  - Intervals/timeouts cleared
  
- [ ] **Reasonable resource usage**
  - CPU usage stable during play
  - Multiple videos play without issues
  - No browser warnings/errors

## Edge Cases
- [ ] **One player not ready**
  - Start game button stays hidden
  - Both players can toggle ready state
  - No forced start
  
- [ ] **Player unselects "ready"**
  - Start button disappears
  - Player can toggle back to ready
  - Other player's state unaffected
  
- [ ] **No videos loaded**
  - Appropriate error message
  - Game doesn't crash
  - Clear instruction to load videos
  
- [ ] **Insufficient videos (<4)**
  - Error message displayed
  - Game doesn't start
  - Instructions clear
  
- [ ] **Mid-game stop**
  - Stop button works correctly
  - All overlays cleared
  - Clean state reset
  - Ready to restart

## Accessibility
- [ ] **Text contrast sufficient**
  - Text shadows provide readability
  - Colors distinguishable
  - Phase colors clearly different
  
- [ ] **Touch targets sized appropriately**
  - Minimum 44x44px per iOS guidelines
  - Comfortable spacing between elements
  - Easy to tap without mistakes
  
- [ ] **Visual feedback clear**
  - Ready state clearly indicated
  - Active elements highlighted
  - Progress visible (tally, timer)

## Final Smoke Test
- [ ] Load 4+ videos
- [ ] Click Start
- [ ] Both players click READY
- [ ] Click START GAME
- [ ] Both players select theme and video
- [ ] Game plays with both quadrants active
- [ ] Complete a PUFF phase (observe flash/confetti)
- [ ] Complete an ACTION phase
- [ ] Verify TRANSITION has no label overlay
- [ ] Verify videos continue playing smoothly
- [ ] Complete a FIRST CLICK challenge (observe confetti on winner)
- [ ] Verify both players can act simultaneously
- [ ] Click Stop and verify clean shutdown
- [ ] Restart and verify no issues

---

## Summary
This checklist covers all requirements from the problem statement:
1. ✅ Two-player readiness gate (no 30s timer)
2. ✅ Minimal, non-overlapping overlays
3. ✅ Seamless video transitions (no labels/downtime)
4. ✅ Touch-first iPad UX
5. ✅ Light celebratory effects
6. ✅ Comprehensive validation coverage
