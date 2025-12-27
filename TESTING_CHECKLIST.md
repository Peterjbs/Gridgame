# Manual Testing Checklist for iPad UX Fixes

## Testing Environment Setup

### Required Devices
- [ ] iPad (any model with Safari 13+)
- [ ] macOS device with Safari
- [ ] Desktop with Chrome/Edge/Firefox

### Test Files
- [ ] Open `index.html` in browser
- [ ] Open `newq.html` in browser
- [ ] Have some video files ready for upload

---

## Test Suite 1: Keyboard Behavior

### Test 1.1: Backspace Editing (index.html)
**Steps**:
1. Open index.html
2. Click on Gemini API key input (top-right)
3. Type some text: "test12345"
4. Press Backspace 5 times
5. Verify text becomes "test"

**Expected**: ✅ Backspace deletes characters normally
**Actual**: ___________

### Test 1.2: Cmd+Backspace Closes Modal (index.html)
**Steps**:
1. Click any challenge tile
2. Modal opens with challenge options
3. Press Cmd+Backspace (or Ctrl+Backspace on Windows)
4. Verify modal closes

**Expected**: ✅ Modal closes, no character deletion
**Actual**: ___________

### Test 1.3: Escape Key Still Works (index.html)
**Steps**:
1. Click any challenge tile
2. Press Escape key
3. Verify modal closes

**Expected**: ✅ Modal closes
**Actual**: ___________

---

## Test Suite 2: Challenge Distribution

### Test 2.1: Visual Even Distribution (index.html)
**Steps**:
1. Refresh page multiple times
2. Observe challenge tile distribution
3. Look for adjacent duplicates or clumps

**Expected**: ✅ Challenges spread evenly, minimal clumping
**Actual**: ___________

### Test 2.2: Distribution in newq.html
**Steps**:
1. Open newq.html
2. Refresh page multiple times
3. Observe 21-tile distribution

**Expected**: ✅ Even distribution across 21 tiles
**Actual**: ___________

---

## Test Suite 3: Image Usage

### Test 3.1: Grid Images Varied (index.html)
**Steps**:
1. Refresh page 5 times
2. Note down tile images shown
3. Count unique images seen across refreshes

**Expected**: ✅ High variety, different images each refresh
**Actual**: ___________

### Test 3.2: Avatar Sequence Images (index.html)
**Steps**:
1. Upload video files
2. Play until Avatar Sequence challenge appears
3. Note the 9 tile images shown
4. Fail/complete challenge and try again
5. Note images in second attempt

**Expected**: ✅ Different images shown between attempts
**Actual**: ___________

---

## Test Suite 4: 3-Choice System

### Test 4.1: Identify 3-Choice Tiles (index.html)
**Steps**:
1. Click tiles at indices 3, 7, 11, 15, 19, 23 (count from 0, left-to-right, top-to-bottom)
2. Verify "Choose Your Challenge!" appears
3. Count options shown

**Expected**: ✅ 3 distinct challenge options shown
**Actual**: ___________

### Test 4.2: Selection Works (index.html)
**Steps**:
1. Click tile at index 3
2. Click one of the 3 options
3. Verify selected challenge starts

**Expected**: ✅ Chosen challenge launches
**Actual**: ___________

---

## Test Suite 5: iPad Touch Interactions

### Test 5.1: Touch Target Sizes (iPad Safari)
**Steps**:
1. Open index.html on iPad
2. Try tapping challenge tiles
3. Try tapping modal buttons
4. Try tapping task option buttons

**Expected**: ✅ All buttons easy to tap, no missed taps
**Actual**: ___________

### Test 5.2: No Double-Tap Zoom (iPad Safari)
**Steps**:
1. Open index.html on iPad
2. Double-tap various areas
3. Try to zoom with double-tap

**Expected**: ✅ No zoom occurs, touch-action works
**Actual**: ___________

### Test 5.3: Modal Buttons on iPad (iPad Safari)
**Steps**:
1. Open any challenge modal
2. Tap "Start" or option buttons
3. Verify responsive feedback

**Expected**: ✅ Buttons respond immediately to touch
**Actual**: ___________

---

## Test Suite 6: Overlays Don't Block

### Test 6.1: Pressure Front Overlay (index.html)
**Steps**:
1. Upload videos
2. Play Pressure Front challenge
3. Verify you can see video playing
4. Verify you can click tally buttons
5. Verify you can click emoji counts

**Expected**: ✅ Video visible, tally buttons clickable
**Actual**: ___________

### Test 6.2: Paint Splatter Canvas (index.html)
**Steps**:
1. Upload videos
2. Play Paint Splatter challenge
3. Click/touch anywhere on screen to paint
4. Verify coverage counter updates

