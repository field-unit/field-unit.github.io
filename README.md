# Field Unit — music site

Live at **https://field-unit.co.uk/** (GitHub Pages, repository `field-unit/field-unit.github.io`; the `CNAME`
file in this folder is what gives it the domain). Twelve demo tracks with their artwork, the radio, the CHIP FX
switch, floating ink drawings and a dancing robot. No games, no tickets, no downloads.

## The controls

One row of pixel symbols under the logo. Each is a real button with its name for screen readers, a tooltip on
hover or keyboard focus, and a lit corner and filled face when it is on (not colour alone). The line underneath
says what just changed, and **?** opens a key with every name, for touch screens, where there is no hover.

| Symbol | Name | What it does |
|---|---|---|
| a chip round a square wave | Chip effect | Sound and picture together (below) |
| a pencil and a trail | Draw | Touch screens only: turns drawing on, so a swipe draws a mark instead of scrolling; off again after each mark |
| an eraser over a line | Clear drawings | Removes the floating drawings, and nothing else |
| a dancing figure | Dancer | The robot dances on the page, and starts the radio if nothing is playing |
| a radio | Radio | Plays the tracks one after another |
| an envelope | Contact | A small panel for getting in touch (below) |

On a computer, drawing is with the mouse anywhere on the page, as before.

## Contact (23 Sep 2026)

The envelope opens a small panel under the controls; Esc or × closes it and focus goes back to the envelope. It
never touches the music, and drawing is off inside it.

- **Now:** there is no form service yet, so the panel shows the site's own address,
  fieldofunits@gmail.com, as a mail link. A Send button that only pretended to send would be worse than none.
