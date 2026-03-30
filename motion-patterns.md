# Motion patterns library

Pre-built animation patterns for Remotion. Each pattern is a self-contained code snippet ready to use in compositions.

## Text entrances

### Fade + slide up (most versatile)

```tsx
const FadeSlideUp: React.FC<{ text: string; delay?: number }> = ({ text, delay = 0 }) => {
  const frame = useCurrentFrame();
  const { fps } = useVideoConfig();
  const progress = spring({ frame: frame - delay, fps, config: { damping: 15, mass: 0.8 } });
  return (
    <div style={{
      opacity: progress,
      transform: `translateY(${interpolate(progress, [0, 1], [30, 0])}px)`,
    }}>
      {text}
    </div>
  );
};
```

### Typewriter

```tsx
const Typewriter: React.FC<{ text: string; startFrame?: number }> = ({ text, startFrame = 0 }) => {
  const frame = useCurrentFrame();
  const { fps } = useVideoConfig();
  const charsPerSecond = 30;
  const elapsed = Math.max(0, frame - startFrame);
  const charsToShow = Math.floor((elapsed / fps) * charsPerSecond);
  return (
    <span>
      {text.slice(0, charsToShow)}
      {charsToShow < text.length && (
        <span style={{ opacity: frame % 15 < 8 ? 1 : 0 }}>|</span>
      )}
    </span>
  );
};
```

### Word-by-word reveal with stagger

```tsx
const WordReveal: React.FC<{ text: string; staggerFrames?: number }> = ({ text, staggerFrames = 5 }) => {
  const frame = useCurrentFrame();
  const { fps } = useVideoConfig();
  const words = text.split(" ");
  return (
    <div style={{ display: "flex", flexWrap: "wrap", gap: "0.3em" }}>
      {words.map((word, i) => {
        const wordDelay = i * staggerFrames;
        const progress = spring({
          frame: frame - wordDelay,
          fps,
          config: { damping: 12, mass: 0.5 },
        });
        return (
          <span key={i} style={{
            opacity: progress,
            transform: `translateY(${interpolate(progress, [0, 1], [20, 0])}px)`,
            display: "inline-block",
          }}>
            {word}
          </span>
        );
      })}
    </div>
  );
};
```

### Character stagger (letter by letter)

```tsx
const CharStagger: React.FC<{ text: string; staggerFrames?: number }> = ({ text, staggerFrames = 2 }) => {
  const frame = useCurrentFrame();
  const { fps } = useVideoConfig();
  return (
    <div style={{ display: "flex" }}>
      {text.split("").map((char, i) => {
        const charProgress = spring({
          frame: frame - i * staggerFrames,
          fps,
          config: { damping: 10, mass: 0.4 },
        });
        return (
          <span key={i} style={{
            opacity: charProgress,
            transform: `translateY(${interpolate(charProgress, [0, 1], [15, 0])}px)`,
            display: "inline-block",
            whiteSpace: "pre",
          }}>
            {char}
          </span>
        );
      })}
    </div>
  );
};
```

### Line-by-line reveal (for paragraphs)

```tsx
const LineReveal: React.FC<{ lines: string[]; staggerFrames?: number }> = ({ lines, staggerFrames = 10 }) => {
  const frame = useCurrentFrame();
  const { fps } = useVideoConfig();
  return (
    <div>
      {lines.map((line, i) => {
        const progress = spring({
          frame: frame - i * staggerFrames,
          fps,
          config: { damping: 14, mass: 0.8 },
        });
        return (
          <div key={i} style={{
            opacity: progress,
            transform: `translateX(${interpolate(progress, [0, 1], [-40, 0])}px)`,
          }}>
            {line}
          </div>
        );
      })}
    </div>
  );
};
```

## Logo and image entrances

### Scale pop (spring)

```tsx
const ScalePop: React.FC<{ children: React.ReactNode; delay?: number }> = ({ children, delay = 0 }) => {
  const frame = useCurrentFrame();
  const { fps } = useVideoConfig();
  const scale = spring({ frame: frame - delay, fps, config: { damping: 8, mass: 0.5, stiffness: 200 } });
  return (
    <div style={{ transform: `scale(${scale})`, transformOrigin: "center" }}>
      {children}
    </div>
  );
};
```

