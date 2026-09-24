# Field Unit — music site

Live at **https://field-unit.co.uk/** (GitHub Pages, repository `field-unit/field-unit.github.io`; the `CNAME`
file in this folder is what gives it the domain). Twelve demo tracks with their artwork, the radio, the fx dice,
a logo that talks when you spin it, and a dancing figure. Each track has a link of its own, and the player follows you
down the page. No games, no tickets, no downloads.

## The controls

The logo itself is one (below). Under it, one row of pixel symbols. Each is a real button with its name for screen
readers, a tooltip on hover or keyboard focus, and a lit corner and filled face when it is on (not colour alone).
The line underneath says what just changed, and **?** opens a key with every name, for touch screens, where there is
no hover.

| Symbol | Name | What it does |
|---|---|---|
| a die, with a narrow ▾ beside it | FX dice | Rolls one of six effects on the sound and the picture; press again for off. Hover it, or press the ▾, to choose a colour instead (below) |
| a dancing figure | Dancer | A small figure dances on the page, and starts the radio if nothing is playing |
| a radio | Radio | Plays the tracks one after another |
| an envelope | Contact | A small panel for getting in touch (below) |

## The talking ∅ (23 Sep 2026)

Scroll over the logo, or swipe sideways across it on a phone (or drag it with a mouse), and it says "field unit".
An up-and-down swipe still scrolls the page, so nobody gets stuck on it.

- **It turns like a flywheel.** Each notch of the wheel adds speed, and once you stop it runs down by itself over a
  few seconds. The faster it turns, the quicker and higher it says it — about natural speed for one notch, up to
  2.4 times as fast flat out, a word every third of a second — and the louder and brighter. As it slows the words
  slow, drop and fade, and the slash comes back round to where it belongs.
- **Each time it's set going from still, it's a new voice:** a pitch between about 80 and 160 Hz, a longer or
  shorter throat, flat or sung, and now and then a growl, a whisper, a doubled octave, a ring-modulated buzz or a
  vibrato. Spinning it harder while it's going keeps the same voice.
- **A tap** (a click, or Enter with it focused) says it once in a new voice and flips the slash over; a tap while
  it's turning stops it. The arrow keys spin it, and Esc stops it.
- A scroll that began on the page carries on scrolling the page when the logo passes under the pointer; one that
  begins on the logo keeps turning it until you pause.
- Browsers don't let a scroll start sound. Before the first tap or click on the page it turns silently and the
  line under the buttons says "tap the ∅ first".
- **The voice is made in the page, not recorded:** a buzz from a model of the vocal folds, sent through five
  resonances, three of them moving through the shapes of the two words, with noise for the f, the d and the t. The timing and
  the shapes follow a measured spoken "field unit" (the stress on field, the u fronted, the d run into the y). Each
  new voice is rendered once, in a few milliseconds, then played like tape at the speed of the spin.
- **The dice's face is on it too.** It goes into the same audio bus as the tracks: chip plays a crunched take (held
  at 9.6 kHz like the tracks' chip copies, sixteen companded steps each way), slow plays it at 0.84, and dub, swirl,
  radio and cave treat it as they treat the music. It never pulls the tracks into the audio graph by itself, and it
  works with the page opened from disk.
- With reduced motion set, it talks and brightens but doesn't turn.
- Checked with Windows' en-GB speech recogniser as a rough, independent listener: every one of 18 test voices comes
  out as "field unit" or its near-twin "sealed unit" (they differ only in the first sound, and the recogniser barely
  separates them even for a recorded voice).

## The fx dice (23 Sep 2026)

Press the die and a small 3D die, drawn in the same dithered grain as everything else, bounces along the top of the
buttons as if they were a shelf, turning a quarter at a time, and lands with one face up. Its faces are colours, not
numbers, and each is an effect on the sound and the picture together. It sits on the shelf while the effect is on,
the button lights in the face's colour, and the line underneath names it. Press again: off, back to the original
sound and picture. Press again: another roll, never the same face twice running. Presses while it rolls are ignored.

