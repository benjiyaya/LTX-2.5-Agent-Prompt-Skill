---
name: ltx-2-5-prompter
description: "Use when making LTX 2.5 video prompts from ideas or media."
version: 1.0.0
author: Hermes Agent
license: MIT
metadata:
  hermes:
    tags: [video, prompt-engineering, ltx, lightricks, comfyui, text-to-video, image-to-video, multishot, creative]
    related_skills: [comfyui]
---

# LTX 2.5 Video Prompter

## Overview

Transform a user's rough video idea + attached assets into a production-grade LTX 2.5 video generation prompt. The skill handles three LTX 2.5 generation modes:

- **Single-Shot** — one continuous take. The default for most generations. Outputs a flowing cinematic paragraph. Load `references/single-shot-format.md` for the full spec.
- **Multi-Shot** — NEW in LTX 2.5. Multiple connected shots with named cuts in a single generation. Outputs a chronological prose paragraph with explicit transitions. Load `references/multishot-format.md` for the full spec.
- **Screenplay-Style** — for dialogue-heavy scenes with character cues and timing beats. Load `references/screenplay-format.md` for the full spec.

The skill's distinctive value: it doesn't just format-comply — it **creatively enhances** the brief with professional-grade cinematic detail (camera aesthetics, visual texture, lighting design, pacing arcs, spatial choreography, continuity tracking) before mapping everything into the LTX 2.5 prompt format. Load `references/creative-examples.md` for quality benchmarks and pattern examples.

## When to Use

**Trigger when the user:**
- Attaches images/videos/audio and describes a video they want to create for LTX
- Says "make a video prompt" / "enhance this for LTX" / "write an LTX prompt" / "img2vid" / "txt2vid"
- Provides a video concept and wants it structured for LTX 2.5 generation
- Mentions LTX, LTX 2.5, Lightricks, LTXV, LTX Studio
- Pastes a creative brief and wants it converted to LTX format
- Asks about multishot prompts or multi-cut scenes

**Don't use for:**
- Non-LTX video models (H3, Sora, Runway, Kling, Seedance, Veo) — use the model-specific skill instead
- Pure image generation prompts
- Video editing tasks that don't involve new generation

## Step 0: Classify the Mode

Determine the LTX 2.5 mode from what the user attached and stated:

| User provides | Mode | Format reference |
|---|---|---|
| Nothing — just a text idea | **T2V** (text-to-video) → Single-Shot or Multi-Shot | `references/single-shot-format.md` or `references/multishot-format.md` |
| 1 image as the first frame | **I2V** (image-to-video) → Single-Shot preferred | `references/single-shot-format.md` |
| Multiple images as style/character references | **T2V with visual refs** → treat as inspiration | `references/single-shot-format.md` |
| Audio input | **A2V** (audio-to-video) → Single-Shot | `references/single-shot-format.md` |
| Source video for restyle | **V2V** (video-to-video) | `references/single-shot-format.md` |
| Requests multiple cuts/angles | **Multi-Shot** (NEW 2.5 feature) | `references/multishot-format.md` |
| Dialogue-heavy scene with character cues | **Screenplay-Style** | `references/screenplay-format.md` |

**Key question to ask:** "Single continuous shot, or multiple cuts? LTX 2.5 supports native multishot (2–4 connected shots in one generation)."

**When in doubt:** Default to Single-Shot. It's the most reliable mode, especially for I2V from a first frame.

## Step 1: Gather Parameters

**This skill is INTERACTIVE.** Ask the user for these before generating. Proceed only when enough information is available.

Confirm these (ask if missing, but proceed if the idea is clear enough):

- **Mode**: Single-shot, multishot (2–4 cuts), or screenplay-style?
- **Duration**: Let LTX auto-predict (2.5 feature), or specify? Default: auto-predict.
- **Aspect ratio**: 16:9, 9:16, 1:1, 4:3. Default: 16:9.
- **Resolution target**: Stage 1 (e.g., 544×960), Stage 2 (2× upscale). Default: Stage 1 + spatial upscale.
- **Asset inventory**: What each attached file is and its role (first frame, style ref, audio track, etc.)
- **Audio**: Should the prompt include audio description? LTX 2.5 generates synced audio natively.
- **Tone/mood reference**: Any films, shows, or visual styles to match?

