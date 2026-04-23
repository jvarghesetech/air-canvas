How to Use
1. Open the file
Open air-canvas.html in Google Chrome (recommended) or any modern Chromium-based browser. Firefox works but performance may vary.
2. Allow camera access
Click Allow Camera & Start Drawing and grant camera permission when the browser asks. Your camera feed never leaves your device — everything runs locally in the browser.
3. Draw
GestureAction☝️ Point index fingerDraw with current color✊ Make a fistErase while held (64px eraser)🖐 Move hand to top of screenOpen color paletteHover over a color for ~0.7sSelect that color
4. Clear the canvas
Click the 🗑 Clear button in the bottom-right corner to wipe everything.

Color Palette
Move your hand to the top strip of the screen to reveal the palette. Hover your index finger over any swatch and hold for ~0.7 seconds — a progress ring fills up, then the color locks in. Moving your hand back down returns you to drawing mode.
ColorSwatchEraser⬜ (white with ✕)Red🔴Orange🟠Yellow🟡Green🟢Cyan🔵Blue🔵Purple🟣Pink🩷White⬜

Tips for Best Results

Lighting matters most. Make sure your hand is well-lit and clearly visible against the background. Avoid dark rooms or cluttered backgrounds.
Keep your hand 1–2 feet from the camera. Too close or too far reduces tracking accuracy.
Move deliberately. The position is smoothed to produce fluid lines — very fast flicks may not register fully.
Use a solid background behind your hand (a plain wall) for the most reliable tracking.
Fist fully. Curl all four fingers down to trigger eraser mode reliably.


How It Works
Webcam feed
    │
    ▼
MediaPipe Hands (WASM, runs in browser)
    │  — 21 hand landmarks per frame
    ▼
Gesture detection
    ├── Fist? → eraser mode
    ├── Hand in top zone? → palette UI, dwell to select color
    └── Otherwise → draw with index fingertip (lm[8])
    │
    ▼
Canvas 1 (persistent drawing layer)
Canvas 2 (ephemeral overlay: cursor + palette)
    │
    ▼
Rendered over mirrored live video
Finger detection uses a distance-from-wrist algorithm rather than raw Y comparisons, making it rotation-invariant. Fist detection requires ≥3 of 4 main fingers to be curled, smoothed over 8 frames to prevent flickering.
Color selection uses a dwell-time system (700ms hover) so colors never change accidentally while drawing.

Tech Stack
LibraryVersionPurposeMediaPipe Hands0.4.1646424915Hand landmark detectionMediaPipe Camera Utils0.3.1640029074Webcam frame pumpingHTML5 Canvas API—Drawing & overlay rendering
No build step. No npm. No server. Just one .html file.

Browser Requirements

Chrome 88+ / Edge 88+ / Brave (recommended)
Firefox 90+ (functional, slightly slower)
Safari is not supported (MediaPipe WASM issues)
Camera permission required
Works on desktop and laptop — not optimized for mobile


Privacy
All processing happens entirely in your browser. No video, images, or hand data are ever sent to any server. The only network requests are to load the MediaPipe model files from cdn.jsdelivr.net on first load (cached after that).

License
MIT — do whatever you want with it.
