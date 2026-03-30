# Motion direction

Motion direction is not animation — it is the art direction of time. A motion director decides what moves, when, how fast, with what energy, and why. The animation is the execution; the direction is the intent.

## Motion personality

Every brand and every piece has a motion personality. Define it before animating anything.

| Motion personality | Speed | Amplitude | Easing | Stagger | Feel |
|---|---|---|---|---|---|
| Precise | Medium | Small (5-15px) | Ease-out | Tight (3-4 frames) | Apple, Stripe |
| Energetic | Fast | Large (30-60px) | Spring (low damping) | Quick (2-3 frames) | Nike, Spotify |
| Elegant | Slow | Very small (3-8px) | Cubic-bezier, long ease | Generous (10-15 frames) | Chanel, Aesop |
| Playful | Medium-fast | Large with overshoot | Bounce / spring | Irregular | Slack, Mailchimp |
| Dramatic | Very slow | Large | Ease-in (slow start) | Very long (20+ frames) | Cinematic, trailer |
| Minimal | Slow | Tiny (2-5px) | Linear or slight ease | No stagger (simultaneous) | Muji, COS |
| Technical | Medium | Small | Linear | Mechanical (even) | IBM, data tools |

## The three laws of motion direction

### Law 1: One thing moves at a time

The viewer's eye can only track one movement. When everything moves simultaneously, nothing has impact. Stagger entrances so each element has its moment.

Exception: background shifts and ambient motion (particles, gradients) can happen during element entrances because they are environmental, not focal.

### Law 2: The most important element gets the best entrance

Do not waste a dramatic spring-in on a caption. The hero element (main message, product, logo) gets the most carefully crafted animation. Supporting elements get simpler treatments (fade, basic slide).

Hierarchy of animation impact:
1. Scale from 0 → spring pop (highest impact)
2. Slide-in from off-screen → spring settle (high)
3. Clip-reveal / mask wipe (high, cinematic)
4. Fade + slight translate (medium)
5. Simple fade (low impact, for supporting elements)
6. Cut / instant appear (lowest, for background or grid elements)

### Law 3: Motion has rhythm

Like music, animation needs rhythm: moments of action and moments of rest.

Structure a 10-second animation like a sentence:
- Beat 1 (0-2s): Opening — establish the world (background, tone)
- Beat 2 (2-5s): Build — introduce elements progressively
- Beat 3 (5-7s): Climax — the key message lands with the strongest animation
- Beat 4 (7-9s): Resolve — CTA, supporting info
- Beat 5 (9-10s): Close — end card, logo

Never have continuous movement from start to end. Hold moments (0.5-1.5s of stillness) between beats let the viewer absorb what they have seen.

## Transition philosophy

Transitions are not decorative — they communicate the relationship between scenes.

| Transition | Communicates | Use between |
|---|---|---|
| Cut (instant) | New topic, new energy, interruption | Unrelated scenes, high-energy montage |
| Fade | Passage of time, softness, ending | Related scenes, emotional moments, closing |
| Slide | Progression, continuation, sequence | Sequential steps, carousel, spatial relationship |
| Wipe | Dramatic reveal, before/after | Reveals, comparisons, dramatic moments |
| Zoom | Focus change, entering a world | Overview → detail, establishing → intimate |
| Morph | Transformation, evolution | Same element changing state, brand evolution |

**Default rule:** when in doubt, use a fade of 10-15 frames. It is the safest transition and never looks wrong.

**Never:** use 3D rotating cube transitions, star wipes, or any transition that calls attention to itself rather than the content. The transition serves the story, not the other way around.

## Stagger patterns

Stagger is the delay between multiple elements entering. It creates rhythm and directs the reading order.

| Pattern | Description | Use for |
|---|---|---|
| Top-to-bottom | First element enters, then each below | Text paragraphs, vertical lists |
| Left-to-right | Elements enter from left side first | Horizontal sequences, timelines |
| Center-out | Center element first, then outward | Symmetric layouts, logos with text |
| Random | Slightly randomized delays | Particle-like, organic, casual |
| Cascade | Each triggers the next (domino) | Grid items, gallery, card layouts |

**Timing:** the delay between elements should be 3-8 frames (100-270ms at 30fps). Less than 3 frames feels simultaneous. More than 10 frames feels sluggish.

## Pacing by content type

| Content type | Total duration | Scenes | Transition speed | Hold time |
|---|---|---|---|---|
| Stories ad | 6-15s | 3-5 | Fast (0.3s) | 1-2s |
| Feed post | 5-10s | 2-4 | Medium (0.5s) | 1.5-2.5s |
| Logo sting | 2-4s | 1-2 | Medium (0.5s) | 1-1.5s |
| Product showcase | 10-20s | 4-6 | Medium (0.5s) | 2-3s |
| Explainer | 30-60s | 8-15 | Slow (0.7s) | 2-4s |
| Title sequence | 10-30s | 3-8 | Slow (0.7-1s) | 1.5-3s |
| End card | 2-3s | 1 | Medium (0.5s) | 1.5-2s |

## Color in motion

How color behaves over time is a direction decision:

- **Consistent palette throughout** — cohesive, brand-safe. Default choice.
- **Color progression** (warm → cool or light → dark) — creates narrative arc. "Journey" feeling.
- **Scene-based color** — each scene has a dominant color. Creates rhythm. Best for product showcases with multiple items.
- **Accent flash** — 1-3 frames of the accent color between scenes. Adds punch. Best for energetic content.

## Sound-to-motion sync

When the animation has music or sound:

- **Beat sync** — key visual moments land on musical beats. The most impactful technique.
- **Anticipation** — start the animation 2-3 frames before the beat. It creates a feeling of the visuals driving the music.
- **Texture match** — quiet music = subtle motion. Loud music = bold motion. Match the energy curve.

## Quality checklist for motion

Before finalizing any animation, verify:

1. Can you identify the three hierarchy levels while it plays?
2. Does every element have a clear entrance? No element should "just be there" from frame 1 unless it is the background.
3. Are there rest moments (holds) between action beats?
4. Does the most important message get the most impactful animation?
5. Is the transition style consistent throughout? (Do not mix wipes and fades randomly)
6. At 1x speed, can you read all text comfortably?
7. Does the last frame work as a standalone static image?
8. Is the animation under the target duration?
