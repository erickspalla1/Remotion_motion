---
name: vibe-motion-engine
description: Generate Remotion animation code from natural language prompts, design briefs, and storyboards. Includes motion design patterns (easing, timing, transitions), ready-to-use animation templates (lower thirds, reveals, text animations, logo stings), and a prompt-to-component pipeline for AI-driven video creation. Use this skill whenever the user wants to create animations by describing them in natural language, needs motion design templates for Remotion, wants to convert a storyboard into animated sequences, or is building an AI-powered video creation tool. Also use when discussing animation timing, easing presets, transition design, or professional motion graphics patterns.
---

# Vibe Motion engine

Generate professional Remotion animations from natural language descriptions, design briefs, and storyboards. Covers three areas: motion design patterns, ready-to-use templates, and AI-driven code generation.

Works alongside `remotion-best-practices` (Remotion API reference) and `design-file-parser` (PSD/AI/Figma import). This skill focuses on the creative and generative layer.

## Motion design system

### Timing presets

```typescript
export const TIMING = {
  fadeIn: { frames: 12, delay: 0 },        // 0.4s @ 30fps
  slideIn: { frames: 15, delay: 0 },       // 0.5s
  scaleIn: { frames: 18, delay: 0 },       // 0.6s
  bounceIn: { frames: 24, delay: 0 },      // 0.8s
  crossfade: { frames: 15 },               // 0.5s
  wipe: { frames: 12 },                    // 0.4s
  zoom: { frames: 18 },                    // 0.6s
  staggerShort: 4,                          // 0.13s between items
  staggerMedium: 6,                         // 0.2s
  staggerLong: 10,                          // 0.33s
  holdShort: 45,                            // 1.5s — single word
  holdMedium: 75,                           // 2.5s — short sentence
  holdLong: 120,                            // 4s — paragraph
  holdCTA: 90,                              // 3s — call to action
  fadeOut: { frames: 10 },
  slideOut: { frames: 12 },
} as const;
```

### Easing presets

Never use linear easing for motion graphics.

```typescript
import { Easing, spring } from "remotion";

export const EASING = {
  standard: Easing.bezier(0.4, 0, 0.2, 1),
  enter: Easing.bezier(0, 0, 0.2, 1),
  exit: Easing.bezier(0.4, 0, 1, 1),
  emphasis: Easing.bezier(0.4, 0, 0.6, 1),
  overshoot: Easing.bezier(0.34, 1.56, 0.64, 1),
  decelerate: Easing.bezier(0.0, 0.0, 0.2, 1),
  snap: Easing.bezier(0.7, 0, 0.3, 1),
} as const;

export const SPRINGS = {
  gentle: { damping: 15, mass: 1, stiffness: 120 },
  snappy: { damping: 20, mass: 0.8, stiffness: 300 },
  bouncy: { damping: 8, mass: 1, stiffness: 200 },
  heavy: { damping: 25, mass: 2, stiffness: 150 },
  elastic: { damping: 6, mass: 0.5, stiffness: 250 },
} as const;
```

### Animation building blocks

**Fade + slide**
```typescript
const FadeSlide: React.FC<{
  direction?: "up" | "down" | "left" | "right";
  distance?: number; delay?: number; children: React.ReactNode;
}> = ({ direction = "up", distance = 30, delay = 0, children }) => {
  const frame = useCurrentFrame();
  const { fps } = useVideoConfig();
  const progress = spring({ frame: frame - delay, fps, config: SPRINGS.gentle });
  const offsets = { up: { x: 0, y: distance }, down: { x: 0, y: -distance }, left: { x: distance, y: 0 }, right: { x: -distance, y: 0 } };
  const { x, y } = offsets[direction];
  return <div style={{ opacity: progress, transform: `translate(${x * (1 - progress)}px, ${y * (1 - progress)}px)` }}>{children}</div>;
};
```

**Scale reveal**
```typescript
const ScaleReveal: React.FC<{ delay?: number; from?: number; children: React.ReactNode }> = ({ delay = 0, from = 0.5, children }) => {
  const frame = useCurrentFrame();
  const { fps } = useVideoConfig();
  const scale = spring({ frame: frame - delay, fps, config: SPRINGS.bouncy });
  return <div style={{ opacity: scale, transform: `scale(${from + (1 - from) * scale})` }}>{children}</div>;
};
```

**Stagger group**
```typescript
const StaggerGroup: React.FC<{ stagger?: number; children: React.ReactNode[] }> = ({ stagger = TIMING.staggerMedium, children }) => (
  <>{React.Children.map(children, (child, i) => <FadeSlide delay={i * stagger}>{child}</FadeSlide>)}</>
);
```