### Clip reveal (mask wipe)

```tsx
const ClipReveal: React.FC<{
  children: React.ReactNode;
  direction?: "left" | "right" | "up" | "down";
  delay?: number;
}> = ({ children, direction = "left", delay = 0 }) => {
  const frame = useCurrentFrame();
  const { fps } = useVideoConfig();
  const progress = spring({ frame: frame - delay, fps, config: { damping: 15, mass: 1 } });

  const clipPaths = {
    left: `inset(0 ${interpolate(progress, [0, 1], [100, 0])}% 0 0)`,
    right: `inset(0 0 0 ${interpolate(progress, [0, 1], [100, 0])}%)`,
    up: `inset(0 0 ${interpolate(progress, [0, 1], [100, 0])}% 0)`,
    down: `inset(${interpolate(progress, [0, 1], [100, 0])}% 0 0 0)`,
  };

  return (
    <div style={{ clipPath: clipPaths[direction] }}>
      {children}
    </div>
  );
};
```

### Rotate reveal (3D flip in)

```tsx
const RotateReveal: React.FC<{ children: React.ReactNode; delay?: number }> = ({ children, delay = 0 }) => {
  const frame = useCurrentFrame();
  const { fps } = useVideoConfig();
  const progress = spring({ frame: frame - delay, fps, config: { damping: 12, mass: 1 } });
  return (
    <div style={{
      perspective: 1000,
      transformStyle: "preserve-3d",
    }}>
      <div style={{
        opacity: progress,
        transform: `rotateY(${interpolate(progress, [0, 1], [-90, 0])}deg)`,
        transformOrigin: "left center",
      }}>
        {children}
      </div>
    </div>
  );
};
```

## Background effects

### Gradient shift (animated background)

```tsx
const GradientShift: React.FC<{ color1: string; color2: string }> = ({ color1, color2 }) => {
  const frame = useCurrentFrame();
  const { durationInFrames } = useVideoConfig();
  const angle = interpolate(frame, [0, durationInFrames], [0, 360]);
  return (
    <AbsoluteFill style={{
      background: `linear-gradient(${angle}deg, ${color1}, ${color2})`,
    }} />
  );
};
```

### Particle field (floating dots)

```tsx
const ParticleField: React.FC<{ count?: number; color?: string }> = ({ count = 30, color = "rgba(255,255,255,0.3)" }) => {
  const frame = useCurrentFrame();
  const particles = useMemo(() =>
    Array.from({ length: count }, (_, i) => ({
      x: (i * 137.5) % 100,
      y: (i * 73.3) % 100,
      size: 2 + (i % 4),
      speed: 0.2 + (i % 5) * 0.1,
      phase: i * 0.5,
    })), [count]);

  return (
    <AbsoluteFill>
      {particles.map((p, i) => (
        <div key={i} style={{
          position: "absolute",
          left: `${p.x}%`,
          top: `${(p.y + frame * p.speed) % 110 - 5}%`,
          width: p.size,
          height: p.size,
          borderRadius: "50%",
          backgroundColor: color,
          opacity: 0.3 + 0.3 * Math.sin(frame * 0.05 + p.phase),
        }} />
      ))}
    </AbsoluteFill>
  );
};
```

### Noise texture overlay

```tsx
const NoiseOverlay: React.FC<{ opacity?: number }> = ({ opacity = 0.04 }) => {
  return (
    <AbsoluteFill style={{
      backgroundImage: `url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='1'/%3E%3C/svg%3E")`,
      opacity,
      mixBlendMode: "overlay",
      pointerEvents: "none",
    }} />
  );
};
```

## Scene transitions

### Cross-fade between scenes

```tsx
// Use with TransitionSeries from @remotion/transitions
import { TransitionSeries, linearTiming } from "@remotion/transitions";
import { fade } from "@remotion/transitions/fade";

<TransitionSeries>
  <TransitionSeries.Sequence durationInFrames={90}>
    <SceneA />
  </TransitionSeries.Sequence>
  <TransitionSeries.Transition
    presentation={fade()}
    timing={linearTiming({ durationInFrames: 15 })}
  />
  <TransitionSeries.Sequence durationInFrames={90}>
    <SceneB />
  </TransitionSeries.Sequence>