### Technical Constraints (LTX 2.5)

- **Frame count**: `num_frames % 8 == 1` (1, 9, 17, 25, ..., 121, ...)
- **Resolution**: Width and height divisible by 32
- **Distilled model**: Fixed 8-step schedule, CFG=1
- **Auto-duration**: Omit `--num-frames` to let the duration head predict clip length from the prompt
- **VRAM**: 16GB minimum (int8 convrot), 24GB+ recommended for bf16

## Step 2: Creative Enhancement

This is the core value-add. Take the user's idea and enrich it across six dimensions — the LTX 2.5 "6-Part Structure." The goal: produce a prompt with the depth of a professional cinematographer's shot description.

### The 6-Part Prompt Structure (LTX 2.5)

Models weight earliest tokens more heavily. Structure the prompt in this order:

**1. Establish the Shot** — Cinematography terms matching the genre:
- Shot scale: extreme close-up, close-up, medium close-up, medium, medium wide, wide, extreme wide
- Angle: eye-level, low angle, high angle, overhead, Dutch angle
- Style markers: documentary, film noir, anime, period drama, arthouse, 35mm, Alexa

**2. Set the Scene** — Lighting, color, texture, atmosphere:
- Lighting: natural sunlight, golden hour, neon glow, flickering candles, dramatic shadows, sodium streetlights, soft key light, back-lit rim
- Color palette: vibrant, muted, monochromatic, high contrast, warm, cool
- Textures: rough stone, smooth metal, worn fabric, glossy surfaces, wet asphalt
- Atmosphere: fog, rain, dust, smoke, particles

**3. Describe the Action** — Core action as a natural sequence:
- Write as a flowing sequence from beginning to end
- Use present tense verbs ("walks" not "walked")
- One dominant action per shot — never cram multiple actions
- Describe how subjects move through space

**4. Define Character(s)** — Physical specificity:
- Age range, build, hair color/style, skin tone, distinctive features
- Wardrobe: specific garments with colors, materials, textures, accessories
- **Express emotion through physical cues** — "eyes widen," "lips tremble," "grips the table edge" — NOT abstract labels like "sad" or "confused"
- Visual signature: a recurring element that makes the character recognizable across shots

**5. Camera Movement** — How and when the camera moves:
- Types: slow push-in, slow pull-back, dolly left/right, handheld tracking, orbit, crane up, whip pan, static frame, follow shot, overhead view
- Name the move first, intensity second: "Slow orbit, roughly 45 degrees over the shot length"
- For I2V: describe what happens AFTER the initial frame — the transition from stillness to motion
- State what the subject looks like after the movement completes

**6. Describe the Audio** — Full soundscape:
- Ambient sound: rain on pavement, distant traffic, forest birds, coffeeshop chatter
- Physical action sounds: footsteps, door creak, fabric rustling, liquid pouring
- Music: instrumentation, tempo, mood — specify if diegetic (visible source) or non-diegetic (score)
- Dialogue: place in quotation marks, specify language and accent
- Voice qualities: whisper, mutter, shout, scream; resonant, cracking, monotone, childlike

### Enhancement Quality Bar

Every prompt must demonstrate:
- **Specificity over vagueness**: "A young woman in a red coat walking briskly through a rain-soaked Tokyo street" beats "a person walking"
- **Named references over qualifiers**: "Shot on 35mm, documentary look" beats "cinematic" or "beautiful"
- **Physical cues over emotional labels**: "He pauses, looks to the side, voice cracking" beats "he looks sad"
- **One action per shot**: Never cram 3 verbs into a single shot description
- **Consistent light logic**: One coherent light source per shot; mixed lighting confuses the model

## Step 3: Format and Output

Load the appropriate format reference and produce the final LTX 2.5 prompt.

**For Single-Shot** → Load `references/single-shot-format.md`. Output:
1. One flowing paragraph, 4–8 descriptive sentences
2. Present tense throughout
3. Six elements integrated naturally (shot → scene → action → character → camera → audio)
4. Dialogue in quotation marks
5. No markdown, no field labels, no preamble — just the prose prompt

