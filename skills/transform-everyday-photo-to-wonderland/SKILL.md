---
name: transform-everyday-photo-to-wonderland
description: Guide and execute an interactive style-transfer workflow that turns an uploaded lifestyle photo into a whimsical hand-drawn miniature-world illustration. Preserve either the chosen subject or the meaningful scene, support subject isolation with complete background replacement, and provide a clean-color low-speckle rendering mode. Use when a user uploads a portrait, family, pet, food, travel, street, home, or everyday photo and asks for a botanical fairy-tale world, giant-object miniature scene, cute character illustration, watercolor/gouache/crayon storybook image, a new setting around the main subject, cleaner coloring with fewer AI-like dots, or help choosing and refining an illustration direction before generation.
---

# Transform Everyday Photo to Wonderland

Turn a real-life photo into a guided, controllable illustration. Treat the user's photo as the edit target and any user-supplied references as style guidance, not content to copy.

## Load the visual system

Read [references/style-system.md](references/style-system.md) before recommending a direction. Read [references/generation-and-qa.md](references/generation-and-qa.md) before composing the generation prompt or diagnosing an output.

## Use this conversation flow

### 1. Inspect and diagnose the photo

- Locate every uploaded image and label its role: `edit target`, `user style reference`, or `supporting input`.
- Inspect local images with `view_image` before making visual claims.
- Identify four things in the edit target:
  1. the strongest visual anchor;
  2. the memory or emotion worth preserving;
  3. immutable details such as identity, pose, pet markings, clothing color, object shape, or place cues;
  4. one promising scale-change or world-building opportunity.
- Tell the user the diagnosis in four short bullets. Do not bury the recommendation in a long critique.

### 1A. Choose the background policy

- Use `scene-preserve` when the place, architecture, furniture, event, or spatial relationship is part of the memory.
- Use `subject-first` when the background is generic, distracting, private, visually weak, or the user asks to keep only the person, pet, food, or object.
- In `subject-first`, preserve the subject's identity, pose, silhouette, visible markings, gaze, and essential contact shape. Treat every other pixel as replaceable.
- Remove source bedding, walls, curtains, bags, furniture, clutter, and lighting cues unless one item is structurally necessary to explain the pose.
- Build a wholly new setting suited to the subject. Let the subject occupy roughly 45–65% of the frame and establish scale with a ladder, path, bridge, doorway, cart, or tiny inhabitants.
- Keep narrative elements away from the face and do not allow remnants of the old background to leak into the new scene.

### 2. Offer three direction cards

- Select the three most suitable directions from the five routes in `style-system.md`.
- Put the recommended direction first.
- Describe each card with: route name, what becomes the giant anchor, who or what becomes miniature, medium/palette, and the main tradeoff.
- Ask the user to choose one route, combine two, or say “你帮我决定”. Ask no more than three short questions at once.
- If the user already specified a clear route, skip the menu and confirm the interpretation in one sentence.

### 3. Resolve only high-impact controls

Use the controls in `style-system.md`. Default to:

- high identity and memory-cue preservation for recognizable people or pets;
- one dominant giant anchor with a medium-density miniature story;
- recognizable illustrated humans unless the user asks for animal or object avatars;
- the source photo's aspect ratio and broad composition;
- botanical green with one warm accent;
- clean-color mode by default: broad connected fills, restrained continuous paper tone, and no point-based texture;
- no text.

Ask only about controls that would materially change the result. Never make a user answer every control before proceeding.

### 4. Present a visual prescription

Summarize the selected plan before the first render:

```text
保留：<3–5 immutable details>
变形：<giant anchor + miniature-world mechanism>
角色：<human / animal avatar / object creature>
画法：<medium + line quality + texture>
色彩：<dominant palette + accent>
构图：<framing + density + aspect ratio>
```

If the user is choosing interactively, wait for route selection before generation. If the user says to decide automatically or has already given a complete direction, proceed without another confirmation.

### 5. Generate with the built-in image tool

- Use the built-in `image_gen` path by default. Do not switch to CLI/API mode unless the user explicitly requests it.
- Treat the request as `style-transfer` when preserving the source subject or scene.
- Include the edit target and only one to three relevant style references. More references can blur the direction.
- When every required image has a local path, pass them through `referenced_image_paths` and name each role in the prompt.
- When the edit target has no local path, use `num_last_images_to_include` with the smallest count that includes it. Do not also pass `referenced_image_paths`; use the selected route's distilled visual language in the prompt instead.
- Preserve invariants explicitly in every iteration. Generate non-destructively and keep the source unchanged.
- For `subject-first`, state that Image 1 supplies only the isolated subject; explicitly reject all non-subject source content and describe the replacement setting from scratch.
- Use the clean-color mode in `generation-and-qa.md` unless the user explicitly requests grainy crayon, dry brush, stippling, or heavily granulating watercolor.
- Use one call per requested concept or variant. Do not use a generic batch prompt for distinct directions.
- Save a project-bound final inside the workspace with a descriptive, versioned filename. Preview-only drafts may remain in the default generated-image location.

### 6. Inspect and guide the next move

Inspect every result before presenting it. Evaluate:

- subject/identity preservation;
- clarity of the giant-versus-miniature scale story;
- match to the selected medium and palette;
- composition, anatomy, duplicated objects, unwanted text, logos, signatures, or watermarks.

Show the image, state what worked in one sentence, then offer at most three targeted next moves. Examples: “更像本人”, “微缩世界更明显”, “减少绿色并增加暖色”. Change one main variable per iteration and repeat all immutable details.

## Creative guardrails

- Derive a shared visual language from the references; do not trace a composition or reproduce a signature, watermark, logo, or artist credit.
- Describe observable traits such as broad watercolor wash, continuous paper tone, crisp line art, limited palette, or editorial white space. Do not rely on an artist's name as the style instruction.
- Keep the miniature story legible: one hero object, two or three secondary actions, and an obvious size cue such as a ladder, doorway, table, rope, pond, or path.
- Preserve faces, bodies, pet markings, and meaningful personal details unless the user explicitly approves stronger abstraction.
- Avoid adding unrequested characters, slogans, decorative text, brand marks, horror, grime, or photorealistic 3D rendering.
- Do not claim perfect likeness. If identity drifts, diagnose it and tighten the next prompt.

## Finish the task

Report the final saved path, selected route, final prompt, and any remaining identity or detail limitation. Keep the user-facing explanation in the user's language.