**Expected**: ✅ Canvas responds to clicks/touches everywhere
**Actual**: ___________

### Test 6.3: Icon Click Hunt (index.html)
**Steps**:
1. Upload videos
2. Play Icon Click Hunt challenge
3. Click floating icons
4. Verify score increases

**Expected**: ✅ Icons clickable, score updates
**Actual**: ___________

---

## Test Suite 7: Creative Challenge

### Test 7.1: Winner Selection (index.html)
**Steps**:
1. Upload videos
2. Play Creative Challenge
3. Click "P1 Wins" button
4. Verify next turn goes to P1

**Expected**: ✅ Winner gets next turn
**Actual**: ___________

### Test 7.2: Random Challenge Text (index.html)
**Steps**:
1. Add custom challenges in settings
2. Play Creative Challenge multiple times
3. Verify different challenges shown

**Expected**: ✅ Random selection from pool
**Actual**: ___________

---

## Test Suite 8: Removed Features

### Test 8.1: No DAB Tiles (index.html)
**Steps**:
1. Refresh page multiple times
2. Look for any tile with "DAB" text
3. Check tile styling

**Expected**: ✅ No DAB tiles visible anywhere
**Actual**: ___________

### Test 8.2: No Quick Challenge (index.html)
**Steps**:
1. Play through multiple challenges
2. Look for "Quick Challenge! ⚡" title
3. Check for emoji-style simple challenges

**Expected**: ✅ No quick challenges appear
**Actual**: ___________

---

## Test Suite 9: File Integrity

### Test 9.1: index.html Loads (All Browsers)
**Steps**:
1. Open index.html in Chrome
2. Open index.html in Firefox
3. Open index.html in Safari
4. Check console for errors

**Expected**: ✅ No console errors in any browser
**Actual**: ___________

### Test 9.2: newq.html Loads (All Browsers)
**Steps**:
1. Open newq.html in Chrome
2. Open newq.html in Firefox
3. Open newq.html in Safari
4. Check console for errors

**Expected**: ✅ No console errors in any browser
**Actual**: ___________

---

## Test Suite 10: Regression Testing

### Test 10.1: Video Upload Still Works
**Steps**:
1. Click "Choose video folder"
2. Select folder with videos
3. Verify videos load
4. Verify video playback works

**Expected**: ✅ Videos load and play normally
**Actual**: ___________

### Test 10.2: 2-Player Mode Works
**Steps**:
1. Verify P1 and P2 cards display
2. Complete a challenge
3. Verify turn switches
4. Verify scores update

**Expected**: ✅ 2-player mechanics work normally
**Actual**: ___________

### Test 10.3: Score Decay Works
**Steps**:
1. Complete a challenge
2. Wait 10 seconds without activity
3. Observe score changes

**Expected**: ✅ Score decays over time as before
**Actual**: ___________

### Test 10.4: All Minigames Load
**Steps**:
1. Play through at least 10 different challenge types
2. Verify each opens correctly
3. Verify each is completable

**Expected**: ✅ All challenges work as before
**Actual**: ___________

---

## Test Suite 11: Cross-Browser Compatibility

### Test 11.1: Chrome Desktop
- [ ] Keyboard shortcuts work (Ctrl+Backspace)
- [ ] All challenges load
- [ ] No console errors
- [ ] Visual styling correct

### Test 11.2: Firefox Desktop
- [ ] Keyboard shortcuts work (Ctrl+Backspace)
- [ ] All challenges load
- [ ] No console errors
- [ ] Visual styling correct

### Test 11.3: Safari Desktop
- [ ] Keyboard shortcuts work (Cmd+Backspace)
- [ ] All challenges load
- [ ] No console errors
- [ ] Visual styling correct

### Test 11.4: iPad Safari
- [ ] Touch interactions smooth
- [ ] No zoom issues
- [ ] All challenges load
- [ ] Overlays don't block gameplay
- [ ] Button sizes adequate

---

## Summary

### Total Tests: 50+
### Tests Passed: _____ / 50+
### Tests Failed: _____ / 50+
### Critical Issues: _____
### Minor Issues: _____

### Overall Assessment
- [ ] ✅ Ready for production
- [ ] ⚠️ Minor issues to address
- [ ] ❌ Critical issues found

---

## Notes

Add any additional observations or issues here:

___________________________________________
___________________________________________
___________________________________________
___________________________________________
___________________________________________

---

## Tester Information

**Name**: _____________________
**Date**: _____________________
**Browser Versions Tested**: _____________________
**iPad Model**: _____________________
**iOS Version**: _____________________

---

## Sign-Off

I have completed the testing checklist and verified the implementation meets all requirements.

**Signature**: _____________________
**Date**: _____________________
