# Mouse & 17 Demons

Hell looks at you and laughs!
Welcome to The Mouse & 17 Demons,A rage game made in powerpoint for wrong tool ysws

## Play it in a browser

The whole game is now available as a single HTML file - no PowerPoint required.

1. Download this repository (or just the `Mouse_&_17_Demons.html` file **together with
   the `assets` folder** - they belong next to each other).
2. Open `Mouse_&_17_Demons.html` in any modern browser (Chrome, Edge, Firefox, Safari).
3. Click the shapes to play. Keyboard also works:
   <kbd>Space</kbd> / <kbd>&rarr;</kbd> next slide, <kbd>&larr;</kbd> previous,
   <kbd>Home</kbd> / <kbd>End</kbd> first / last slide, <kbd>R</kbd> restart.

**Playtesting shortcut:** <kbd>&rarr;</kbd> / <kbd>&darr;</kbd> (or
<kbd>Space</kbd>, <kbd>PageDown</kbd>, <kbd>Enter</kbd>) jump straight to the next
level and <kbd>&larr;</kbd> / <kbd>&uarr;</kbd> to the previous one, from any point
of any slide - including while an animation is still playing. This is deliberately
kept in the browser build so levels can be skipped while testing; it has nothing to
do with the in-game click/hover logic.

The browser build reproduces the original exactly: the same 50 slides, the same
animations, the same sound effects, the same click/hover traps and the same Office
Math formula.

## Play it in PowerPoint

You can play this by:
Clicking on that green button and clicking download zip
Extract the zip
and then double clicking the Mouse_&_17_Demons.pptm file (Make sure you have powerpoint installed!)
<img width="608" height="24" alt="{F586BD88-F9FE-4AA8-ABA2-0DF3A03C174E}" src="https://github.com/user-attachments/assets/e328818a-c801-4cea-8fe1-81e8d4ef21ff" />
<p>Double Click This!</p>

## What is the lore behind this game?
You are Mouse!,A resident of mouseville.You were at your everyday life existing when suddenly a demon kidnapped you and brought you to hell!
Your goal is to defeat the demon and get out this hellish place ASAP
## Screenshots
<img width="824" height="462" alt="{8684CE87-87F1-49F3-B102-75E91CE94C6E}" src="https://github.com/user-attachments/assets/b9b3ea0d-58c0-4f54-8897-674588e0e00a" />
<p>Vs. Reddit Mod</p>
<img width="817" height="461" alt="{622A4473-2382-4622-8805-E898B800F424}" src="https://github.com/user-attachments/assets/0e4c0730-6939-40cd-9210-a508d5889918" />
<p>Precursor to slack fight</p> 
<img width="814" height="457" alt="{C08169E2-8D13-4DCD-8809-21DDE5CC5C13}" src="https://github.com/user-attachments/assets/455d43c7-4597-46fe-be12-8ac74667ef74" />
<p>Precursor to final fight</p>
<img width="816" height="463" alt="{AAA29A93-EE1D-4986-A600-864CF97A2D9F}" src="https://github.com/user-attachments/assets/50629ec4-3e38-42bb-893a-4081b87099b0" />
<p>A random level</p>

## Why is this game so hard?
<p>Skill issue XD try harder </p> 
If you rage quit this game you have to give me a pico-8 license

## How can i contact this game's creator?
Contact @Cat on slack or email me at kartikmeow71@gmailcom

---

## Rebuilding the HTML version

The HTML build is generated from the `.pptm` by a small converter, so it can be
regenerated whenever the presentation changes.

```bash
python tools/pptm_to_html.py "Mouse_&_17_Demons.pptm" --out .
```

| file | purpose |
| --- | --- |
| `tools/pptm_to_html.py` | reads the OOXML package and emits the HTML + `assets/` |
| `tools/runtime.js` | the playback engine (inlined into the HTML) |
| `tools/style.css` | the stylesheet (inlined into the HTML) |
| `tools/fetch_fonts.py` | downloads the fallback webfonts (Carlito, Lobster, Oswald) into `assets/fonts` |
| `tools/verify.js` | renders every slide with Chromium and pixel-diffs it against a PowerPoint export |
| `tools/playtest.js` | automated playthrough: navigation, sounds, interactive triggers, missing assets |

> Tip: append `?font=Calibri` to the HTML URL to force a single font family while
> comparing renders.

### How the port works

* **Geometry** - every shape is emitted as an absolutely positioned element in a
  fixed 1280x720 stage (1 px = 9525 EMU) that is scaled to the viewport, so the
  layout is identical on every screen.
* **Animation** - `ppt/timing` is interpreted at runtime rather than baked into
  keyframes: `set`, `animEffect` (fade / wipe / wheel), `anim` on
  `ppt_x`/`ppt_y`/`ppt_w`/`ppt_h`/`style.rotation`, `animScale`, `animRot` and
  `animMotion` (paths are parsed and sampled) are all supported, including the
  `tavLst` formula language (`#ppt_w*sin(2.5*pi*$)` and friends).
* **Game logic** - the 213 hyperlink actions (`nextslide`, `firstslide`,
  `hlinksldjump`, `noaction`, external URLs), the click/hover sound effects and
  the three click-triggered interactive sequences are reproduced verbatim.
* **Office Math** - the Fourier-series formula is rendered from the rasterised
  fallback that PowerPoint itself embeds, so it is pixel-identical.
* **3D models** - the three `.glb` models are shown through the rendered preview
  image PowerPoint caches for them (identical, and 21 MB lighter).
* **Fonts** - the exact fonts the deck asks for (Aptos, Aptos Display, Freestyle
  Script, Agency FB) are bundled in `assets/fonts` and declared with `@font-face`,
  so the page renders with the same letterforms everywhere - even on machines
  without Office. Carlito / Lobster / Oswald remain as last-resort fallbacks.
* **Anti-skip** - clicking the slide background no longer advances the level (that
  let you skip any puzzle by clicking out of bounds); the only exception is slide
  46, which has no forward link at all. The two invisible full-slide rectangles on
  slides 27/29 whose *hover* jumped to the next slide are ignored for the same
  reason.
