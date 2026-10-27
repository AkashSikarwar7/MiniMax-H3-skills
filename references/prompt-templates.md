# RunDiffusion H3 Prompt Templates

Use these as compact scaffolds. Replace every bracketed placeholder and remove sections that do not apply. Keep the prompt in English except for exact dialogue, lyrics, or visible text that must remain in its original language.

## Simple prompt

```text
[visual style, lighting, and mood]

Image 1 defines [role]. Image 2 defines [role]. Video 1 guides [specific motion/camera/pacing/voice/sound role]. Preserve [few critical details].

[Opening composition]. [Subject] [visible action in chronological order]. The camera [one main camera behavior]. [Exact short dialogue, if any]. End on [final pose/composition].

Sound includes [action-synchronized sounds].
```

Use this for a single subject, a small reference set, or an exploratory generation.

## Three-part keyframe prompt

Use one alignment instruction at the top, matching the selected frame mode, then keep the fields in this order:

```text
[frame alignment instruction]

integrated_multimodal_description: [Shot 1] [style and opening composition]. [Playback-order action, camera, dialogue, and synchronized sound. Add later shots with in-duration cut times only when needed.]

overall_soundscape: [Clip-wide ambience and non-verbal physical sounds.]

non_diegetic_music: [Audience-only score, or N/A.]
```

Frame-mode logic:

- Start Frame: state that the uploaded picture is fully referenced at 0.00 seconds and develop forward from it.
- End Frame: state that the uploaded picture aligns with the final timestamp and describe a plausible path that converges to it.
- Start + End Frame: align the two pictures to the opening and final timestamps and describe the continuous physical transition between them.

## Six-part reference prompt

Use this when several subjects, a storyboard, a reference video, or voice reference must remain traceable:

```text
subject_definitions:
<Subject 1> is [reusable person/object/place/style] from [asset]. Preserve [critical attributes].
<Picture 1> is [exact frame or storyboard role, only if the picture itself is a frame/planning anchor].
<Video 1> supplies [specific motion/camera/pacing role].
<Audio 1> is [voice/audio role] for <Subject 1> (S1).

summary:
[reference generation + optional audio reference/keyframe relationship] [one paragraph describing the target and main reference relationships.]

retention_analysis:
<Subject 1> (appears in [shots]): fully_preserved - [what remains stable].
<Video 1> ([role]): attribute_transfer - [what transfers and what does not].
<Audio 1>: reference - [timbre/delivery or sound qualities used without copying the signal].

detailed_description:
[Visual style before Shot 1.]
[Shot 1] [composition, subjects, action, camera, dialogue, and synchronized sound.]
[Shot 2] At [time], [new information and continuity from the previous shot.]

overall_soundscape:
[Clip-wide ambience and non-verbal sounds.]

non_diegetic_music:
[Audience-only music, or N/A.]
```

Use `fully_preserved`, `partially_preserved`, `attribute_transfer`, or `weak_reference` for visible references. Use `fully_copy`, `partially_copy`, `reference`, or `weak_reference` for audio references. Keep label meanings stable across all sections.

## Storyboard or sheet mapping

For one organized image:

```text
Image 1 upper section defines [cast/identity/wardrobe/props].
Image 1 lower section guides [shot order/framing/action] for Shots [1–N].
Render the final video in [style] and preserve [critical recurring details].
```

For separate panels, assign one image to each shot and state its intended viewpoint or placement. Treat the storyboard as guidance, not a frame-by-frame guarantee.

## Output checklist

- Correct H3 mode and reference workflow selected.
- Every uploaded asset has a named role.
- Identity, product, setting, and lighting details that matter are protected.
- Actions are chronological and achievable within the duration.
- Each shot has one dominant camera idea.
- Cut times are inside the clip duration.
- Dialogue is exact, short, and mapped to the right speaker.
- Ambience, synchronized sound, and audience-only music are separated.
- Start/end frame alignment and aspect-ratio assumptions are explicit.