</TransitionSeries>
```

### Slide transition

```tsx
import { slide } from "@remotion/transitions/slide";

<TransitionSeries.Transition
  presentation={slide({ direction: "from-left" })}
  timing={springTiming({ config: { damping: 15 }, durationInFrames: 20 })}
/>
```

### Wipe transition

```tsx
import { wipe } from "@remotion/transitions/wipe";

<TransitionSeries.Transition
  presentation={wipe({ direction: "from-left" })}
  timing={linearTiming({ durationInFrames: 20 })}
/>
```

## Composition assembly pattern

A standard Remotion composition built from storyboard frames:

```tsx
import { AbsoluteFill, Sequence, useVideoConfig } from "remotion";
import { TransitionSeries, linearTiming } from "@remotion/transitions";
import { fade } from "@remotion/transitions/fade";
import { loadFont } from "@remotion/google-fonts/Montserrat";

const { fontFamily } = loadFont();

export const MyComposition: React.FC<{ brand: BrandContext }> = ({ brand }) => {
  const { fps, durationInFrames } = useVideoConfig();

  // Calculate frame allocations from storyboard
  const intro = Math.round(fps * 2);       // 2 seconds
  const message = Math.round(fps * 4);     // 4 seconds
  const cta = Math.round(fps * 2);         // 2 seconds
  const endcard = Math.round(fps * 2);     // 2 seconds
  const transitionDur = Math.round(fps * 0.5); // 0.5s transitions

  return (
    <AbsoluteFill style={{
      backgroundColor: brand.colors.background,
      fontFamily,
      color: brand.colors.text,
    }}>
      <TransitionSeries>
        <TransitionSeries.Sequence durationInFrames={intro}>
          <IntroFrame brand={brand} />
        </TransitionSeries.Sequence>

        <TransitionSeries.Transition
          presentation={fade()}
          timing={linearTiming({ durationInFrames: transitionDur })}
        />

        <TransitionSeries.Sequence durationInFrames={message}>
          <MessageFrame brand={brand} />
        </TransitionSeries.Sequence>

        <TransitionSeries.Transition
          presentation={fade()}
          timing={linearTiming({ durationInFrames: transitionDur })}
        />

        <TransitionSeries.Sequence durationInFrames={cta}>
          <CTAFrame brand={brand} />
        </TransitionSeries.Sequence>

        <TransitionSeries.Transition
          presentation={fade()}
          timing={linearTiming({ durationInFrames: transitionDur })}
        />

        <TransitionSeries.Sequence durationInFrames={endcard}>
          <EndCardFrame brand={brand} />
        </TransitionSeries.Sequence>
      </TransitionSeries>
    </AbsoluteFill>
  );
};
```

## Easing reference

Common easing curves and when to use them:

| Name | Remotion code | Feel | Use for |
|---|---|---|---|
| Linear | `Easing.linear` | Robotic, constant | Progress bars, timers |
| Ease out | `Easing.out(Easing.ease)` | Decelerating | Most entrances |
| Ease in | `Easing.in(Easing.ease)` | Accelerating | Exits, throws |
| Ease in-out | `Easing.inOut(Easing.ease)` | Smooth arc | Repositioning |
| Cubic out | `Easing.out(Easing.cubic)` | Snappy stop | UI elements |
| Expo out | `Easing.out(Easing.exp)` | Very fast then slow | Dramatic reveals |
| Back out | `Easing.out(Easing.back(1.5))` | Overshoot then settle | Playful pops |
| Bounce | `Easing.bounce` | Bouncing ball | Playful landings |
| Spring | `spring({ fps, config })` | Physics-based | Organic motion (preferred) |

Spring config quick reference:

| Feel | damping | mass | stiffness |
|---|---|---|---|
| Snappy | 15 | 0.5 | 200 |
| Bouncy | 6 | 0.4 | 180 |
| Smooth | 20 | 1.0 | 100 |
| Heavy | 25 | 2.0 | 80 |
| Elastic | 4 | 0.3 | 250 |
| Gentle | 30 | 1.5 | 60 |
