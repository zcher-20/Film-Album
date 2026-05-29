
# Film Album

An interactive, scroll-driven photo gallery built with vanilla JavaScript — no frameworks, no build step, no dependencies. A single self-contained HTML file featuring a continuous depth-based carousel, real-time caption editing, and full client-side persistence.

<img width="544" height="470" alt="Screenshot 2026-05-29 at 1 39 49 PM" src="https://github.com/user-attachments/assets/8bcd35b0-5e36-4f62-ad29-ba8d52be1798" />


## Highlights

- **Continuous scroll-linked animation** — Rather than snapping between discrete slides, photo position, scale, opacity, and blur are interpolated in real time from a fractional scroll value. A `requestAnimationFrame` render loop with lerp-based smoothing produces fluid 60fps motion that feels hand-controlled across both trackpad and mouse-wheel input.
- **Depth model via interpolation** — A tiered keyframe system (`large → medium → small → fade`) with eased interpolation gives photos a sense of receding into the distance, recalculated every frame from each photo's signed distance to the viewport center.
- **Client-side persistence (IndexedDB)** — All photos and edits are stored in IndexedDB with a seed-once strategy: originals are written on first load, then the database becomes the single source of truth so additions persist and deletions stay deleted across sessions.
- **In-browser content management** — Add photos via the File API (read as base64 data URLs), delete the centered photo, and reset to defaults — each mutating state and triggering a clean rebuild of the DOM, navigation, and scroll height.
- **Editable captions** — `contenteditable` fields write directly back to the corresponding IndexedDB record on blur, keeping a single source of truth for all content.

## Technical Stack

- **Vanilla JavaScript** (ES6+) — no frameworks or libraries
- **IndexedDB** for persistent client-side storage
- **File API / FileReader** for in-browser image uploads
- **CSS transforms & filters** driven imperatively for performance
- **Sticky-positioning scroll architecture** mapping page scroll to gallery state

## Engineering Notes

The interface maps a tall scroll container to a sticky viewport, translating scroll offset into a continuous `progress` value that drives the entire visual state. Keeping the animation in a single rAF loop (rather than CSS transitions) allows every visual property to track scroll velocity smoothly and avoids the jank of competing transitions. The entire app ships as one portable HTML file with zero external requests.

## Usage

Open `index.html` in any modern browser, or visit the live demo above. Scroll to move through the gallery; use the arrow buttons, dots, or arrow keys to jump between photos.
EOF
