# Single-Shot Format (LTX 2.5)

## When to Use

- Text-to-video (T2V) with no frame anchors
- Image-to-video (I2V) from a single first frame
- Audio-to-video (A2V) where audio anchors temporal structure
- Video-to-video (V2V) restyle
- Any generation where the user wants ONE continuous take

## Output Format

A single flowing paragraph, 4–8 descriptive sentences. No headers, no field labels, no markdown. Just cinematic prose.

## Structure

Integrate the 6 elements in this order (models weight earliest tokens more heavily):

1. **Shot type + style** → "Wide tracking shot, documentary look on 35mm,"
2. **Scene/lighting** → "warm sodium streetlights reflecting on wet asphalt after rain,"
3. **Character** → "a young courier in a rain shell,"
4. **Action** → "walking briskly through a Shibuya backstreet at 6pm, glancing at a paper map,"
5. **Camera movement** → "camera dollies alongside at hip height, shallow depth of field,"
6. **Audio** → "the sound of rain on pavement and distant traffic fills the air."

## Rules

- **Present tense** throughout ("walks" not "walked")
- **One dominant action** — never cram multiple actions
- **No shot lists or numbered beats** — this is one continuous take
- **Match detail to shot scale** — close-ups need more detail than wide shots
- **Describe camera movement relative to the subject**
- **Dialogue in quotation marks** — "He whispers, 'Wait for me.'"
- **No preamble or commentary** — output ONLY the prompt prose

## I2V Specifics

When generating from a first frame image:
- Do NOT describe static elements already visible in the image
- DO describe the transition from stillness to motion
- DO describe what happens next — how the subject moves, how the camera follows, what sounds emerge
- Focus the prompt on MOTION and ACTION

## Length Guidance

| Duration | Sentences | Detail Level |
|---|---|---|
| 2–4s | 3–4 | Lean, one clear action |
| 5–8s | 4–6 | Moderate, action + environment |
| 9–12s | 6–8 | Rich, multiple sensory layers |
| 13s+ | 8+ | Dense, but still one continuous action |

**Note**: With LTX 2.5's auto-duration predictor, you can omit explicit duration. The model infers clip length from prompt complexity.

## Examples

### Strong Single-Shot (T2V)

> Wide tracking shot of a young courier in a rain shell walking briskly through a Shibuya backstreet at 6pm, glancing at a paper map, warm sodium streetlights reflecting on wet asphalt, camera dollies alongside at hip height, shallow depth of field, documentary look on 35mm. The sound of rain on pavement and distant traffic fills the air.

### Strong Single-Shot (I2V)

> The camera slowly dollies out as wind moves through the golden grass, the retriever's fur rippling in the breeze. Birds call distantly. The warm afternoon light shifts as clouds drift overhead.

### Strong Single-Shot (Product)

> Close-up product shot of a brushed-steel water bottle on a bone-white marble surface, slow 20-degree camera arc from the left, soft key light from the top-left with a subtle fill, matte-black backdrop, high-end commercial aesthetic, shallow depth of field. A faint ambient hum and the soft clink of the bottle settling on the stone.

### Weak Prompt (Don't Do This)

> A nice cinematic video of a person walking in the city.

**Why it fails**: No shot type, no lighting, no character detail, no camera movement, no audio, "nice" and "cinematic" carry no signal.