**For Multi-Shot** → Load `references/multishot-format.md`. Output:
1. One chronological paragraph (NOT a shot list, NOT numbered beats)
2. Each cut introduced with a named transition: "A hard cut transitions to...", "A match cut connects...", "The image dissolves into..."
3. At every cut: re-establish framing, re-identify characters, state audio continuity
4. 2–4 shots maximum
5. Each shot gets a clear job: establish → detail → reaction, or wide → medium → close-up
6. Same 6-element structure within each shot segment

**For Screenplay-Style** → Load `references/screenplay-format.md`. Output:
1. Scene header (INT./EXT. LOCATION – TIME)
2. Visual description paragraph
3. Character cues with physical acting directions
4. Dialogue in quotation marks
5. Camera and audio notes woven throughout
6. Same 6-element structure, formatted as a screenplay scene

### Critical Format Rules (all modes)

- Output ONLY the prompt text — no preamble, no explanation, no markdown fences, no field labels, no commentary around the prompt itself
- Write in **present tense** for all action and movement
- **Match prompt length to video duration**: short prompts for long videos leave the model without enough direction. 4–8 sentences for single-shot; longer for multishot/screenplay
- **One dominant action per shot** — this is a hard LTX constraint
- **No numerical specifications** — "camera pans at 2 degrees per second" doesn't work. Use natural language: "The camera slowly pans right"
- **No conflicting directions** — "peaceful lake with crashing waves" confuses the model. Be internally consistent
- **No abstract emotional labels** — use physical cues instead
- Dialogue: always in quotation marks, verbatim. Specify language/accent if non-English
- On-screen text: describe it but note that exact spelling isn't guaranteed — keep it short and prominent
- Avoid named third-party IP, real celebrities, trademarked characters — describe generically

### Camera Vocabulary (LTX)

**Shot size**: extreme close-up · close-up · medium close-up · medium · medium wide · wide · extreme wide
**Angle**: eye-level · low angle · high angle · overhead · Dutch angle
**Movement**: static · slow push-in · slow pull-back · dolly left · dolly right · handheld tracking · orbit · crane up · whip pan · follow shot
**Depth**: shallow depth of field · deep focus · rack focus
**Transitions (multishot)**: hard cut · match cut · dissolve · fade · jump cut

### Helpful Vocabulary Reference

Load `references/ltx-vocabulary.md` for the full categorized vocabulary list (animation styles, lighting, textures, color palettes, atmosphere, sound design, pacing effects, visual effects).

## Step 4: Present to User

After generating the LTX 2.5 prompt:

1. **Present the full prompt in a code block** so it can be copied directly into ComfyUI/LTX Studio
2. **State which mode was detected** and why (single-shot / multishot / screenplay)
3. **List the 6 elements** as a checklist showing what was included
4. **Flag any assumptions** made (e.g., "Assumed 8s auto-duration and 16:9 — adjust if needed")
5. **Offer to refine** specific aspects: camera aesthetic, pacing, character detail, shot count, sound design, multishot vs single-shot

### Also Provide (when relevant)

- **ComfyUI settings**: Suggested resolution (e.g., 768×512 or 544×960), frame count (`num_frames % 8 == 1`), steps (8 for distilled), CFG (1.0 for distilled)
- **Model files needed**: Which `.safetensors` to load (distilled vs dev, bf16 vs int8 convrot)
- **Duration head**: Whether to enable auto-duration or set manual frames
- **Spatial upscaler**: Note that LTX 2.3 spatial upscaler is still required for Stage 2

## Step 5: Interactive Refinement Loop

Offer iteration options (cheapest → most expensive change):

1. **Style keyword**: swap "documentary" for "commercial" or "shot on 35mm" for "shot on Alexa"
2. **Lighting direction**: swap "top-left key" for "back-lit rim"
3. **Camera move**: swap "slow push-in" for "static wide"
4. **Action verb**: swap "walks" for "strides" or "hesitates"
5. **Subject specificity**: add age, dress, demeanor
6. **Re-roll seed** (last resort before model settings)
7. **Change model settings** (guidance scale, steps) — nuclear option, changes everything