| Face | Sound | Picture |
|---|---|---|
| chip — crunched | every track swaps to its rendered chip copy (below) | 4-pixel blocks, three greens |
| dub — tape echo | repeats at 0.36 s that darken and wobble as they fade | teal, with a faint repeat trailing each shape |
| slow — down a gear | the tracks play at 0.84, and the pitch drops with them | amber, the grain crawling at under half speed |
| swirl — phased | a slow six-stage phaser | purple, 2-pixel blocks, the logo twisting |
| radio filter — far off | a narrow band, 420 Hz to 2.8 kHz, gently overdriven | red, a line slipping sideways now and then |
| cave — big room | a long, dark 3.2 s reverb behind the dry sound | blue, everything a little lighter |

- Dub, swirl, radio and cave run live in the browser's audio graph, built the first time one of them is rolled
  (inside the press, so the browser lets it sound). From then on every copy of every track goes through it: a dry
  path, plus the rolled effect faded in or out over a tenth of a second, and a safety limiter just under full scale
  for when the two add up. A page opened from disk can't send the tracks through it, so there the dice rolls only
  chip and slow.
- Nothing is remembered between visits; every visit starts with the dice off.

**Choosing a face (24 Sep 2026).** Hovering the dice (with a mouse) opens six colour swatches directly under it, one
per face, always in the order above and in the face's own colour; no words on them. Choosing one puts that effect on
at once, through the same path as a roll (the die lands with that face up, the button lights, the line underneath
names it); choosing the lit one again turns it off. Opening the swatches changes nothing, and the dice itself still
rolls. The menu stays open while the pointer travels into it and closes a third of a second after it leaves, or on a
press elsewhere, or Esc. For touch and the keyboard, the narrow ▾ joined to the dice opens it (and keeps it open
until pressed again): Tab reaches the swatches, the arrow keys step along them, Enter or Space chooses, Esc closes
and puts focus back on the ▾. Each swatch is a button named for screen readers ("chip", "dub", "slow", "swirl",
"radio filter", "cave") with its pressed state, and the lit one has a ring and a mark under it as well as its
colour. The key under **?** shows which colour is which. From disk only chip and slow work, and the others are
dimmed.

## The player and track links (24 Sep 2026)

**The player.** Once a track has been picked it stays in the bottom corner as you scroll: whether it's playing one
track (TRACK) or the radio (RADIO), the track's name (press it to go to its tile), the effect on (ORIGINAL, or the
face in its colour, blinking while chip loads), a line with the time so far and the length (`0:42` … `3:03`), and
PLAY/PAUSE, SKIP and STOP. The line can be dragged (a tall invisible target round the thin line), or focused and
moved with the arrow keys (5 s), Page Up and Page Down (30 s), Home and End; it keeps playing, or stays paused, as it
was. The time is the track's own, whichever copy (original or chip) is sounding. PLAY carries on as it was, one track
or the radio; SKIP goes to the next track the same way; STOP turns the radio off and pauses, and the track keeps its
place (the key says so). The page keeps room at the bottom so the player never covers the last tile, and the dancing
figure stands clear of it.

**Track links.** Each tile has a small share button at the end of its row. It copies
`https://field-unit.co.uk/?track=<id>` (the ids are in `POSTS`: `tuckshop`, `trenchcoat`, `nature-of-freak`,
`nomemory-notreal`, `the-of-the`, `curley-cuh`, `pocket-muck`, `medium-slate`, `lan-33`, `navvy`, `lbd-m3`, `wilt`;
keep an id once a link has gone out). The button turns to a tick and says "copied", and screen readers hear "link to
navvy copied". Where the page can't use the clipboard, the link appears in a field under the row, selected, to copy by
hand. Copying never touches what is playing.

Opening such a link is the same single page: it finds the track, brings its tile into view once, puts it in the
player and tries to play it from the start, as one track, in its original sound. If the browser won't let sound start
by itself (usual on a first visit), the track stays ready and the player shows one wide **▶ PLAY TUCKSHOP** button;
pressing it starts that track, and nothing says it's playing until it is. A track that fails to load shows its ∅ as
before. A link to a track that isn't there says so on the line under the buttons and plays nothing. The address
follows whichever track is playing, without adding to the browser's history, so it can be copied from the address
bar too, and the tab reads "tuckshop — field unit" ("field unit — music" before anything is picked). A shared link's
preview is the site's own (`og.png`): a page without a server can't give each track its own preview.

**The lock screen and headphones.** Where the browser offers it (the Media Session API), the track's name, "field
unit" and its artwork show in the system's media controls, and play, pause, stop, next, previous and seeking there
drive the same player. Not yet tried on a real phone's lock screen.

