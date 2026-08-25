# Design System Spec

Reference doc for building and extending this portfolio site. Keep new work consistent with these values rather than introducing one-off styles.

---

## 1. Color palette (light theme, WCAG-checked)

| Token | Hex | Use | Contrast on `--bg` |
|---|---|---|---|
| `--bg` | `#F5F4F4` | Page background | — |
| `--card` | `#FFFFFF` | Card and surface background | — |
| `--card-border` | `rgba(35,29,29,0.10)` | Card borders and dividers | — |
| `--text` | `#231D1D` | Primary text and headings | 15.1:1 |
| `--text-dim` | `#6E5E5E` | Secondary text, body copy, and small metadata | 5.58:1 |
| `--text-mute` | `#7B8285` | Large metadata, icons, or borders only | 3.56:1 |
| `--sage` | `#445B4B` | Primary accent, links, buttons, and active states | 6.73:1 |
| `--sage-deep` | `#27372C` | Hover state for sage elements | 11.46:1 |
| `--pink` | `#893E5C` | Secondary accent, tags, and labels | 6.58:1 |
| `--pink-deep` | `#572439` | Hover state for pink elements | 11.14:1 |
| `--blue` | `#2F4E62` | Decorative accent only | 8.01:1 |

Any text below 18px must use a token with at least 4.5:1 contrast against its background. Do not use `--text-mute` for small body text.

Do not introduce new hex values without checking WCAG contrast: AA minimum 4.5:1 for normal text and 3:1 for large text or UI components.

---

## 2. Typography

| Role | Font | Weight | Notes |
|---|---|---|---|
| Display and headings | `Fraunces` | 500 | Optical-size variable font for headings and card titles |
| Body | `Inter` | 400 / 500 | Default reading text, navigation, and buttons |
| Data and labels | `IBM Plex Mono` | 400 / 500 | Eyebrows, tags, and metadata; uppercase with letter spacing |

All three fonts are loaded through Google Fonts and are available under the SIL Open Font License.

### Type scale

| Size | Use |
|---|---|
| 11–12px | Tags, eyebrows, and metadata |
| 13–14px | Secondary text, card descriptions, and navigation links |
| 15–16px | Primary body copy and section subtitles |
| 17–19px | Case-study and work-experience card titles |
| `clamp(26px, 3.4vw, 34px)` | Section headings |
| `clamp(34px, 5vw, 52px)` | Page and hero titles |

Use line height `1.5–1.7` for body copy and `1.12–1.2` for large display headings.

---

## 3. Layout and container alignment

Use one shared content rail across every page:

```css
.wrap,
.nav-inner,
.hero-inner,
.tools-head {
  max-width: 1200px;
  margin: 0 auto;
  padding-left: 16px;
  padding-right: 16px;
}
```

The global rule `box-sizing: border-box` applies to every element. Keep major content aligned to the same left edge. On small screens, retain the `16px` side inset and let the layout collapse naturally.

The hero uses vertical padding only on its outer wrapper. Its inner content owns the horizontal padding so it aligns with the sections below.

---

## 4. Spacing scale

Use an 8px base unit:

```
4px    micro — icon-to-label and tight inline gaps
8px    tight — tags, labels, and related content
16px   default — navigation inset and paragraph-to-control spacing
24px   component gap and card internal spacing
32px   gap between cards in a grid
48px   gap between sub-sections and hero columns
64px   compact section or hero vertical padding
64–90px section vertical padding
```

Avoid arbitrary spacing values. Use the nearest scale value or a 4px half-step when an intermediate value is necessary.

---

## 5. Button hierarchy and states

| Tier | Style | Use |
|---|---|---|
| Primary | Solid `--sage` fill, white text, `30px` pill radius | One main action per view |
| Ghost | Transparent, `1px` border, `--text` label | Secondary action beside a primary |
| Text link | No fill or border, `--sage` color | Navigation and inline actions |

Interactive elements use `translateY(-2px)` and a `0.25s ease` transition on hover. Keyboard users must receive a visible `:focus-visible` outline. Disabled controls reduce opacity to about 40%, remove the hover transform, and use `cursor: not-allowed`.

---

## 6. Component patterns

- Cards use a white surface, `1px solid var(--card-border)`, a `10–16px` radius, and a subtle `0 2px 14px rgba(35,29,29,0.04)` shadow.
- Card hover states use a small upward transform and a stronger shadow.
- Tags and pills use IBM Plex Mono at 10.5–11px, uppercase, with an accent-colored border and no fill.
- Eyebrows use IBM Plex Mono at 12px, uppercase, `--sage`, and a leading dot or divider.
- Navigation is sticky with a translucent blurred background, underline-on-hover links, and one active state per page.
- Home navigation is an inline Lucide house icon beside the wordmark, using the sage accent without a filled button background.

---

## 7. Tools marquee

The homepage tools section uses a logo-only horizontal marquee for Figma, Miro, Framer, VS Code + AI, Canva, Notion, Medium, Claude, and ChatGPT.

- Use two identical rows for a seamless loop.
- Use a slow, linear, infinite animation with no easing or abrupt reset.
- Keep logo tiles at a stable size and maintain equal spacing.
- Use a fade mask at both edges of the viewing area.
- Pause on hover and pause automatically for `prefers-reduced-motion: reduce`.
- Keep tool names available through `title` and `alt` attributes even when labels are not visible.

---

## 8. General hierarchy principles

1. Size, weight, and color should agree rather than compete.
2. Use whitespace to group related items and separate unrelated sections.
3. Use one primary action per view.
4. Reuse the existing tokens, type scale, spacing scale, and component patterns.
5. Check contrast for every new text and background pairing.
6. Preserve content and copy when making visual-system updates unless a content change is explicitly requested.
