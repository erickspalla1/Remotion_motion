# Typography

Typography is the single most impactful design decision. A wrong typeface undermines everything else; the right one carries the entire piece.

## Type selection framework

Never pick a font because it "looks nice." Pick it because it communicates the right thing to the right audience. Every typeface has a voice — match that voice to the brief.

### Typeface personality map

| Category | Communicates | Use when brief says | Avoid when |
|---|---|---|---|
| Geometric sans (Futura, Montserrat, Poppins) | Modern, clean, accessible | "friendly tech", "startup", "approachable" | Luxury, editorial, gravitas |
| Grotesque sans (Helvetica, Arial, Akzidenz) | Neutral, institutional, reliable | "corporate", "no-nonsense", "trusted" | Personality, warmth, creativity |
| Neo-grotesque (Inter, SF Pro, Albert Sans) | Contemporary, functional, UI | "digital product", "tech platform" | Print editorial, luxury, craft |
| Humanist sans (Gill Sans, Frutiger, Source Sans) | Warm, readable, approachable | "healthcare", "education", "government" | Edgy, fashion, youth |
| Display sans (Clash Display, Space Grotesk, General Sans) | Bold, contemporary, standout | "brand launch", "campaign hero", "impact" | Body text, long-form, subtle |
| Old-style serif (Garamond, Caslon, Minion) | Classical, literary, trustworthy | "publishing", "law", "heritage brand" | Tech, youth, speed |
| Transitional serif (Baskerville, Times, Georgia) | Authoritative, balanced, formal | "news", "academia", "established institution" | Casual, playful, startup |
| Modern serif (Didot, Bodoni, Playfair) | Luxurious, high-contrast, editorial | "fashion", "luxury", "magazine" | Friendly, casual, tech |
| Slab serif (Rockwell, Roboto Slab, Clarendon) | Strong, grounded, confident | "construction", "sports", "bold statement" | Delicate, ethereal, light |
| Humanist serif (Freight Text, Merriweather, Lora) | Warm, readable, contemporary | "long-form reading", "warm editorial" | Corporate, impact, minimal |
| Monospace (JetBrains Mono, Fira Code, IBM Plex Mono) | Technical, precise, code | "developer tools", "data", "brutalist design" | Luxury, warmth, mainstream |
| Script/handwritten (Caveat, Dancing Script) | Personal, casual, human | "wedding", "café", "handmade brand" | Corporate, tech, serious |

### Type pairing rules

A type pairing works when the two fonts have contrast but share structure.

**Contrast means:** different category (serif + sans), different weight (bold heading + light body), different personality (display + text).

**Shared structure means:** similar x-height, similar proportions, similar stroke width in the regular weight.

**Reliable pairing patterns:**

1. **Display serif + geometric sans** — Playfair Display + Montserrat. Classic luxury + accessible body.
2. **Bold grotesque + humanist serif** — Clash Display + Freight Text. Impact heading + warm reading.
3. **Geometric sans + humanist sans** — Futura + Source Sans. Two sans-serifs that work because geometric carries headlines while humanist carries text.
4. **Modern serif + neo-grotesque** — Instrument Serif + Inter. Editorial elegance + functional body.
5. **Mono + geometric sans** — JetBrains Mono + Albert Sans. Technical edge + clean structure.

**Pairing failures (avoid):**
- Two display fonts (both compete for attention)
- Two very similar sans-serifs (no contrast, looks like a mistake)
- Script + script (illegible chaos)
- Overly decorative heading + overly decorative body (visual noise)

### Font size hierarchy

Establish clear levels. On a 1080px wide canvas:

| Level | Purpose | Size range | Weight |
|---|---|---|---|
| H1 | Hero headline | 64-96px | Bold (700) or Black (900) |
| H2 | Section heading | 36-48px | Semibold (600) or Bold (700) |
| H3 | Subheading | 24-32px | Medium (500) or Semibold (600) |
| Body | Reading text | 16-20px | Regular (400) |
| Caption | Supporting info | 12-14px | Regular (400) or Light (300) |
| Overline | Category label | 11-13px | Medium (500), uppercase, tracked |

Scale proportionally for different canvas sizes. On 1920px wide: multiply by ~1.5. On 1080x1920 stories: heading can be 72-120px because of the tall format.

### Tracking (letter-spacing)

- **Headlines large (48px+):** tighten to -0.02em to -0.04em. Large type has too much natural spacing.
- **Body text:** leave at default (0). Trust the type designer.
- **Overlines and labels in uppercase:** widen to 0.05em to 0.15em. Uppercase text needs breathing room.
- **Script fonts:** never alter tracking. It breaks connected letterforms.

### Line height

- **Headlines:** 1.0 to 1.15 — tight. Headlines should feel like a block, not lines.
- **Body text:** 1.5 to 1.7 — comfortable. Readability over density.
- **Captions:** 1.3 to 1.5.
- **Single-line labels:** 1.0.

## Google Fonts recommendations by mood

For web and Remotion (free, easily loadable):

**Modern luxury:** Instrument Serif (heading) + Albert Sans (body)
**Clean tech:** Space Grotesk (heading) + Inter (body)
**Warm editorial:** Fraunces (heading) + Source Serif 4 (body)
**Bold impact:** Clash Display (heading) + General Sans (body)
**Friendly startup:** Outfit (heading) + DM Sans (body)
**Minimal elegance:** Cormorant Garamond (heading) + Karla (body)
**Creative agency:** Syne (heading) + Work Sans (body)
**Corporate trust:** IBM Plex Sans (heading) + IBM Plex Serif (body)
**Playful brand:** Bricolage Grotesque (heading) + Nunito (body)
**News/authority:** Newsreader (heading) + Roboto (body)
