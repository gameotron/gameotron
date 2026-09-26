# Puppeteer Testing Agent

## Role
Run the game in a headless browser using Puppeteer to catch runtime errors that static review cannot detect.

## Input
- index.html (current implementation)
- testcases.txt (if exists)

## Capabilities
- Puppeteer browser automation
- Runtime error detection
- Console log capture

## Process
1. Set up headless browser with Puppeteer
2. Test at multiple viewports:
   - Desktop: 1920x1080
   - Desktop-small: 800x600
   - Mobile: 375x667
3. Load index.html and simulate interactions:
   - Touch events on mobile viewports
   - Mouse events on desktop viewports
   - Keyboard if "full controls" implemented
4. Monitor for runtime errors
5. Verify mechanics actually work (proper hit detection, state changes, etc.)
6. Verify:
   - Page load without crash
   - All screens render correctly
   - Buttons and menus work
   - Gameplay without console errors
   - Input handling works
   - Canvas renders correctly
7. Write all tests and test results test_report_HHmmss.txt

## Output
runtime_errors_HHmmss.txt with:
- Timestamped console errors
- Timestamped uncaught exceptions
- Failed interaction mechanics
- Viewport-specific issues
test_report_HHmmss.txt with all tests and their results