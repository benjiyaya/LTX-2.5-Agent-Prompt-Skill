# 🎬 LTX 2.5 Video Prompt Agent Skill

A [Hermes Agent](https://github.com/NousResearch/hermes-agent) skill that transforms rough video ideas + reference images/audio into production-grade **LTX 2.5** (Lightricks) video generation prompts.

Unlike structured-format skills (e.g., MiniMax H3), LTX 2.5 prompting is **pure natural language** — one flowing cinematic paragraph that reads like a shot description for a cinematographer. No JSON, no field labels, no tags. Just prose.

## What It Does

When you describe a video concept (with or without attached media), this skill:

1. **Detects the mode** — single-shot, multishot (NEW in 2.5), or screenplay-style
2. **Creatively enhances** your idea across 6 cinematic dimensions
3. **Outputs a natural-language prompt** — ready to paste into ComfyUI or LTX Studio

## LTX 2.5 Modes

| Mode | Use Case | Output Format |
|---|---|---|
| **Single-Shot** | One continuous take (T2V, I2V, A2V, V2V) | Flowing paragraph, 4–8 sentences |
| **Multi-Shot** ⭐ | Multiple connected cuts in one generation | Chronological prose with named transitions |
| **Screenplay-Style** | Dialogue-heavy scenes with character cues | Screenplay scene with acting directions |

⭐ **Native multishot is the headline feature of LTX 2.5.** Previous versions only produced a single continuous shot. Now you can generate 2–4 connected shots — holding character identity, environment, lighting, and voice across cuts — all from one prompt.

## The 6-Part Prompt Structure

Every prompt integrates these elements in order (models weight earliest tokens more heavily):

1. 🎥 **Establish the Shot** — Cinematography terms, shot scale, angle, style markers
2. 💡 **Set the Scene** — Lighting, color palette, textures, atmosphere
3. 🏃 **Describe the Action** — Core action as a flowing sequence, present tense
4. 👤 **Define Character(s)** — Physical specifics, wardrobe, emotion via physical cues
5. 📷 **Camera Movement** — How and when the camera moves, relative to subject
6. 🔊 **Describe the Audio** — Ambient sound, action SFX, music, dialogue

**Important:** This structure is a mental model for the writer. The output is pure prose — the model never sees field labels or numbered sections.

## Installation

### For Hermes Agent Users

Copy the skill folder to your Hermes skills directory:

```bash
# Linux/macOS
cp -r ltx-2-5-prompter ~/.hermes/skills/creative/

# Windows
xcopy ltx-2-5-prompter %LOCALAPPDATA%\hermes\skills\creative\ /E /I
```

Restart Hermes Agent. The skill auto-triggers when you mention LTX, attach media, and describe a video idea.

### For Other Agent Frameworks (Claude, Codex, etc.)

The `SKILL.md` and reference files are standard Markdown — load them as system context or project rules in any agent that supports file-based instructions.

## File Structure

```
ltx-2-5-prompter/
├── README.md                            # You are here
├── SKILL.md                             # Main skill — workflow, rules, verification
└── references/
    ├── single-shot-format.md            # Default mode — one continuous take
    ├── multishot-format.md              # NEW 2.5 feature — connected cuts in one prompt
    ├── screenplay-format.md             # Dialogue-heavy scenes with character cues
    ├── creative-examples.md             # Weak→strong transformations + advanced patterns
    └── ltx-vocabulary.md                # 100+ categorized cinematic terms
```

## Usage Examples

### Single-Shot (Text-to-Video)

```
💬 "A golden retriever running through a sunny meadow"
```

→ The skill enhances this into:

> Wide tracking shot of a golden retriever sprinting through a sunlit wildflower meadow, 
> golden hour light catching the fur, lens flares from the low sun, camera follows at 
> ground level alongside the dog, shallow depth of field with wildflowers blurring in 
> the foreground. The sound of padded footsteps on grass, distant birdsong, and a warm 
> breeze rustling the flowers.

### Multi-Shot (NEW in 2.5)

```
💬 "A woman in a raincoat waiting for someone at a rainy intersection, 
    then we see the person arriving — multishot"
```

→ The skill produces a chronological paragraph with named cuts, audio continuity, and 
character re-identification at each transition. 2–4 shots, each with a clear job 
(establish → detail → reaction).

### Screenplay-Style (Dialogue Scene)

```
💬 "A news reporter discovering oil has been found in a small town, 
    live broadcast format"
```

→ The skill formats the scene with INT./EXT. headers, character cues, physical acting 
directions between dialogue beats, and camera/audio notes woven throughout.

## Weak → Strong Transformation

| Weak Prompt | Why It Fails | Strong Prompt |
|---|---|---|
| "A nice cinematic video of a person walking" | No shot type, no lighting, no character, no camera, no audio — "nice" and "cinematic" carry no signal | "Wide tracking shot of a young courier in a rain shell walking briskly through a Shibuya backstreet at 6pm, warm sodium streetlights reflecting on wet asphalt, camera dollies alongside at hip height, shallow depth of field, documentary look on 35mm" |
| "A sad man talks about his family" | "Sad" is an abstract label the model can't render | "A middle-aged man with greying hair speaks in a slow-paced voice, pauses, looks to the side, voice cracking — eyes widening momentarily" |
| "A product shot of a bottle" | Zero specificity | "Close-up product shot of a brushed-steel water bottle on bone-white marble, slow 20-degree camera arc, soft key light top-left, matte-black backdrop, high-end commercial aesthetic" |

## What's New in LTX 2.5 (vs 2.3)

| Feature | LTX 2.3 | LTX 2.5 |
|---|---|---|
| **Multishot** | Single continuous shot only | Native multishot (2–4 connected cuts) ⭐ |
| **Text Encoder** | T5-based | Custom Gemma 4 12B (holds more detail) |
| **Video Decoder** | Standard VAE | Diffusion video decoder (sharper faces/text) |
| **Prompt Enhancer** | Not built-in | Built-in, auto-expands short prompts |
| **Duration** | Manual frame count | Optional auto-predict from prompt |
| **Rendering** | Fixed compression | Diffusion Fidelity (dynamic compute) |
| **Resolution** | Up to ~1080p | Native 4K HDR + RAW pipeline |
| **Artifacts** | 0.74 (Pro score) | 0.28 (2.6× improvement) |
| **Speed** | Slower | 6.8s on-prem (10s I2V clip) |
| **Parameters** | 22B DiT | 22B DiT (same — everything else is new) |
| **License** | Open, free < $10M ARR | Same |

## Key Prompting Principles

1. **Natural language, not tags** — LTX reads prose like a cinematographer reads a shot description
2. **One action per shot** — never cram multiple actions; split across shots or generations
3. **Physical cues, not emotional labels** — "eyes widen, voice cracking" not "sad"
4. **Named references, not vague qualifiers** — "shot on 35mm, documentary look" not "cinematic"
5. **Match length to duration** — short prompts for long videos leave the model without direction
6. **One coherent light source** — mixed lighting confuses scene interpretation
7. **Always describe audio** — LTX 2.5 generates synced audio natively
8. **Present tense throughout** — "walks" not "walked"

## Multishot Transition Vocabulary

| Transition | When to Use | Example Phrasing |
|---|---|---|
| **Hard cut** | Abrupt, most common | "A hard cut transitions to..." |
| **Match cut** | Visually similar compositions | "A match cut connects..." |
| **Dissolve** | Gradual blend, time passage | "The image dissolves into..." |
| **Jump cut** | Temporal leap | "A jump cut leaps to..." |
| **Fade** | Through black/white | "The scene fades to black, then reveals..." |

At every cut, state: new framing, who's in frame (re-identified), and audio continuity 
("the score continues across the cut" or "the music drops; only wind remains").

## Technical Constraints (LTX 2.5)

- **Frame count:** `num_frames % 8 == 1` (1, 9, 17, 25, ..., 121, ...)
- **Resolution:** Width and height divisible by 32
- **Distilled model:** Fixed 8-step schedule, CFG=1
- **Auto-duration:** Omit `--num-frames` to let the duration head predict clip length
- **VRAM:** 16GB minimum (int8 convrot), 24GB+ recommended (bf16)
- **Spatial upscaler:** LTX 2.3 spatial upscaler still required for Stage 2

## Sources & References

- [LTX 2.5 Model Page](https://ltx.io/model/ltx-2-5) — Official features and benchmarks
- [LTX 2.5 HuggingFace](https://huggingface.co/Lightricks/LTX-2.5) — Model card, weights, code samples
- [LTX 2.5 Prompt Guide](https://ltx.io/blog/ltx-2-5-prompt-guide) — Official prompting guide
- [LTX 2.3 Prompt Guide](https://ltx.io/blog/ltx-2-3-prompt-guide) — Previous version reference
- [AI Video Prompt Guide](https://ltx.io/blog/ai-video-prompt-guide) — General 6-part structure

## License

MIT — use freely. The LTX 2.5 model weights themselves are under the [LTX-2.x Community License](https://huggingface.co/Lightricks/LTX-2.5) (free for organizations under $10M ARR).

## Author

**Benji AI Playground** — [YouTube](https://youtube.com/@benjiAIplayground) · [GitHub](https://github.com/benjiyaya)

In-depth technical AI video content. H3, LTX, SeeDance pipelines and workflows.
