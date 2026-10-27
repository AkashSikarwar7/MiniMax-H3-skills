---
name: rundiffusion-h3-prompting
description: Create RunDiffusion-ready MiniMax H3 prompts for text, keyframes, reference images or video, storyboards, voice reference, and synchronized sound. Use when turning a video brief into an H3 prompt or diagnosing a weak H3 generation; not for operating the RunDiffusion UI or rendering videos.
---

# RunDiffusion H3 Prompting

Use this skill to translate a creative brief into a precise MiniMax H3 prompt that works with RunDiffusion's H3 or H3 Ref. to Video workflows. The goal is to remove ambiguity, preserve important reference details, and keep the requested action achievable within the selected duration.

Read [references/prompt-templates.md](references/prompt-templates.md) when producing a structured prompt, using keyframes, or combining several references.

## Workflow

1. Choose the generation mode before writing:
   - Text-to-video when the scene is fully described in text.
   - Start Frame when an uploaded image must be the exact opening composition.
   - End Frame when the video should plausibly arrive at an uploaded final composition.
   - Start + End Frame when the prompt must describe a continuous transition between two known states.
   - H3 Ref. to Video when images or a reference video guide identity, objects, setting, storyboard, motion, camera, pacing, voice, or sound.
2. Inventory every uploaded asset in upload order as `Image 1`, `Image 2`, `Video 1`, and so on. Give each asset an explicit role. If one asset supplies multiple related cues, name each cue instead of leaving H3 to infer the role.
3. Protect only the details that matter: identity markers, wardrobe, product geometry and visible text, setting anchors, composition, and lighting direction. Use a small compatible reference pack rather than many conflicting images.
4. Describe visible action in playback order. For each shot, state the current composition, subject position, action, one main camera behavior, and any sound caused by that action. Keep cuts, actions, dialogue, and camera changes realistic for the selected duration.
5. Choose the shortest prompt structure that preserves control. Use the simple structure for one subject or one clear reference; use the structured three-part format for keyframes; use the six-part reference format for multiple subjects, storyboard sheets, reference video, or voice referencing.
6. Separate RunDiffusion control settings from prompt prose. Put duration, resolution, aspect ratio, and upload choices in the UI settings; mention timing in the prompt only when it defines a cut or frame alignment.
7. Return the final prompt first, followed by a short setup checklist and any assumptions. Do not claim that H3 will reproduce a reference exactly; describe it as guidance unless the user explicitly requests a frame anchor.

## Reference roles

- A character image defines identity, not automatically the location or motion.
- A product image defines the product's shape, material, color, and printed details; explicitly prevent overlays or invented variants when those details matter.
- A location image defines the environment and lighting direction.
- A storyboard or sheet is a visual planning reference. Explain which region controls cast, shot order, framing, or action. Use shot-by-shot text only where a panel is ambiguous.
- A reference video can supply a readable action, camera path, cuts, pacing, voice delivery, or sound. State exactly which of these transfer, and what must not transfer.

## Motion and camera

Prefer one main camera idea per shot: static, push/pull, pan/tilt, truck/pedestal, arc, tracking, or a controlled zoom. Add speed or amplitude only when useful. Avoid contradictory instructions such as a static camera plus a fast orbit. For a short clip, begin with one continuous shot and add a cut only when it reveals new information.

For Start + End Frame, write the intermediate physical path rather than describing only the endpoints: opening state → observable action → intermediate state changes → final composition. For End Frame, infer a plausible earlier state and converge deliberately toward the final image.

## Voice and sound

- Use a clean, voice-forward reference video with permission to use the person's likeness or voice. Treat voice reference as timbre and delivery guidance, not an exact identity copy.
- Map the reference voice to the correct character and keep speaker IDs stable across shots.
- Write the target dialogue exactly, keep it short enough for the clip, and do not accidentally reproduce source-video words when only delivery is being referenced.
- Put action-synchronized physical sounds beside the action that creates them.
- Use `overall_soundscape` for clip-wide ambience and non-verbal sounds; do not repeat dialogue there.
- Use `non_diegetic_music` for audience-only music, or `N/A` when there is no background score. Do not use `N/A` for the entire soundscape unless complete silence is intended.

## Staged testing

When the brief is complex, recommend staged generation: prove identity and scene first; add one motion or camera path; add voice and sound; then add cuts, storyboard complexity, or a second character; only then make the final-resolution version. Higher resolution cannot repair conflicting references or an overloaded timeline.

## Troubleshooting

- Identity drift: reduce and reconcile the character pack; name a few stable features.
- Wrong part of an image copied: assign the image's role explicitly.
- Storyboard ignored: shorten the prompt, assign the sheet one clear role, and increase duration or reduce panels.
- Motion mismatch: use a cleaner reference clip with one readable action or camera idea.
- Wrong character gets the voice: bind the voice reference to a named speaker and reuse that mapping.
- Unwanted music: keep ambience in `overall_soundscape` and set `non_diegetic_music: N/A`.
- Rushed clip: remove actions, cuts, or dialogue before adding more detail.

The source guide's current RunDiffusion-specific values include 5–15 second clips, 768P or 2K output, up to five reference images in H3 Ref. to Video, and a 7,000-character prompt field. Treat the visible RunDiffusion controls as authoritative if they differ.
