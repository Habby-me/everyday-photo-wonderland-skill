# Generation and QA

## Prompt recipe

Use the following scaffold, omitting irrelevant lines. Write concrete visual instructions and repeat invariants at the end.

```text
Use case: style-transfer
Asset type: <personal keepsake / social post / print / wallpaper / other>
Primary request: Transform the edit-target lifestyle photo into a whimsical hand-drawn miniature world.
Input images: Image 1 is the edit target; Images 2–N are style references only.
Background policy: <scene-preserve / subject-first>
Preserve: <identity, pose, pet markings, clothing, key object, memory cues, broad framing>
Replace: <all non-subject pixels / only named background elements>
World mechanism: <one ordinary subject becomes a giant inhabitable landscape>
Miniature story: <2–3 clear activities and scale cues>
Character treatment: <recognizable humans / animal avatars / object-creatures>
Style/medium: <route-specific medium, line quality, paper/paint texture>
Composition/framing: <hero-object share, camera angle, density, aspect ratio>
Color palette: <dominant colors + limited warm accent>
Lighting/mood: <soft, calm, playful, nostalgic>
Constraints: Preserve every listed invariant. In subject-first mode, use Image 1 only for the isolated subject and replace the entire original environment.
Avoid: photorealistic 3D, glossy CGI, horror, clutter, extra limbs, duplicate people, illegible anatomy, text, logos, signatures, watermarks.
```

Do not say “copy Image 2 exactly.” Say which observable qualities to borrow and require an original composition based on the edit target.

## Subject-first prompt fragment

Use this fragment when the uploaded photo contains a strong subject in an unimportant setting:

```text
Image 1 supplies only the main subject. Preserve its identity anchors, pose, silhouette, gaze, and visible markings. Discard every other source element and rebuild the environment from scratch. Do not retain or reinterpret the original bed, wall, curtains, bag, furniture, floor, clutter, or room lighting. Place the isolated subject naturally inside the newly described world, with clean edge integration and no halo. Keep the face unobstructed.
```

For a giant-subject miniature scene, let the subject fill 45–65% of the frame and add two or three unmistakable scale cues. Do not shrink the subject into an ordinary animal inside a large landscape.

## Route fragments

Append one chosen fragment:

- **A:** fine imperfect ink contours, transparent watercolor washes, off-white paper grain, layered botanical foliage, sage and mint greens, warm soil and tiny orange accents.
- **B:** rounded friendly silhouettes, soft watercolor and colored pencil, oversized edible forms, cute miniature workers or animal avatars, fresh green with peach and terracotta accents.
- **C:** clean cream-white negative space, isolated giant object, orbiting characters, crisp editorial line work, dry-brush grain, high silhouette clarity.
- **D:** matte gouache and crayon grain, chunky geometric shapes, slightly rough edges, limited olive-mustard-orange palette, close cropped retro editorial composition.
- **E:** clean precise line art, flat teal-emerald-chartreuse colors, minimal shading, object-as-ecosystem concept, playful modern surrealism.

## Clean-color mode

Enable this mode when the user asks for fewer dots, less AI texture, cleaner coloring, or less fragmented paint. It overrides route phrases such as `paper grain`, `dry-brush grain`, and `crayon grain`.

- Allocate roughly 70% of the image to broad quiet color areas, 25% to purposeful contours and readable shapes, and at most 5% to small details near faces or functional scale cues.
- Build each large subject from two or three connected value shapes. For an animal, use identity markings and silhouette instead of dense fur texture; allow no more than 8–12 purposeful fur-direction lines across the body.
- Fill each large leaf coherently and keep one main vein plus at most two secondary veins. Merge moss, grass, ground, clouds, and distant foliage into connected masses rather than repeated dabs.
- Keep any paper texture extremely subtle, uniform, continuous, and low-contrast. Never express texture as isolated points.
- Explicitly ban stippling, speckling, dry-brush peppering, spray, confetti, scattered white flecks, granular watercolor blooms, mottled fur, repeated tiny curls, and random highlight dots.

## Preservation checklist

Before generation, name the invariants. For a person or pet, include at least three identity anchors that are actually visible. Examples:

- face shape and hair silhouette;
- glasses or a distinctive accessory;
- clothing color and cut;
- body pose or hand placement;
- pet coat pattern, ear shape, or collar;
- a place-specific sign, window, table, bicycle, dish, or landmark;
- relative positions when several people appear.

Do not invent hidden details. If a face is tiny, blurred, or obstructed, state that likeness may be approximate.

## Visual QA scorecard

Check each output on a 0–2 scale:

| Criterion | 0 | 1 | 2 |
|---|---|---|---|
| Identity/source | lost | partly recognizable | key anchors preserved |
| Scale story | unclear | one weak cue | giant/miniature relation obvious |
| Route match | generic | some route traits | medium, palette, and composition align |
| Composition | chaotic/empty | usable | clear hierarchy and readable actions |
| Artifact control | major errors | minor errors | no distracting anatomy/text/logo issues |
| Background replacement | source clutter remains | mostly replaced | old setting fully absent and new world coherent |
| Surface coherence | noisy or fragmented | mixed quiet/noisy areas | broad connected fills with only purposeful detail |

Do not call a draft final when any criterion scores 0. Explain the weakest criterion and make one targeted revision.

## Diagnosis and targeted fixes

| Symptom | Next change |
|---|---|
| Face or pet identity drifted | Reduce abstraction; restate 3 visible identity anchors; keep pose and crop; remove unnecessary tiny characters near the face. |
| Output still looks photographic | Strengthen the chosen physical medium, simplified value shapes, hand-drawn contour, and paper/paint texture; exclude photographic depth of field and glossy rendering. |
| Miniature idea is unclear | Increase the hero object's frame share and add one explicit size cue such as a ladder, door, table, bridge, path, or rope. |
| Scene is too busy | Keep one hero object and two secondary activities; simplify foliage/background and create quiet negative space. |
| Scene is too empty | Add one foreground layer, one background layer, and two small narrative actions without changing the hero. |
| Everything is green | Preserve source skin/clothing colors and reserve 10–20% of the palette for warm orange, coral, ochre, or cream accents. |
| It copies a reference composition | Rebuild the layout from the source photo, change viewpoint and character actions, and retain only the shared medium/palette traits. |
| Unwanted words or marks appear | Repeat “no text, lettering, signatures, artist marks, logos, or watermarks”; simplify small high-contrast patches. |
| Original room or bedding remains | Switch to `subject-first`; declare Image 1 subject-only; list every old setting element to remove; describe a complete replacement scene. |
| Subject looks pasted on | Match contour weight, palette, value grouping, and contact shadows to the new illustration; remove halos and photographic edge detail. |
| Random dots or AI-like texture appear | Enable clean-color mode; apply the 70/25/5 detail budget; merge fur, moss, leaves, and ground into broad connected fills; ban every point-based texture term. |

## Iteration language

Offer specific choices tied to visible results, not vague “more style” requests. Good options include:

- 更像本人：提高五官、发型和服装的保留度。
- 更像微缩世界：放大主体并增加明确比例参照。
- 更松弛：减少角色数量，留出呼吸感。
- 更有手绘感：加强纸纹、透明水彩叠色或蜡笔颗粒。
- 更暖：降低绿色占比，增加橙、土黄和奶油色。

Change only one main variable per revision. Keep all previous invariants and successful elements explicit.