**Clip reveal**
```typescript
const ClipReveal: React.FC<{ direction?: "left" | "right" | "top" | "bottom"; delay?: number; children: React.ReactNode }> = ({ direction = "left", delay = 0, children }) => {
  const frame = useCurrentFrame();
  const { fps } = useVideoConfig();
  const progress = spring({ frame: frame - delay, fps, config: SPRINGS.snappy });
  const clips = { left: `inset(0 ${100 - progress * 100}% 0 0)`, right: `inset(0 0 0 ${100 - progress * 100}%)`, top: `inset(0 0 ${100 - progress * 100}% 0)`, bottom: `inset(${100 - progress * 100}% 0 0 0)` };
  return <div style={{ clipPath: clips[direction] }}>{children}</div>;
};
```

## Templates

### Lower third
```typescript
const LowerThird: React.FC<{ name: string; title: string; accentColor?: string; fontFamily?: string }> = ({ name, title, accentColor = "#FF6B35", fontFamily = "Inter" }) => {
  const frame = useCurrentFrame();
  const { fps } = useVideoConfig();
  const bar = spring({ frame, fps, config: SPRINGS.snappy });
  const text = spring({ frame: frame - 8, fps, config: SPRINGS.gentle });
  return (
    <AbsoluteFill>
      <div style={{ position: "absolute", bottom: 80, left: 60, display: "flex", flexDirection: "column", gap: 4 }}>
        <div style={{ width: 40 * bar, height: 3, backgroundColor: accentColor, marginBottom: 8 }} />
        <div style={{ fontFamily, fontSize: 32, fontWeight: 700, color: "white", opacity: text, transform: `translateY(${20 * (1 - text)}px)` }}>{name}</div>
        <div style={{ fontFamily, fontSize: 18, fontWeight: 400, color: "rgba(255,255,255,0.7)", opacity: text, transform: `translateY(${15 * (1 - text)}px)` }}>{title}</div>
      </div>
    </AbsoluteFill>
  );
};
```

### Word-by-word text reveal
```typescript
const WordReveal: React.FC<{ text: string; fontSize?: number; color?: string; fontFamily?: string; stagger?: number }> = ({ text, fontSize = 48, color = "white", fontFamily = "Inter", stagger = 3 }) => {
  const frame = useCurrentFrame();
  const { fps } = useVideoConfig();
  return (
    <div style={{ display: "flex", flexWrap: "wrap", gap: "0.3em", fontFamily, fontSize, fontWeight: 700, color }}>
      {text.split(" ").map((word, i) => {
        const p = spring({ frame: frame - i * stagger, fps, config: SPRINGS.snappy });
        return <span key={i} style={{ opacity: p, transform: `translateY(${20 * (1 - p)}px)`, display: "inline-block" }}>{word}</span>;
      })}
    </div>
  );
};
```

### Logo sting
```typescript
const LogoSting: React.FC<{ logoSrc: string; backgroundColor?: string; accentColor?: string; size?: number }> = ({ logoSrc, backgroundColor = "#000", accentColor = "#FF6B35", size = 200 }) => {
  const frame = useCurrentFrame();
  const { fps, durationInFrames } = useVideoConfig();
  const circle = spring({ frame, fps, config: SPRINGS.heavy });
  const logo = spring({ frame: frame - 8, fps, config: SPRINGS.bouncy });
  const exit = interpolate(frame, [durationInFrames - 15, durationInFrames], [1, 0], { extrapolateLeft: "clamp", extrapolateRight: "clamp" });
  return (
    <AbsoluteFill style={{ backgroundColor, justifyContent: "center", alignItems: "center", opacity: exit }}>
      <div style={{ position: "absolute", width: size * 1.5, height: size * 1.5, borderRadius: "50%", backgroundColor: accentColor, opacity: 0.15, transform: `scale(${circle})` }} />
      <Img src={logoSrc} style={{ width: size, height: size, objectFit: "contain", transform: `scale(${0.5 + 0.5 * logo})`, opacity: logo }} />
    </AbsoluteFill>
  );
};
```

### Slide wipe transition
```typescript
const SlideWipe: React.FC<{ children: React.ReactNode; direction?: "left" | "right"; color?: string }> = ({ children, direction = "left", color = "#FF6B35" }) => {
  const frame = useCurrentFrame();
  const { fps } = useVideoConfig();
  const wipe = spring({ frame, fps, config: SPRINGS.snappy });
  const content = interpolate(frame, [10, 16], [0, 1], { extrapolateLeft: "clamp", extrapolateRight: "clamp" });
  const tx = direction === "left" ? `${-100 + wipe * 200}%` : `${100 - wipe * 200}%`;
  return (
    <AbsoluteFill>
      <div style={{ opacity: content }}>{children}</div>
      <div style={{ position: "absolute", inset: 0, backgroundColor: color, transform: `translateX(${tx})` }} />
    </AbsoluteFill>
  );
};
```

## Prompt-to-component pipeline

