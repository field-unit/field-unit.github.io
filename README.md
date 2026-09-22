# Field Unit — music site

The Field Unit site with the games taken out (18 Sep 2026): twelve demo tracks with their artwork to play, the radio, the 12BIT / 8BIT bit-crusher effects, ink drawing and the dancer.

Made from `field-unit.github.io-main.zip`. The untouched original is in `../source-assets-private/field-unit-original/`. `index.html` and this README changed; the MP3s and artwork are as downloaded.

## What changed

- **Games removed.** Their five launchers, the full-screen game frame, and the code that opened games or exchanged messages with them are gone. The games themselves live in their own repositories and are untouched.
- **No tickets.** The completion tickets and the ticket panel are gone. Old tickets saved in a browser are simply ignored.
- **No downloads** (James, 18 Sep 2026). The track-download page (`field-unit-downloads.html`) has been removed and nothing links to it. The tracks can be played on the site but aren't offered for download.
  - Any audio a website plays can still be saved by someone determined, since the browser has to fetch the file.
- **Radio, synced with the tiles.**
  - The radio no longer has its own player: it plays the tiles in turn. Whatever is playing shows on its tile (‖, moving progress and time) and on the radio panel at once.
  - **Tiles move the radio:** pressing play on any tile makes that the radio's current track, and pausing either the tile or the panel pauses both.
  - **Radio controls:**
    - RADIO or PLAY carries on into the next track when one ends;
    - SKIP moves to the next tile;
    - STOP pauses and ends the run.
  - All 11 tracks are included, played from the files in this folder rather than the live site.
  - Music only starts when someone presses a play button, RADIO or DANCE. DANCE won't restart the music after STOP, or start a second track over one that's playing.
  - Only one track plays at a time, and the bit-reduction effects apply to whatever is playing.
- **Keyboard and screen readers.** The play, radio and image buttons show a focus outline. Each play button is named after its track, and says "pause" while the track plays.
- **12BIT and 8BIT you can hear** (19 Sep 2026). James found they made no audible difference, and they barely did: a true 12-bit, 24 kHz reduction is all but inaudible on mastered music, and 8-bit, 12 kHz only slightly more.
  - They are now a proper bit crusher. 12BIT is a gritty sampler: 6-bit, 12 kHz. 8BIT is a lo-fi games console: 4-bit, 6 kHz.
  - The levels are spaced µ-law fashion, fine near silence, so quiet passages go grainy instead of cutting out.
  - The names stay as the style, not the literal bit depths; the settings are one line (`FXP`) if they want tuning.
  - The effect runs in an audio worklet, off the page's own thread, so it doesn't stutter while the visuals animate. Browsers without worklets fall back to the older script processor.
  - The audio engine is woken whenever a track starts, so the sound doesn't go missing after a phone has paused it.
- **Room for the radio.** While the radio panel shows, the page gets extra space at the bottom, so the last tiles can scroll clear of it.
- **Buttons lined up with the tiles** (19 Sep 2026).
  - On a computer the six-track row puts each pair over one column of tiles: 12BIT 8BIT | CLEAR INK | DANCE RADIO.
  - Touch screens add DRAW and get two rows of three.
- **Works when opened from disk** (19 Sep 2026).
  - Browsers won't let a page read the pixels of images opened from disk, so the artwork used to show plain there, without its green grain.
  - `art-thumbs.js` now carries a small copy of each of the 11 artworks (384 × 144 px, 226 KB together), which the grain uses instead.
  - Online the page uses the same copies. A new track added without one still gets the grain online, but shows plain when opened from disk.
  - From disk, 12BIT and 8BIT change the look, and a line under the buttons says the sound only changes when the site is served (see below). Online that line never shows.

- **Wilt** (21 Sep 2026). A twelfth track, at the end of the list, dated June 25.
  - From `Tilted stuff Demo.wav` (3:54, 24-bit, 48 kHz) as `Wilt_Demo.mp3`: 320 kbps at 48 kHz, joint stereo,
    which is what the other eleven are. Nothing was done to the sound.
  - `Wilt_Artwork.jpg` is the sunset photograph, as supplied.

