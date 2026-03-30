# Color

Color is the fastest communicator in design. The audience reads color before they read text, before they understand layout, before they notice typography. Get it wrong and nothing else matters.

## Color decision framework

### Step 1: What must the color communicate?

Map the brief's tone to a color temperature and saturation level:

| Tone | Temperature | Saturation | Lightness |
|---|---|---|---|
| Trustworthy / reliable | Cool (blue-green) | Medium | Medium |
| Energetic / exciting | Warm (red-orange-yellow) | High | High |
| Luxurious / premium | Warm or neutral | Low-medium | Dark |
| Calm / wellness | Cool (blue-green) | Low | Light-medium |
| Playful / fun | Warm or mixed | High | Bright |
| Serious / authoritative | Neutral (dark gray-navy) | Low | Dark |
| Natural / organic | Green-earth tones | Low-medium | Medium |
| Innovative / tech | Blue-purple-cyan | Medium | Medium-dark |
| Provocative / bold | High contrast, any hue | Very high | Extreme (very light or very dark) |
| Minimal / refined | Neutral | Very low | Light |

### Step 2: Build the palette

Every palette needs these roles filled:

- **Primary** — the dominant brand color. Appears on 60% of colored surfaces. Must work on both light and dark backgrounds.
- **Secondary** — supports the primary. Appears on 30% of colored surfaces. Creates contrast or harmony with primary.
- **Accent** — draws attention to CTAs, highlights, interactive elements. Appears on 10% of colored surfaces. Must pop against both primary and secondary.
- **Background** — the canvas. Usually near-white or near-black. Rarely saturated.
- **Text** — must have minimum 4.5:1 contrast ratio against background (WCAG AA).

### Step 3: Choose the palette structure

| Structure | What it is | Best for | Example |
|---|---|---|---|
| Monochromatic | One hue, multiple tints/shades | Elegant, minimal, cohesive | Navy 900 → Navy 100 |
| Analogous | Adjacent hues on the wheel | Harmonious, natural, warm | Blue + Teal + Green |
| Complementary | Opposite hues | High contrast, energetic | Blue + Orange |
| Split complementary | One hue + two adjacent to its complement | Dynamic but controlled | Blue + Red-orange + Yellow-orange |
| Triadic | Three evenly spaced hues | Vibrant, playful, bold | Red + Blue + Yellow |
| Neutral + accent | Grayscale base + one color | Professional, focused | Gray system + Electric blue |

**Default recommendation for most briefs:** Neutral + accent. It is the safest path to looking professional while having visual interest. Use it unless the brief explicitly calls for more color.

## Color by industry

These are conventions the audience already expects. Respect or deliberately break them — but never accidentally ignore them.

| Industry | Expected colors | Why | How to differentiate |
|---|---|---|---|
| Finance / fintech | Blue, navy, dark green | Trust, stability, money | Use warm accent (gold, coral) or unexpected blue (electric, not corporate) |
| Health / wellness | Green, teal, soft blue, white | Nature, calm, cleanliness | Use deeper tones (forest green vs mint) or add warm neutral |
| Food / restaurant | Red, orange, yellow, brown | Appetite, warmth, comfort | Go moodier (wine red, burnt orange) or minimal (black + one food color) |
| Tech / SaaS | Blue, purple, gradient | Innovation, digital | Use non-gradient flat colors, or unexpected hue (green tech, warm tech) |
| Fashion / luxury | Black, white, gold, nude | Sophistication, exclusivity | Surprise with saturated jewel tones or stark neon |
| Education | Blue, green, orange | Trust, growth, energy | Warmer palette, illustration-led color |
| Entertainment | Any — high saturation, high contrast | Excitement, engagement | Match the specific genre's visual language |
| Real estate | Blue, green, brown, white | Trust, nature, home | Warmer neutrals, architectural gray palette |

## Functional color system

Beyond brand colors, every project needs functional colors:

| Role | Recommended | Usage |
|---|---|---|
| Success | Green (#22C55E family) | Confirmations, positive metrics |
| Warning | Amber (#F59E0B family) | Alerts, attention needed |
| Error | Red (#EF4444 family) | Errors, destructive actions |
| Info | Blue (#3B82F6 family) | Informational, neutral status |
| Disabled | Gray at 40% opacity | Inactive elements |

These should be separate from brand colors. A brand's primary red should never also be the error color — it creates confusion.

## Color contrast and accessibility

Non-negotiable rules:

- **Body text on background:** minimum 4.5:1 contrast ratio (WCAG AA)
- **Large text (24px+ or 18px bold):** minimum 3:1
- **UI components and focus indicators:** minimum 3:1 against adjacent color
- **Never rely on color alone** to communicate information — always pair with shape, icon, or text

Quick reference for common combinations:

| Text | Background | Ratio | Passes? |
|---|---|---|---|
| #000000 | #FFFFFF | 21:1 | Yes (AAA) |
| #333333 | #FFFFFF | 12.6:1 | Yes (AAA) |
| #666666 | #FFFFFF | 5.7:1 | Yes (AA) |
| #999999 | #FFFFFF | 2.8:1 | No |
| #FFFFFF | #3B82F6 | 4.6:1 | Yes (AA) |
| #FFFFFF | #EF4444 | 4.0:1 | Borderline — test |

## Palette generation from a single brand color

When the user provides one brand color, expand to a full system:

1. **Primary** = the given color
2. **Primary dark** = shift hue -5°, reduce lightness -20%
3. **Primary light** = shift hue +5°, increase lightness +30%, reduce saturation -15%
4. **Secondary** = analogous hue (+30° or -30° on the color wheel)
5. **Accent** = complementary hue (+180°) with adjusted saturation
6. **Neutral dark** = desaturate primary to ~5% saturation, lightness 15%
7. **Neutral light** = desaturate primary to ~3% saturation, lightness 95%

This guarantees the palette feels cohesive because every color is mathematically related to the primary.

## Color in motion

Specific guidance for animated content:

- **Background color transitions** should be slow (0.8-1.5s) and use analogous colors — jumping between complementary colors feels jarring in motion
- **Text color should never animate** — it is disorienting. Change text color by replacing text elements, not transitioning the color property
- **Accent color flash** (1-3 frames of a bright accent on scene change) adds energy to fast-paced motion
- **Gradient animations** work best rotating the angle, not changing the colors
- **Dark-to-light transitions** feel like "opening up" or "revealing" — use for positive moments
- **Light-to-dark transitions** feel like "closing" or "intensifying" — use for dramatic moments