### System prompt for LLM code generation

```
You are a Remotion motion design expert. Generate TypeScript/React code for Remotion compositions.

RULES:
- Always use useCurrentFrame() and useVideoConfig()
- Prefer spring() over interpolate() for natural motion
- Always clamp interpolate: extrapolateRight: "clamp", extrapolateLeft: "clamp"
- Use <Sequence> with from and durationInFrames for scene organization
- Use <AbsoluteFill> as root container
- Use <Img> from "remotion", not <img>
- Use <OffthreadVideo> for video embeds
- Use brand palette from context for all colors
- Export a single root component with all Sequences

TIMING: 30fps standard. Entrances 12-24 frames. Hold text min 60 frames. Transitions 12-18 frames. Stagger 4-8 frames.
```

### Natural language → animation mapping

| User says (PT/EN) | Implementation |
|---|---|
| texto entrando / text comes in | FadeSlide or ClipReveal |
| com bounce / bouncy | spring() SPRINGS.bouncy |
| suave / smooth | spring() SPRINGS.gentle |
| rápido / fast | spring() SPRINGS.snappy |
| um por um / one by one | StaggerGroup |
| zoom no logo | ScaleReveal |
| fade / desvanecer | opacity interpolation |
| slide / deslizar | translateX/Y spring |
| wipe / cortina | SlideWipe |
| piscar / pulse | looped opacity 0→1→0 |
| girar / rotate | rotate 0→360 |
| partículas / particles | Array.from + random + stagger |

### Data structures

```typescript
interface Briefing {
  brand: { name: string; colors: { primary: string; secondary: string; accent: string }; fonts: { heading: string; body: string }; logoUrl: string };
  campaign?: { name: string; kvUrl?: string };
  format: { width: number; height: number; fps: number; durationSeconds: number };
  objective: string;
}

interface StoryboardScreen {
  id: string; order: number; description: string; text?: string; imageUrl?: string;
  durationFrames: number; transition?: "cut" | "crossfade" | "wipe" | "slide";
}
```

### Format presets

```typescript
export const FORMATS = {
  stories: { width: 1080, height: 1920, fps: 30 },
  feed_square: { width: 1080, height: 1080, fps: 30 },
  feed_portrait: { width: 1080, height: 1350, fps: 30 },
  reels: { width: 1080, height: 1920, fps: 30 },
  youtube: { width: 1920, height: 1080, fps: 30 },
  youtube_shorts: { width: 1080, height: 1920, fps: 30 },
  preroll_16x9: { width: 1920, height: 1080, fps: 30 },
  presentation: { width: 1920, height: 1080, fps: 30 },
} as const;
```

### Storyboard → composition

```typescript
import { TransitionSeries, linearTiming } from "@remotion/transitions";
import { fade } from "@remotion/transitions/fade";
import { slide } from "@remotion/transitions/slide";
import { wipe } from "@remotion/transitions/wipe";

const TRANSITIONS = {
  cut: null,
  crossfade: { presentation: fade(), timing: linearTiming({ durationInFrames: 15 }) },
  wipe: { presentation: wipe(), timing: linearTiming({ durationInFrames: 12 }) },
  slide: { presentation: slide(), timing: linearTiming({ durationInFrames: 12 }) },
};

function buildComposition(briefing: Briefing, screens: StoryboardScreen[]) {
  const hasTransitions = screens.some(s => s.transition && s.transition !== "cut");
  if (hasTransitions) {
    return (
      <TransitionSeries>
        {screens.map((screen, i) => (
          <React.Fragment key={screen.id}>
            <TransitionSeries.Sequence durationInFrames={screen.durationFrames}>
              <ScreenComponent screen={screen} briefing={briefing} />
            </TransitionSeries.Sequence>
            {i < screens.length - 1 && screen.transition !== "cut" && TRANSITIONS[screen.transition] && (
              <TransitionSeries.Transition presentation={TRANSITIONS[screen.transition].presentation} timing={TRANSITIONS[screen.transition].timing} />
            )}
          </React.Fragment>
        ))}
      </TransitionSeries>
    );
  }
  let f = 0;
  return (
    <AbsoluteFill>
      {screens.map((screen) => { const from = f; f += screen.durationFrames; return <Sequence key={screen.id} from={from} durationInFrames={screen.durationFrames}><ScreenComponent screen={screen} briefing={briefing} /></Sequence>; })}
    </AbsoluteFill>
  );
}
```

## Quality rules

- Max 5 Sequences per composition without user confirmation
- Always include safe area (10% padding) for social media
- Logo in first or last 2 seconds, never floating randomly
- Text readable for minimum 2 seconds — flag if script too long for duration
- Primary color for backgrounds, accent for highlights
- When in doubt, slower animations — rushed feels cheap
- One hero element per screen
- Test at 1x speed before rendering
