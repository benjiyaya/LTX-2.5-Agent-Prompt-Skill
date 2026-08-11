# Screenplay-Style Format (LTX 2.5)

## When to Use

- Dialogue-heavy scenes with multiple speaking characters
- Scenes requiring precise timing, pauses, and emotional beats
- Narrative scenes with acting direction more complex than a single paragraph can convey
- When the user provides a script or screenplay excerpt

## When NOT to Use

- Simple action scenes (use single-shot)
- Multi-cut sequences without dialogue (use multishot)
- Quick product shots (use single-shot)

## Output Format

A screenplay-formatted scene. Uses scene headers, character cues, and quoted dialogue — but still follows the 6-part prompt structure within the prose.

## Structure

```
INT./EXT. LOCATION – TIME

[Visual description: shot type, scene/lighting, character introduction. 2-3 sentences setting the stage.]

[Action description with camera movement. Present tense.]

CHARACTER NAME
(physical acting direction)
"Dialogue in quotation marks."

[Camera note or transition]

[Audio description: ambient, music, sound effects.]
```

## Rules

- **Scene header**: `INT. COFFEE SHOP – AFTERNOON` or `EXT. CITY STREET – NIGHT`
- **Present tense** for all action and movement
- **Physical acting directions** in parentheses under character name — NOT emotional labels
- **Dialogue in quotation marks** — preserve the user's exact words
- **Break long dialogue** into shorter phrases with acting directions between them
- **One dominant action** between dialogue beats
- **Camera notes** woven naturally: "The camera slowly zooms into his face."
- **Audio description** at the end or woven throughout
- **No numbered shots** — this is a continuous scene, not a shot list

## Dialogue Formatting

Break long speeches into segments with physical acting directions between them:

**Good:**
> A middle-aged man with greying hair speaks in a slow-paced voice, "I remember after you kids came along..." He pauses and looks to the side, then continues, "your mom..." His eyes widen momentarily. He finishes with a cracking voice, "said something to me I never quite understood."

**Bad:**
> A sad man says: "I remember after you kids came along, your mom said something to me I never quite understood."

**Why bad**: "Sad" is an emotional label the model can't render. No physical cues. No pauses or beats. One long undifferentiated speech.

## Full Example

> EXT. SMALL TOWN STREET – MORNING – LIVE NEWS BROADCAST
>
> The shot opens on a news reporter standing in front of a row of cordoned-off cars, yellow caution tape fluttering behind him. The light is warm, early sun reflecting off the camera lens. The faint hum of chatter and distant drilling fills the air. The reporter, composed but visibly excited, looks directly into the camera, microphone in hand.
>
> REPORTER (live, composed but grinning)
> "Thank you, Sylvia. And yes — this is a sentence I never thought I'd say on live television — but this morning, here in the quiet town of New Castle, Vermont... black gold has been found!"
>
> He gestures slightly toward the field behind him.
>
> REPORTER (grinning, turning)
> "If my cameraman can pan over, you'll see what all the excitement's about."
>
> The camera pans right, slowly revealing a construction site surrounded by workers in hard hats. A beat of silence — then, with a sudden roar, a geyser of oil erupts from the ground, blasting upward in a violent plume. Workers cheer and scramble, the black stream glistening in the morning light. The camera shakes slightly, trying to stay focused through the chaos.
>
> REPORTER (off-screen, shouting over the noise)
> "There it is, folks — the moment New Castle will never forget!"
>
> The camera catches the sunlight gleaming off the oil mist before pulling back, revealing the entire scene — the small-town skyline silhouetted against the wild fountain of oil. The sounds of cheering, the oil geyser's roar, and distant sirens blend together.

## Element Checklist for Screenplay Style

- [ ] Scene header with INT./EXT., location, time of day
- [ ] Visual description opens with shot type and lighting
- [ ] Character introduced with physical specifics (age, hair, clothing)
- [ ] Dialogue broken into segments with physical acting directions
- [ ] Emotion expressed through physical cues ("eyes widen," "voice cracking")
- [ ] Camera movement described at natural transitions
- [ ] Audio described (ambient, action sounds, music)
- [ ] Present tense throughout
- [ ] No abstract emotional labels ("sad," "confused," "angry")
- [ ] Dialogue preserved verbatim from user input
