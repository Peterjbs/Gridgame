# PR F: Minigame Updates — Major Video Redesigns

## Summary
This PR implements comprehensive updates to three video-based minigames in `index.html`, adding a central ObjectURL management system and redesigning game mechanics for better user experience and memory management.

## Changes Made

### 1. Central ObjectURL Manager (Lines 2357-2374)
**New Infrastructure:**
- Created `objectURLManager` object with methods:
  - `create(file)`: Creates and tracks object URLs
  - `revoke(url)`: Safely revokes a specific URL
  - `revokeAll()`: Revokes all tracked URLs
- Integrated with `closeTaskModal()` (line 3708) to automatically cleanup on exit
- Prevents memory leaks from unreleased blob URLs

### 2. Reflex Test Updates (Lines 4390-4540)
**3-Round Mode Implementation:**
- Changed from single-round to 3-round gameplay
- Tracks reaction time for each round (milliseconds)
- Displays average reaction time at completion
- Shows individual times: Round 1, Round 2, Round 3, and Average

**UI Improvements:**
- Increased target size from 8rem to 12rem (CSS line 1329)
- Repositioned target from 50% to 40% to avoid UI overlap
- Enhanced visibility with improved shadow effects
- Removed all `alert()` calls, replaced with in-modal messages

**Cleanup:**
- Uses `objectURLManager.create()` for video URLs
- Automatic cleanup via `closeTaskModal()`

### 3. Video Clip Detective Updates (Lines 5091-5280)
**Loading State:**
- Added "Preparing clips..." message during thumbnail generation
- Shows progress before playback begins

**Thumbnail Selection:**
- Replaced text buttons ("Clip 1", "Clip 2", etc.) with visual thumbnails
- 6 thumbnails displayed in 3x2 grid
- Each thumbnail shows a frame from the respective clip
- Hover effects: green border and scale-up animation

**Playback Control:**
- Ensures only one clip plays at a time
- Pauses player before changing source
- Proper sequence: pause → change src → play

**Cleanup:**
- Uses `objectURLManager.create()` for all video URLs
- Automatic cleanup on modal close

### 4. Video Quarter Puzzle Complete Redesign (Lines 6256-6480)
**Changed from 8 to 6 clips:**
- Reduced video pool requirement from 8 to 6
- Updated error message: "You need at least 6 videos"

**True Corner View Implementation:**
- Each corner now shows the actual corner segment of the video
- CSS properties:
  - `width: 200%; height: 200%` (zoomed)
  - `object-position`: specific to each corner
  - `transform: scale(1.5)` for proper cropping
- Corner positions:
  - Top-Left: `object-position: 0% 0%`
  - Top-Right: `object-position: 100% 0%`
  - Bottom-Left: `object-position: 0% 100%`
  - Bottom-Right: `object-position: 100% 100%`

**Sequence Rules (Lines 6285-6302):**
- 1 correct video appears once in each of the 4 corners
- 5 decoy videos appear in only 2-3 corners each
- Algorithm ensures no decoy appears in all 4 corners
- Uses `decoyUsage` Map to track distribution

**Lock/Unlock Toggle (Lines 6463-6474):**
- Click corner to toggle between LOCKED and UNLOCKED
- Green border and "✓" when locked
- White border when unlocked
- Can unlock after locking (unlimited toggles)

**Proper Validation (Lines 6481-6498):**
- Win condition: All 4 corners locked on the SAME video
- Checks `currentVideoIndex` for each corner
- Success: "🎉 Perfect! You found the correct video in all corners!"
- Failure: "❌ Not Quite! Not all corners were showing the same video."

**Memory Leak Fix (Lines 6415-6430):**
- Revokes old URL before creating new one
- Uses `objectURLManager.revoke(oldUrl)` before assigning new source
- Clears video.src before revoking
- Prevents accumulation of blob URLs during cycling

### 5. Updated closeTaskModal (Lines 3698-3719)
**Enhanced Cleanup:**
```javascript
// Pause and cleanup all videos in modal
taskModalBody.querySelectorAll('video').forEach(video => {
  video.pause();
  video.src = '';
});
// Revoke all object URLs
objectURLManager.revokeAll();
```
- Finds all video elements in modal
- Pauses each video
- Clears src attribute
- Revokes all tracked blob URLs
- Prevents memory leaks across all minigames

## Technical Details

### ObjectURL Lifecycle
1. **Creation**: `objectURLManager.create(file)` → adds to Set
2. **Usage**: Assign to video.src or img.src
3. **Cleanup**: Automatic via `closeTaskModal()` or manual via `revoke()`
4. **Verification**: No blob: URLs remain after modal close

### Browser Compatibility
- Uses modern JavaScript (ES6+ features)
- Object.fit and object-position for video cropping
- Compatible with Chrome, Firefox, Safari
- No external dependencies added

### Memory Management
- Before: Blob URLs created but never revoked → memory leak
- After: All blob URLs tracked and revoked → no leaks
- Applies to all video-based minigames

## Testing Notes

### Manual Testing Required
1. **Reflex Test**: Verify 3-round mode, reaction times, no alerts
2. **Video Clip Detective**: Check loading state, thumbnails, hover effects
3. **Video Quarter Puzzle**: Verify corner cropping, lock/unlock, validation
4. **Memory Leaks**: Use Chrome DevTools Memory tab to verify

### No Automated Tests
- Repository has no test infrastructure
- All testing must be done manually in browser
- Requires actual video files to test

## Files Modified
- `index.html` (only file changed)
- 418 lines modified (308 insertions, 110 deletions)

## Dependencies
- No new dependencies added
- Uses existing libraries: Tailwind CSS, Twemoji, Tone.js
- Pure vanilla JavaScript

## Breaking Changes
- None (all changes are enhancements)
- Existing saved game states remain compatible
- No API changes

## Future Improvements
- Consider extracting objectURLManager to separate module
- Add visual feedback for memory usage
- Implement difficulty levels for minigames
- Add sound effects for better UX

## Related PRs
- Assumes PR B exists for central cleanup patterns
- Builds on existing minigame infrastructure
- Part of ongoing video-based game improvements
