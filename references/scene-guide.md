# Scene guide - drawing one idea per beat

Every idea in the voiceover gets its OWN drawing. For each beat decide: (1) the concrete image the words name or imply, (2) how it is drawn on, (3) the ambient animation, (4) the transition (ink wash, brush wipe, camera pan).

## Where things are in render.py
- `SC = dict(name=(start, end), ...)`: a window per drawing. A drawing function reads its own window: `s0, s1 = SC['name']; a = vis(t, s0, s1); lt = t - s0`, returns if `a <= 0`, and draws everything from the local time `lt`.
- `frame(t)`: the scene tuple `for fn in (sc_a, sc_b, ...)` runs the drawings; add yours there.
- Helpers: `stroke(fr, pts, progress, width, colour, alpha)` (brush stroke that reveals along its length), `wash`, `disc`, `ring`, `leaf`, `petal`, `blob` (red dot), `sparkle`, `person(fr, x, y_base, height, alpha, crown, red, pr)`, `catmull` (smooth path), `backout` (overshoot ease), `ss` (smoothstep), `enso`, `uline`.
- Colours: `BLK`, `RED`, `GREY`, `OCHRE`. Red is the only accent.
- Camera: `K` keys (time, cx, cy, zoom) with a PCHIP curve; `AMAX` is the Vitthal painting's visibility over time (low behind text, 1.0 only when He is the subject).
- Vitthal face shot: set `VIT_A, VIT_B`, the `K` keys (push to x 545, y 520-600, zoom 1.3-1.55) and `AMAX` to 1.0 for the same window; the red tilak is inked in by `vitthal()`.

## Ready drawings (see assets/scene_gallery.jpg)
sc_sunmoon (day and night, then red dot), sc_tilak (clock/time), sc_mukut / sc_mukut2 (crown, red suns), sc_pour (pot pours red into a bowl), sc_rain (dark cloud), sc_gather (people gathering), sc_restless (tangled lines), sc_eyes (eyes close, red dot - second hook), sc_garland, sc_cloth, sc_ear, sc_lamp (red flame), sc_tulsi (bead necklace), sc_feet (feet on brick), sc_murti, sc_garuda (bird), sc_mind, sc_wilt (wilting flower), sc_road (road to temple, pilgrim dot), sc_wishes (many dots drift, one red stays - takeaway), sc_lotus, sc_gem, sc_rakh (two figures), sc_sides (tall figure with two attendants), sc_sages (singing sages), sc_unique (grid of black dots, one red grows), sc_friend (red sun, tall and small figure), sc_crowd (crowd pushes one figure away), sc_words (scribbles toward a figure), sc_drop (rings fall off a figure), sc_drift (dots drift away), sc_dye (red fills a figure from the feet), sc_love (figure with glowing red heart), sc_world (globe with small people), sc_bowl / sc_bowl2 (leaking bowl; takes a window key), sc_near (two figures come together).

## New drawing checklist
- Reads at phone size: bold simple shapes, one focus, empty paper around.
- Inside x 40-980, y 360-1500 (top 120-340 holds the small original lines; subtitles at y 1340-1500 - keep the drawing above ~1300 or accept overlap only on paper-light areas).
- At least one moving element for the whole window; red "life" element appears late (about lt 1-3 s) on the key word.
- Draw-on with `stroke(... progress ...)`, ease with `ss` / `backout`.
- Test with `python3 -I render.py still <t>` at 2-3 moments inside the window.
