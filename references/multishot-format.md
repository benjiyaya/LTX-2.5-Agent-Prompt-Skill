# Multi-Shot Format (LTX 2.5 — NEW)

## When to Use

- User requests multiple cuts, angles, or scene transitions
- Sequences that need establish → detail → reaction progression
- Stories spanning multiple locations or time jumps
- Any scene where a single continuous take can't cover the narrative

## What's New in LTX 2.5

Previous LTX versions produced a single continuous shot. LTX 2.5 can generate **multi-shot scenes**: several distinct shots joined by explicit cuts inside one prompt. Character identity, environment, lighting, and voice hold across cuts.

## Output Format

One chronological paragraph. NOT a shot list. NOT numbered beats. Flowing prose with named transitions woven naturally between shot segments.

## Critical Rules

### DO:
- Write as **one chronological paragraph**
- **Name every transition** in natural language: "A hard cut transitions to...", "A match cut connects...", "The image dissolves into...", "Another hard cut jumps to..."
- **Re-establish framing at every cut**: shot scale, camera angle, who/what is in frame
- **Re-identify characters** when they reappear: "the woman in the red coat, earlier at the table, now..."
- **State audio continuity** at every cut: "the synth score continues across the cut" or "the music drops; only wind remains"
- Keep to **2–4 shots** per generation
- Give each shot a **clear job**: establish → detail → reaction, or wide → medium → close-up
- Keep action **chronological**: "Initially...", "A moment later...", "Simultaneously..."

### DON'T:
- Use `Shot 1:`, `Shot 2:` or any list format
- Use numbered beats
- Use screenplay sluglines (unless using screenplay-style mode)
- Include more than 4 shots — clarity drops sharply
- Change geography or costumes between cuts without explaining the time/place jump

## What to Include at Every Cut

| Element | Requirement |
|---|---|
| **Transition name** | "A hard cut transitions to..." / "A match cut connects..." / "The image dissolves into..." |
| **New framing** | Shot scale + camera angle for the new shot |
| **Subject re-identification** | Who is in frame, using consistent visual descriptors |
| **Audio continuity** | Does music/dialogue/ambience continue or change? |
| **Lighting** | State if it changed (or explicitly note it continues) |

## Transition Vocabulary

- **Hard cut** — abrupt transition, most common. "A hard cut transitions to..."
- **Match cut** — connects two visually similar compositions. "A match cut connects..."
- **Dissolve** — gradual blend. "The image dissolves into..."
- **Jump cut** — temporal jump within same framing. "A jump cut leaps to..."
- **Fade** — fade through black/white. "The scene fades to black, then reveals..."

## Audio Continuity Patterns

- "The piano score continues across the cut, traffic muffled."
- "The dialogue drops; only wind remains."
- "The synth music persists, but the ambience shifts to room tone."
- "The music swells as the cut lands, then settles."

## Shot Budget

| Shot Count | Best For | Risk |
|---|---|---|
| 2 shots | Establish + reveal, wide + close-up | Low risk, very reliable |
| 3 shots | Classic sequence (wide → medium → close) | Moderate, good results |
| 4 shots | Full mini-narrative | Higher risk, shorter beats per shot |
| 5+ shots | Not recommended | Clarity drops sharply |

## When to Stay Single-Shot

Use a single continuous take when:
- You want unbroken camera motion
- Intimate performance or dialogue with lip-sync
- I2V from a first frame (unless you intentionally cut away from the opening image)
- The action is simple enough to capture in one take

## Full Example

> A wide shot frames a rainy city intersection at dusk, neon signs reflecting on wet asphalt. A young woman in a yellow raincoat walks toward camera, gripping a folded newspaper, while cars hiss past behind her. Soft synth music and distant traffic fill the air. A hard cut transitions to a medium close-up of her face under the hood, raindrops catching the neon as she looks off-screen left; the synth score continues across the cut, traffic muffled. She whispers, "He's late." Another hard cut jumps to a low-angle shot of a man's scuffed boots stepping into a puddle at the curb; the music drops to a low drone. He lifts his head into frame — short dark hair, soaked jacket — and smiles toward her off-screen as a bus rumbles past.

## Element Breakdown of Example

| Element | Shot 1 (Wide) | Shot 2 (MCU) | Shot 3 (Low-angle) |
|---|---|---|---|
| **Transition** | Opening | "A hard cut transitions to" | "Another hard cut jumps to" |
| **Framing** | Wide, intersection | Medium close-up, face | Low-angle, boots then face |
| **Character** | Woman in yellow raincoat | Same woman, under hood | Man: dark hair, soaked jacket |
| **Action** | Walks toward camera | Looks off-screen left | Steps into puddle, smiles |
| **Camera** | Static/implicit | Implicit handheld | Low-angle framing |
| **Audio** | Synth + traffic | Score continues, traffic muffled | Music drops to drone, bus rumbles |
| **Dialogue** | — | "He's late." | — |
