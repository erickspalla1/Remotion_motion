# Composition templates

Pre-built Remotion composition structures for common animation types. Each template is a starting point — customize with brand context and storyboard content.

## Template: Social media ad (Stories 9:16)

Best for: Instagram/TikTok stories, product launches, promotions.

Structure: 4 scenes, 8-15 seconds total.

```
Scene 1 (2s)  — Hook: bold text or striking visual to stop the scroll
Scene 2 (3s)  — Product/message: hero image or key benefit
Scene 3 (2s)  — CTA: "Shop now", "Learn more", swipe-up prompt
Scene 4 (1.5s) — End card: logo + brand signature
```

Animation style: Fast, high-energy. Short springs (damping: 8), quick stagger (3 frames), slide-up entrances. Text should be large (60-80px heading on 1080px wide).

```tsx
// Registration
<Composition
  id="stories-ad"
  component={StoriesAd}
  width={1080}
  height={1920}
  fps={30}
  durationInFrames={255} // 8.5s
  defaultProps={{ brand: defaultBrand }}
  schema={storiesAdSchema}
/>
```

## Template: Social media ad (Feed 1:1)

Best for: Instagram feed posts, Facebook ads.

Structure: 3-5 scenes, 6-15 seconds total.

```
Scene 1 (2s)   — Attention: question, stat, or bold statement
Scene 2 (3-5s) — Value: product grid, feature list, or testimonial
Scene 3 (2s)   — CTA + logo lockup
```

Animation style: Moderate pace. Scale-in for images, fade-slide for text. Background color from brand palette.

```tsx
<Composition
  id="feed-square"
  component={FeedSquare}
  width={1080}
  height={1080}
  fps={30}
  durationInFrames={210} // 7s
/>
```

## Template: Lower third

Best for: Name supers in interviews, event titles, podcast videos.

Structure: Single scene with enter → hold → exit.

```
Enter (0.5s) — Bar slides in from left, text fades in staggered
Hold  (3s)   — Static display
Exit  (0.5s) — Reverse animation
```

```tsx
const LowerThird: React.FC<{
  name: string;
  title: string;
  brand: BrandContext;
}> = ({ name, title, brand }) => {
  const frame = useCurrentFrame();
  const { fps, durationInFrames } = useVideoConfig();

  // Enter
  const enterProgress = spring({ frame, fps, config: { damping: 15 } });
  // Exit (starts 15 frames before end)
  const exitFrame = durationInFrames - 15;
  const exitProgress = frame > exitFrame
    ? interpolate(frame, [exitFrame, durationInFrames], [1, 0], { extrapolateRight: "clamp" })
    : 1;

  const progress = Math.min(enterProgress, exitProgress);

  return (
    <AbsoluteFill style={{ justifyContent: "flex-end", padding: 60 }}>
      {/* Accent bar */}
      <div style={{
        width: interpolate(progress, [0, 1], [0, 400]),
        height: 4,
        backgroundColor: brand.colors.accent,
        marginBottom: 12,
      }} />
      {/* Name */}
      <div style={{
        opacity: progress,
        transform: `translateX(${interpolate(progress, [0, 1], [-30, 0])}px)`,
        fontSize: 36,
        fontWeight: 700,
        color: brand.colors.text,
      }}>
        {name}
      </div>
      {/* Title */}
      <div style={{
        opacity: interpolate(progress, [0, 0.6, 1], [0, 0, 1]),
        fontSize: 22,
        color: brand.colors.secondary,
        marginTop: 4,
      }}>
        {title}
      </div>
    </AbsoluteFill>
  );
};
```

## Template: Logo reveal

Best for: Intro/outro animations, brand stings.

Structure: Single scene, 2-4 seconds.

```
Phase 1 (0.3s) — Accent shape animates in (circle expand or line draw)
Phase 2 (0.5s) — Logo scales in with spring
Phase 3 (0.3s) — Brand name fades in below
Phase 4 (1s)   — Hold
Phase 5 (0.5s) — Optional fade out
```