- **To turn the form on:** make a form with a hosted form service (Formspree was the brief's suggestion;
  check its current free allowance first), with fieldofunits@gmail.com as the recipient, and confirm that address
  when the service emails it. Then paste the form's endpoint into `CONTACT_ENDPOINT` near the top of the contact
  script in `index.html` (and `CONTACT_PROVIDER` if it isn't Formspree), and publish. The panel then shows the form:
  your email (required, for a reply), a message (required, up to 2000 characters), an optional name, and Send.
  - It sends JSON with the visitor's address as `email` (Formspree uses it as the reply-to), the site's name, and a
    subject naming the site, so a message says where it came from. A hidden `_gotcha` field catches form-filling
    robots, and the service's own spam filtering does the rest; no secret is in the page.
  - "Sent" shows only once the service has accepted the message. On an error, no connection or a 15-second
    timeout it says so, keeps the message, and offers the address instead; a second press while one send is
    pending does nothing.
  - Before relying on it: send one clearly labelled test and check it arrives, that Reply goes to the visitor, and
    that the subject names the site.
- A copy opened from disk never shows the form, only the address.

## CHIP FX (23 Sep 2026)

One switch in place of 12BIT and 8BIT. On, every track plays in a treated version of the same recording and the
page's grain gets coarser to match; off, the original and the normal picture come back.

- **The sound is rendered once, not approximated live.** An effects-only treatment was approved on Tuckshop:
  the original stereo mix narrowed a little, the bass kept clean below 175 Hz, the upper band saturated, held at
  9.6 kHz, quantised to about seven bits with a little dither, filtered and blended back 78/22 with the dry upper
  band, then matched to the original's loudness under a −1.4 dBFS ceiling. No new notes, instruments, pitch or
  timing — every part stays where it was.
- `tools/chip_fx.py` applies that recipe to every track in `POSTS` and writes `audio/chip-fx/<track>.mp3` at
  192 kbps, plus `audio/chip-fx/manifest.json` (and the same as `manifest.js`, which the page loads): original and
  treated file, length, sample rate, and hashes of the original and of the recipe, so a track is rendered again
  only when one of those changes. The 24-bit WAVs stay on this PC in
  `../source-assets-private/field-unit-chip-fx/`.
  - The recipe is Codex's reference script step for step. That script uses SciPy, which isn't installed here, so
    the processor does SciPy's Butterworth design and zero-phase filtering itself; `--check` renders Tuckshop
    afresh and compares it with the approved WAV: no sample differs by more than one 24-bit step.
  - Every treated file decodes to exactly the length of its original, and a browser decodes each pair onto the same
    timeline (checked by cross-correlation: at most one sample apart), so no offsets are needed.
- **Switching mid-track** keeps the music going. The other version is fetched only when it's wanted; while it
  loads the current one plays on and the switch's light blinks. When it's ready it is started at the same point
  in the song and cross-faded in over 60 ms, and the picture changes at that moment. Only the latest press counts,
  so repeated presses settle on the last one. Paused, it swaps silently and stays paused. The radio and every tile
  play in whichever version is chosen. At most three treated files are kept loaded at once.
- **If a treated file can't load**, the original keeps playing, the switch stays off and the line under the
  switches says so; pressing again tries again. If one fails while playing, the original carries on from the
  same place.
- **The picture:** the logo, the artwork on every tile, the footer strip and the dancer are drawn with 4-pixel
  blocks and three greens instead of five (the old 8BIT look), and the floating ink is drawn at one sixth size
  and blown up with square pixels in the same three greens. Drawings, the dancer, the radio and the logo's motion
  all carry on through a switch. Text, buttons and focus outlines stay sharp.
- The old bit crusher, its audio worklet and the two buttons are gone. No sound goes through Web Audio any more,
  so everything, CHIP FX included, also works with `index.html` opened straight from disk.
- Normal is the default on every visit; the choice isn't remembered, and nothing ever plays on its own.

## Earlier changes

- **18 Sep 2026:** made from `field-unit.github.io-main.zip` (the original is in
  `../source-assets-private/field-unit-original/`). Games, tickets and the download page removed; the radio
  plays the tiles in turn, in step with them; play buttons are named after their tracks.
- **19 Sep:** `art-thumbs.js` carries a small copy of each artwork, so the grain works when the page is opened
  from disk.
- **21 Sep:** Wilt, a twelfth track, from `Tilted stuff Demo.wav`, 320 kbps like the rest.
- **23 Sep:** no dates on the tracks. Each tile shows the track's name alone, and the dates have gone from
  `POSTS` too, so they aren't in the page at all. The order of the list is unchanged, newest first.
- **22 Sep:** the dancer became a robot drawn in grain: ten joints stepping between poses with no easing, boxes
  and rods with gaps at the joints. Published on field-unit.co.uk.

## Adding a track

1. Put the MP3 and its artwork in this folder.
2. Add a line to `POSTS` near the top of `index.html`'s script — newest first, oldest last:
   `{ title:"Wilt", audio:"Wilt_Demo.mp3", art:"Wilt_Artwork.jpg" },`
3. `python tools/make_art_thumbs.py` adds a small copy of the artwork to `art-thumbs.js`.
4. `python tools/chip_fx.py` renders its CHIP FX version and updates the manifest (the others are left alone).
5. Publish (below).

A WAV can be converted here without extra software:

```python
import soundfile as sf
d, sr = sf.read("Track.wav", dtype="float32", always_2d=True)
sf.write("Track.mp3", d, sr, format="MP3", subtype="MPEG_LAYER_III",
         bitrate_mode="CONSTANT", compression_level=0.0)      # 320 kbps
```

## Preview locally

Double-click **`Open music site locally.bat`**, or run `python tools/serve.py` in this folder and open
http://127.0.0.1:8160/. `tools/serve.py` answers byte ranges as GitHub Pages does, so seeking and the CHIP FX
hand-over behave as they will online; Python's own `http.server` doesn't, and seeking fails there. Offline, the
pixel font (Press Start 2P, from Google Fonts) falls back to the system monospace.

## Publishing

This folder is the `field-unit.github.io` repository: commit and `git push` from this PC, and GitHub Pages serves
it at field-unit.co.uk a minute later. `Open music site locally.bat` and `tools/` stay on this PC (`.gitignore`).