## LTX 2.5 Specifics (vs 2.3 and other models)

What makes LTX 2.5 prompting different from H3, Seedance, Veo, etc.:

- **Multishot is native** — no need for external editing or stitching. Write connected cuts in one prompt.
- **Prompt enhancer is built-in** — shorter raw prompts can work; the model expands them. But detailed prompts still produce better results.
- **Auto-duration** — omit frame count, let the model predict. Or set explicitly (`num_frames % 8 == 1`).
- **Gemma 4 12B encoder** — holds more detail per prompt than 2.3's T5-based encoder. Don't be afraid of long, complex prompts.
- **Audio is native** — describe sound in every prompt; the model generates synced audio + video.
- **4K HDR + RAW** — prompts can reference HDR aesthetics, ACES color pipelines, professional finishing looks.
- **No reference labels** — unlike H3's `<Subject N>` / `<Picture N>` system, LTX uses pure prose. Characters are identified by description, not tags.
- **No JSON structure** — LTX prompts are free-form cinematic prose. The 6-part structure is a mental model, not a literal output format.

## Common Pitfalls

1. **Cramming multiple actions into one shot.** One dominant action per shot — hard LTX constraint. Split sequential actions across multiple shots or separate generations.

2. **Using abstract emotional labels.** "She looks sad" → the model can't render "sad." Use: "Her eyes lower, she grips the coffee cup tighter, her shoulders slump."

3. **Writing a shot list instead of prose (multishot).** LTX multishot must be one chronological paragraph. Do NOT use `Shot 1:`, `Shot 2:`, or numbered beats. Weave cuts naturally: "A hard cut transitions to..."

4. **Forgetting camera movement.** Every shot needs camera specification — even "static frame" if intentional. Omitting it leaves the model guessing.

5. **Inconsistent character identity across shots (multishot).** Reuse visual identifiers for recurring characters: "the woman in the red coat, earlier at the table, now..."

6. **Conflicting directions.** "Peaceful, calm lake with dramatic crashing waves" — contradictions confuse the model. Pick one tone.

7. **Mismatched duration and prompt length.** 10-word prompt for a 10-second video = the model rushes through. Long videos need long prompts (4–8+ sentences).

8. **Over-constraining with numbers.** "Exactly 3 birds flying at 45 degrees, camera pans at 2°/sec" — LTX works with natural language, not numerical specs.

9. **Mixing diegetic and non-diegetic music.** Music audible to characters (radio, live performance) goes in the scene description. Background score goes in the audio description. Don't conflate.

10. **Vague qualifiers.** "Nice," "good," "beautiful," "cinematic" carry almost no signal. Replace with named references: "shot on 35mm," "documentary look," "Apple-style commercial."

11. **Skipping audio description.** LTX 2.5 generates native synced audio. Always describe the soundscape — ambient, action sounds, music, dialogue.

12. **Trusting on-screen text.** LTX 2.5 improves text rendering but exact spelling isn't guaranteed. Keep text short and prominent; add critical titles in post-production.

## Verification Checklist

- [ ] Mode correctly detected from user intent (single-shot / multishot / screenplay)
- [ ] All six prompt elements present (shot type, scene/lighting, action, character, camera, audio)
- [ ] Output is pure prose — no field labels, no markdown fences, no JSON structure
- [ ] Present tense throughout
- [ ] Exactly ONE dominant action per shot
- [ ] Camera movement specified for every shot
- [ ] Character identity consistent across all shots (multishot: re-identify at each cut)
- [ ] Emotion expressed through physical cues, not abstract labels
- [ ] Dialogue in quotation marks, preserved verbatim
- [ ] No conflicting directions or lighting contradictions
- [ ] Prompt length matches intended duration (4–8+ sentences for single-shot)
- [ ] Multishot only: transitions named in natural language ("hard cut", "match cut", "dissolve")
- [ ] Multishot only: audio continuity stated at each cut
- [ ] No named IP, celebrities, or trademarked character names
- [ ] Audio description included (ambient, action sounds, music, dialogue)
- [ ] No numerical specifications (use natural language instead)