```tsx
const LogoReveal: React.FC<{ brand: BrandContext }> = ({ brand }) => {
  const frame = useCurrentFrame();
  const { fps } = useVideoConfig();

  // Circle expand behind logo
  const circleScale = spring({ frame, fps, config: { damping: 12, mass: 0.8 } });
  // Logo pop
  const logoScale = spring({ frame: frame - 10, fps, config: { damping: 8, mass: 0.5 } });
  // Brand name
  const nameOpacity = spring({ frame: frame - 25, fps, config: { damping: 20 } });

  return (
    <AbsoluteFill style={{
      backgroundColor: brand.colors.background,
      justifyContent: "center",
      alignItems: "center",
    }}>
      {/* Accent circle */}
      <div style={{
        position: "absolute",
        width: 200,
        height: 200,
        borderRadius: "50%",
        backgroundColor: brand.colors.accent,
        opacity: 0.15,
        transform: `scale(${circleScale * 1.5})`,
      }} />
      {/* Logo */}
      {brand.logo && (
        <Img src={staticFile(brand.logo)} style={{
          width: 180,
          transform: `scale(${logoScale})`,
        }} />
      )}
      {/* Brand name */}
      <div style={{
        position: "absolute",
        bottom: "35%",
        opacity: nameOpacity,
        fontSize: 28,
        fontWeight: 500,
        color: brand.colors.text,
        letterSpacing: 4,
        textTransform: "uppercase",
      }}>
        {brand.name}
      </div>
    </AbsoluteFill>
  );
};
```

## Template: Text showcase (quote / stat / headline)

Best for: Highlighting a single powerful statement, statistic, or quote.

Structure: 3 phases over 4-6 seconds.

```
Phase 1 (1s)   — Background color fills in, decorative element enters
Phase 2 (2-3s) — Main text reveals word-by-word or line-by-line
Phase 3 (1s)   — Source attribution fades in, hold
```

Variations:
- **Stat**: Large number counts up, label below
- **Quote**: Text with quotation marks, author attribution
- **Headline**: Bold heading with accent underline

## Template: Product showcase

Best for: E-commerce, product launches, feature highlights.

Structure: 4 scenes, 10-15 seconds.

```
Scene 1 (2s)  — Product hero image: scale-in or reveal
Scene 2 (4s)  — Feature callouts: staggered badges or text labels appear around product
Scene 3 (2s)  — Price/offer: bold number + offer text
Scene 4 (2s)  — CTA + logo lockup
```

Key patterns:
- Product image uses clip-reveal entrance from center
- Feature callouts use staggered spring-in with 8-frame delay between each
- Price uses number counter animation (interpolate integer values)
- Background: subtle gradient shift matching brand colors

## Template: Countdown / event teaser

Best for: Event announcements, sale countdowns, launch teasers.

Structure: 4-5 rapid scenes, 6-10 seconds.

```
Scene 1 (1.5s) — Date/number slam: "3 DAYS" or "JUNE 15"
Scene 2 (2s)   — Event name reveal
Scene 3 (2s)   — Key details (time, location, or headline act)
Scene 4 (1.5s) — CTA + logo
```

Animation style: High impact. Use scale-slam (spring with very low damping: 4), fast wipes between scenes, accent flash on scene change.

## Template: Slideshow / carousel

Best for: Multi-image presentations, portfolio showcases, before/after.

Structure: N slides with transitions, 2-3 seconds per slide.

```
Each slide:
  Enter (0.5s) — Slide in from right (or fade/zoom)
  Hold  (2s)   — Static with subtle ken-burns (slow zoom)
  Exit  (0.5s) — Transition to next
```

Key patterns:
- Images use `<OffthreadVideo>` or `<Img>` with object-fit: cover
- Ken Burns: slow scale 1 → 1.05 over hold duration
- Caption overlay at bottom with semi-transparent background
- Pagination dots showing current position

## Naming conventions

When generating compositions, use these naming patterns:

| Type | ID pattern | Example |
|---|---|---|
| Social ad | `{brand}-{format}-{campaign}` | `nike-stories-summer24` |
| Lower third | `lower-third-{style}` | `lower-third-minimal` |
| Logo reveal | `{brand}-logo-reveal` | `acme-logo-reveal` |
| Template | `template-{type}` | `template-product-showcase` |
