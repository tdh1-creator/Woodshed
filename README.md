# Woodshed — music practice PWA (prototype)

A practice workspace that installs like an app on iPad and Windows. Each project holds YouTube videos (with bookmarks, A–B loop and remembered speed), tab or sheet music (PDF, image or link), date-stamped practice notes with search, a practice timer, and recorded audio/video takes.

## Files
- `index.html` — the whole app (HTML, CSS, JS in one file)
- `manifest.webmanifest` — app name, icons, standalone display
- `sw.js` — service worker so the app opens offline
- `icons/` — app icons

## Put it online (needed for YouTube, camera/mic and install)
The app must be served over **https** (or `http://localhost` for testing). Opening `index.html` directly from disk will not play YouTube or record.

**Easiest: Netlify Drop**
1. Go to app.netlify.com/drop and drag the `woodshed` folder onto the page.
2. You get an https address like `https://something.netlify.app`. Rename it in site settings if you like.

**Or GitHub Pages**
1. Create a repository, upload these files to it.
2. Settings → Pages → Deploy from branch → `main` / root.

**Test locally on a PC:** in this folder run `python -m http.server 8000`, then open `http://localhost:8000`.

## Install it
- **Windows (Chrome or Edge):** open the address, then click the install icon at the right end of the address bar.
- **iPad (Chrome, iPadOS 16.4+):** open the address, tap the Share button, then **Add to Home Screen**. (Safari works the same way.) Launch it from the home-screen icon from then on.

## Where your data lives
Everything is stored in the browser on that device (IndexedDB). Projects don't sync between your iPad and PC. Use **Back up** on the home screen now and then; **Restore** loads a backup on any device.

On iPad, launch from the home-screen icon: Apple can clear storage for websites you haven't visited in a while, but home-screen apps are exempt.

## Notes on the prototype
- Tab sites like Ultimate Guitar and Songsterr usually block being shown inside another app, so links open in a new tab. Saving the page as a PDF and uploading it gives the best side-by-side experience.
- PDFs render with PDF.js, loaded the first time you open a PDF and cached for offline use.
- Playback speed is saved per video, and your last-used speed becomes the default for new videos.
- Typing `[1:23]` in a note (or tapping **Insert video time**) makes a tag that jumps the video to that moment.
- Tap the timer to pause it. Practice time is added to the project's total.
- The side panel (video, notes, bookmarks, takes) can be hidden with the panel button at the top right so the sheet music fills the screen. The video keeps playing while it's hidden.
- **Metronome:** the metronome button in the top bar opens tempo (30–260 BPM), tap tempo, beats per bar and volume. It runs on its own, and the tempo is saved per project. Press **M** on a keyboard to start or stop it. In the recorder, tick "Metronome during take" and/or "Count in one bar". Use headphones if you don't want the click on the recording. On iPad, the ring/silent switch can mute it.