- **The dancer is a robot, and it is made of grain** (22 Sep 2026). It was an SVG silhouette driven by CSS
  keyframes; it is now drawn into a small canvas through the same Bayer dither as the tiles, then blown up
  with whole pixels.
  - Ten joints, and a pose is ten whole angles, all multiples of 15 degrees. The clock steps from one pose to
    the next and nothing moves in between — there is no easing anywhere — which is what makes it read as a
    machine rather than a person.
  - Head, body, shoulders, hands and feet are boxes; the limbs are thin rods that stop short of each other, so
    the joints stay as gaps.
  - **12BIT and 8BIT take its pixels away too**, exactly as they do a tile: bigger blocks and fewer greens. At
    8BIT the robot is about eighteen blocks wide.
  - It never goes solid. The tone is held around the middle of the green ramp, where the dither speckles most,
    so the figure is a cloud of dots that reads as one shape.

## Adding a track

1. Put the MP3 and its artwork in this folder.
2. Add a line to `POSTS` near the top of `index.html`'s script — newest first, oldest last:
   `{ date:"June 25", title:"Wilt", audio:"Wilt_Demo.mp3", art:"Wilt_Artwork.jpg" },`
3. Run `python tools/make_art_thumbs.py`. It adds a small copy of the new artwork to `art-thumbs.js`, which is
   what the grain reads; without one the tile shows the artwork plain when the page is opened from disk. It
   leaves the existing ones alone.
4. Upload `index.html`, `art-thumbs.js` and the two new files (see below).

A WAV can be converted here without any extra software:

```python
import soundfile as sf
d, sr = sf.read("Track.wav", dtype="float32", always_2d=True)
sf.write("Track.mp3", d, sr, format="MP3", subtype="MPEG_LAYER_III",
         bitrate_mode="CONSTANT", compression_level=0.0)      # 320 kbps
```

## Preview locally

**Double-click `Open music site locally.bat`** (needs Python). It serves this folder at http://127.0.0.1:8160/ and opens it, with everything working as it will online, including the 12BIT / 8BIT sound. Close the minimised "Field Unit server" window to stop it.

Or from a terminal in this folder:

```bash
python -m http.server 8160 --bind 127.0.0.1
```

- **Opening `index.html` directly** shows everything except the bit-reduced sound. Browsers mute any sound a page sends through an effect when the page comes from disk, so there 12BIT and 8BIT change the visuals only and the music plays unaltered.
- Offline, the pixel font (Press Start 2P, from Google Fonts) falls back to the system monospace.

## Going online

Step by step, with the portfolio as well: **`../LAUNCH.md`**. In short:

The site has a domain of its own since 22 Sep 2026: **field-unit.co.uk**. `CNAME` in this folder is the file that tells GitHub Pages so, and it goes up with the rest; `field-unit.github.io` then redirects to it. The portfolio's Field Unit object opens the new address.

This folder is laid out as the `field-unit.github.io` repository: its contents replace what's there now, so delete `field-unit-downloads.html` from the repository when you upload. Nothing has been uploaded.

**Upload it in the browser (about five minutes, no software needed):**
1. Sign in at github.com and open the repository behind the site (`github.com/field-unit/field-unit.github.io`, if `field-unit` is the account name).
2. Open `field-unit-downloads.html` → the `…` menu → **Delete file** → **Commit changes**.
3. Back on the repository's front page: **Add file → Upload files**, drag in `index.html`, `art-thumbs.js`, `README.md`, `Wilt_Demo.mp3`, `Wilt_Artwork.jpg` and `CNAME` from this folder, then **Commit changes**. The other eleven MP3s and their artwork are already there and haven't changed. `Open music site locally.bat`, the `tools` folder and `.gitignore` are only for this PC; leave them out.
4. After a minute or two, open https://field-unit.github.io/ and press Ctrl+F5.

This copy was made from the repository as it stood on 29 Jul 2026. If anything has changed there since (new tracks, for example), say so before uploading, so the changes can be merged instead of overwritten.

**Until then, the live site still has the games** (the five launchers, the ticket console and the downloads), and so does the Field Unit link on the portfolio website, which opens the live site. The offline portfolio file opens this local copy instead, from disk. This folder is the game-free version; preview it locally as above to see it. The games' own repositories (fishexe, trainexe, ringroadexe, signalstepexe, pigeonexe) can stay or be archived; nothing here links to them.