## Contact (23 Sep 2026)

The envelope opens a small panel under the controls; Esc or × closes it and focus goes back to the envelope. It
never touches the music.

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

## The chip face (was the CHIP FX switch, 23 Sep 2026)

CHIP FX came in as one switch in place of 12BIT and 8BIT, and is now one face of the dice. When it's rolled, every
track plays in a treated version of the same recording and the page's grain gets coarser to match; off, the
original and the normal picture come back.

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
- **Switching mid-track** keeps the music going. The other version is fetched only when it's wanted (the die
  starts fetching it as it rolls); while it loads the current one plays on and the dice's light blinks. When it's
  ready it is started at the same point in the song and cross-faded in over 60 ms, and the picture changes at that
  moment. Only the latest press counts. Paused, it swaps silently and stays paused. The radio and every tile play in
  whichever version is chosen. At most three treated files are kept loaded at once.
- **If a treated file can't load**, the original keeps playing, the dice goes back to off and the line under the
  buttons says so; rolling again can bring chip up again. If one fails while playing, the original carries on from
  the same place.
- **The picture:** the logo, the artwork on every tile, the footer strip and the dancer are drawn with 4-pixel
  blocks and three greens instead of five (the old 8BIT look). The dancer, the radio and the logo's motion all
  carry on through a change. Text, buttons and focus outlines stay sharp.
- The old bit crusher, its audio worklet and the two buttons are gone. The chip face needs no Web Audio, so it
  works with `index.html` opened straight from disk.
- Nothing ever plays on its own.

## Earlier changes

- **18 Sep 2026:** made from `field-unit.github.io-main.zip` (the original is in
  `../source-assets-private/field-unit-original/`). Games, tickets and the download page removed; the radio
  plays the tiles in turn, in step with them; play buttons are named after their tracks.
- **19 Sep:** `art-thumbs.js` carries a small copy of each artwork, so the grain works when the page is opened
  from disk.
- **21 Sep:** Wilt, a twelfth track, from `Tilted stuff Demo.wav`, 320 kbps like the rest.
- **23 Sep:** no dates on the tracks. Each tile shows the track's name alone, and the dates have gone from
  `POSTS` too, so they aren't in the page at all. The order of the list is unchanged, newest first.
- **22 Sep:** the dancer became a figure drawn in grain: ten joints stepping between poses with no easing, boxes
  and rods with gaps at the joints. Published on field-unit.co.uk. (Called a dancing figure since 24 Sep.)
- **23 Sep:** the draw tool (floating ink drawings, with its clear button) removed; the talking ∅ took its place as
  the page's odd thing to play with. The CHIP FX switch became the fx dice. A shared link now shows "field unit",
  a line about the site and `og.png` (the logo, the buttons and three tiles, cut from a screenshot) instead of a
  bare ∅. The artwork files carry no camera details.

## Adding a track

1. Put the MP3 and its artwork in this folder, and run `python tools/strip_meta.py <artwork>`: it takes the
   camera details (make, date, location) out of the file without touching the picture.
2. Add a line to `POSTS` near the top of `index.html`'s script — newest first, oldest last, with an `id` for its
   link (lower case, hyphens): `{ id:"wilt", title:"Wilt", audio:"Wilt_Demo.mp3", art:"Wilt_Artwork.jpg" },`
3. `python tools/make_art_thumbs.py` adds a small copy of the artwork to `art-thumbs.js`. The tiles' grain reads
   only brightness, so a dark, flat picture comes out as one shade of green: give it an entry in `TUNE` in that
   tool (where the tile's strip sits, and a brightness stretch) and run it with `--redo <artwork>`. LAN_33 and
   medium slate have one (24 Sep); their artwork files are unchanged.
4. `python tools/chip_fx.py` renders its chip version and updates the manifest (the others are left alone).
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
http://127.0.0.1:8160/. `tools/serve.py` answers byte ranges as GitHub Pages does, so seeking and the chip
hand-over behave as they will online; Python's own `http.server` doesn't, and seeking fails there. Offline, the
pixel font (Press Start 2P, from Google Fonts) falls back to the system monospace.

## Publishing

This folder is the `field-unit.github.io` repository: commit and `git push` from this PC, and GitHub Pages serves
it at field-unit.co.uk a minute later. `Open music site locally.bat` and `tools/` stay on this PC (`.gitignore`).
