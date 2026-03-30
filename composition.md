# Composition

Composition is how you control where the viewer looks and in what order. A good composition is invisible — the eye flows naturally. A bad composition makes the viewer work to find the message.

## Visual hierarchy

The audience scans in a predictable order based on visual weight. Elements with more weight get seen first.

Weight factors (from highest to lowest impact):
1. **Size** — larger elements dominate
2. **Contrast** — high contrast against background draws the eye
3. **Color saturation** — vivid colors pop against muted surroundings
4. **Position** — top-left and center get seen first in Western reading cultures
5. **Isolation** — an element with space around it commands attention
6. **Motion** — in video, the moving element wins over static ones every time

### Establishing hierarchy in 3 levels

Every piece needs exactly three levels of hierarchy. Not two (flat), not four (confusing). Three.

| Level | What it is | Visual treatment |
|---|---|---|
| Primary | The one thing you must see | Largest, boldest, most contrasted, most space |
| Secondary | Context that supports the primary | Medium size, visible but not competing |
| Tertiary | Details for those who keep looking | Small, low contrast, tucked away |

**Test:** squint at the design. If all three levels are still distinguishable when blurred, the hierarchy works.

## Grid systems

### Column grid

The workhorse of layout. Divide the canvas into vertical columns with gutters.

| Canvas width | Columns | Gutter | Margin | Use case |
|---|---|---|---|---|
| 1080px (social) | 4-6 | 16-24px | 40-60px | Feed posts, stories |
| 1920px (landscape) | 8-12 | 24-32px | 60-80px | Presentations, web |
| 1080x1920 (stories) | 4 | 16px | 40px | Vertical content |

**Rule:** content aligns to column edges. Nothing floats between columns unless it is deliberately breaking the grid for emphasis.

### Modular grid

Columns + rows create a grid of modules. Best for:
- Multi-image layouts
- Data-dense content
- Product grids
- Storyboard frames

### Baseline grid

Invisible horizontal lines at regular intervals (usually matching line-height). All text baselines and element edges snap to this grid. Creates vertical rhythm.

Set the baseline to 8px for digital, 4px for dense UI. Every margin, padding, and spacing value should be a multiple of the baseline unit.

### Rule of thirds

Divide the canvas into a 3x3 grid. Place key elements at the intersections or along the lines. Works for:
- Photography crops
- Single-element compositions
- Video framing

The four intersection points are called "power points" — the most naturally attention-grabbing positions on the canvas.

### Breaking the grid

A grid that is never broken feels rigid and lifeless. One deliberate break creates a focal point.

When to break:
- **Hero element** that must dominate — let it span multiple columns or extend past margins
- **Pull quotes** in editorial — offset them from the text column
- **CTAs** — slightly larger or offset from the grid to draw action
- **Accent graphics** — decorative elements that overlap grid boundaries add dynamism

When NOT to break:
- Body text — always on-grid
- Navigation elements — always on-grid
- Multiple elements at once — one break is a focal point, three breaks is chaos

## Composition patterns

### Z-pattern (scanning)

The eye naturally follows a Z path on a page: top-left → top-right → bottom-left → bottom-right. Place elements along this path.

Best for: landing pages, ads with multiple elements, pages with a single CTA.

```
[Logo]                    [Navigation]
          
          [Hero Image/Text]

[Supporting text]         [CTA Button]
```

### F-pattern (reading)

For text-heavy content, the eye scans in an F: across the top, then partway across the middle, then down the left edge.

Best for: content pages, email layouts, list-based content.

### Center-dominant

One element in the dead center, everything else orbiting. The simplest and most impactful composition.

Best for: logo reveals, single-statement ads, minimal designs, end cards.

### Diagonal

Strong diagonal line creates energy and movement. Elements placed along a diagonal feel dynamic even when static.

Best for: sports, action, energy, youth brands. Avoid for: corporate, calm, luxury.

### Asymmetric balance

Instead of mirroring left and right, balance a large element on one side with a small but heavy (dark, saturated, or isolated) element on the other.

Best for: editorial, modern design, sophisticated layouts. This is the signature of confident design — it looks effortless but requires precision.

## Negative space

Negative space (whitespace) is not "empty" — it is an active design element. It creates:

- **Focus** — space around an element makes it more important
- **Breathing room** — prevents visual fatigue
- **Sophistication** — generous spacing signals confidence and quality
- **Hierarchy** — more space around primary elements, less around tertiary

**Budget rule:** at least 40% of the total canvas should be negative space. For luxury brands, aim for 50-60%. For high-energy ads, 30% is acceptable but not less.

## Composition for motion

In animated content, composition changes over time. Plan the composition for each state:

1. **Start state** — what does the first frame look like? Usually minimal (background only, or logo only)
2. **Build state** — elements enter one by one, each finding its position in the grid
3. **Full state** — all elements present, the complete composition. This is the moment that must work as a still frame — if you screenshotted it, would it be a good static ad?
4. **Exit state** — elements leave, usually simplified to end card (logo + CTA)

**Motion hierarchy rule:** the most important element enters LAST. The eye remembers the most recent arrival. Build suspense by revealing supporting elements first, then the hero.

Exception: if the hero is a dramatic reveal (logo sting, product shot), it can enter first and everything else supports it.

## Aspect ratio composition guides

### 9:16 (stories / vertical video)

The tall format is read top-to-bottom. Place the hook in the top third (it is what shows in the feed preview). CTA goes in the bottom third (thumb reach zone).

Keep text in the center 60% of the width — edges get clipped on some devices. Avoid placing critical elements in the top 80px (status bar) or bottom 100px (swipe-up zone).

### 1:1 (feed square)

The most constrained format. Center-dominant compositions work best. Avoid complex grids — there is not enough room.

Text should be bold and minimal. If the message needs more than 8 words, the text is too long for this format.

### 16:9 (landscape / web)

The most spacious format. Use asymmetric compositions with a clear left or right focal point. Generous horizontal margins (80-120px at 1920px wide).

### 4:5 (feed portrait)

A compromise between square and stories. Use the extra vertical space for a headline above or CTA below the main visual. The center area behaves like a square.
