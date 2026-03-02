---
name: tac-visual-identity
description: Brand guide for The Alphabet Cartel. Use for image generation, UI design, dashboards, or visuals for TAC and its bots (Ratatoskr, Portia, Prism, Puck). Defines colors, shadows, and CSS tokens.
---

# The Alphabet Cartel — Visual Identity

## Overview

This skill defines the visual language for The Alphabet Cartel (TAC), an
LGBTQIA+ gaming and advocacy community. Every visual asset — generated images,
bot dashboards, web UIs, documents, and community graphics — should feel like
it belongs to the same family.

The core aesthetic is: **clean, modern, dark-themed with subtle rainbow accent
lighting, soft edges, and gentle depth through colored drop shadows.**

## Design Philosophy

TAC's visual identity communicates warmth, inclusivity, and modern
professionalism without feeling corporate. Think "cozy gaming lounge with
premium lighting" rather than "enterprise SaaS dashboard."

Key principles:

- **Soft, never sharp.** No hard 90-degree corners on UI elements. All
  interactive and container elements use slightly rounded corners
  (typically 8–12px border-radius for cards, 6px for buttons, 4px for
  inputs).
- **Depth through color, not harsh lines.** Elements gain visual hierarchy
  through subtle colored drop shadows rather than borders or stark
  contrast changes. Shadows pick up accent colors from the rainbow palette
  to create a gentle glow effect.
- **Dark-first.** All designs start with dark backgrounds. Light themes are
  not part of the TAC identity.
- **Rainbow as accent, not flood.** The LGBTQIA+ rainbow palette appears in
  accent lighting, glows, gradients, and highlights — never as large
  solid-color blocks. It should feel like light bleeding through, not
  paint on a wall.

## Color Palette

### Base Colors (backgrounds and surfaces)

| Token               | Hex       | Usage                                    |
|----------------------|-----------|------------------------------------------|
| `--tac-bg-deep`      | `#0d0d12` | Page/app background                      |
| `--tac-bg-surface`   | `#16161e` | Cards, panels, containers                |
| `--tac-bg-elevated`  | `#1e1e2a` | Modals, dropdowns, hover states          |
| `--tac-bg-input`     | `#12121a` | Form inputs, text areas                  |

### Text Colors

| Token               | Hex       | Usage                                    |
|----------------------|-----------|------------------------------------------|
| `--tac-text-primary`  | `#e8e6f0` | Primary body text                        |
| `--tac-text-secondary`| `#9896a8` | Labels, captions, muted text             |
| `--tac-text-disabled` | `#55536a` | Disabled/placeholder text                |

### Rainbow Accent Palette

These are used for glows, accent borders, icon highlights, shadows, and
subtle gradient touches. They are intentionally softened (not fully
saturated) to avoid harshness against dark backgrounds.

| Token               | Hex       | Color     |
|----------------------|-----------|-----------|
| `--tac-red`          | `#e05a6d` | Soft red   |
| `--tac-orange`       | `#e0885a` | Warm orange|
| `--tac-yellow`       | `#e0c95a` | Gold       |
| `--tac-green`        | `#5ae08b` | Mint green |
| `--tac-blue`         | `#5a9be0` | Sky blue   |
| `--tac-purple`       | `#9b5ae0` | Violet     |

### Functional Colors

| Token                | Hex       | Usage                                   |
|-----------------------|-----------|-----------------------------------------|
| `--tac-success`       | `#5ae08b` | Success states (mirrors green)          |
| `--tac-warning`       | `#e0c95a` | Warnings (mirrors yellow)               |
| `--tac-error`         | `#e05a6d` | Errors (mirrors red)                    |
| `--tac-info`          | `#5a9be0` | Info states (mirrors blue)              |

## Drop Shadow System

The signature TAC visual element. Shadows use semi-transparent accent colors
to create a soft glow beneath elements, giving depth and warmth.

### Standard shadow (cards and panels)
```css
box-shadow: 0 4px 16px rgba(155, 90, 224, 0.15),  /* purple glow */
            0 1px 4px rgba(0, 0, 0, 0.3);           /* grounding shadow */
```

### Interactive shadow (buttons, clickable cards on hover)
```css
box-shadow: 0 6px 24px rgba(90, 155, 224, 0.2),   /* blue glow */
            0 2px 6px rgba(0, 0, 0, 0.4);
```

### Accent shadow (featured or highlighted elements)
```css
box-shadow: 0 4px 20px rgba(224, 90, 109, 0.18),  /* red/pink glow */
            0 4px 20px rgba(155, 90, 224, 0.12),   /* purple glow */
            0 1px 4px rgba(0, 0, 0, 0.3);
```

The shadow color should complement the element's accent color when one is
present. For example, a success notification card might use a green-tinted
shadow.

## Corner Radius

All containers and interactive elements use rounded corners. Nothing should
have sharp 90-degree corners.

| Element Type         | Radius   |
|----------------------|----------|
| Page-level cards     | `12px`   |
| Inner cards/panels   | `8px`    |
| Buttons              | `6px`    |
| Inputs/selects       | `6px`    |
| Badges/tags          | `4px`    |
| Avatars/icons        | `50%` (circular) |

## Typography

- **Headings**: Inter (weight 600) — clean, modern, excellent at small and
  large sizes.
  Fallback: `system-ui, -apple-system, sans-serif`
- **Body**: Inter (weight 400) — consistency with headings, highly legible
  on screens.
  Fallback: `system-ui, -apple-system, sans-serif`
- **Monospace** (code, IDs, technical values): JetBrains Mono or
  `ui-monospace, monospace`

## Image Generation Prompts

When generating images for TAC using Imagen, Z-Image, or any image
generation tool, apply these standards.

### Tool-Specific Notes

**Google Imagen 4** (via gemini-imagen connector):
- Does NOT support the `negative_prompt` parameter. All avoidance terms
  must be folded into the main prompt (e.g., "no text, no watermarks").
- Generated images are saved automatically to the current user's
  **Windows Pictures directory** (typically `C:\Users\<username>\Pictures`).
  Let the user know where to find the output.
- Images are high resolution and may exceed the 1MB tool response limit.
  If the image cannot be returned inline, remind the user to check their
  Pictures folder.
- Models: `imagen-4` (standard, $0.04), `imagen-4-fast` (quick, $0.02),
  `imagen-4-ultra` (highest quality, $0.06). Default to `imagen-4`.

**Z-Image Turbo** (via Hugging Face connector):
- Supports resolution as a string enum, e.g. `"1536x864 ( 16:9 )"`.
- Subject to HuggingFace GPU quotas. If quota is exhausted, fall back
  to Imagen.
- Good for rapid iteration; lower fidelity than Imagen 4.

### Base Style Prompt (always prepend to the user's request)

Fold the TAC aesthetic AND avoidance terms into a single prompt since
not all tools support separate negative prompts:

```
clean modern dark-themed digital illustration, subtle rainbow accent
lighting, soft ambient glow, smooth rounded shapes, no harsh corners,
matte dark background with gentle colored light reflections,
professional and welcoming atmosphere, no text, no watermarks,
no photorealistic faces, no stock photo aesthetic, no bright white
backgrounds, digital art style
```

### Avoidance Terms Reference

When a tool DOES support a separate negative prompt field, use this list
instead of embedding avoidance in the main prompt:

```
photorealistic faces, stock photo aesthetic, text in image, watermark,
harsh sharp corners, bright white backgrounds, overly saturated
rainbow blocks, clip art, low quality, blurry
```

### Resolution Defaults by Use Case

| Use Case             | Imagen Ratio | Z-Image Resolution           |
|----------------------|--------------|-------------------------------|
| Hero/banner image    | `16:9`       | `1536x864 ( 16:9 )`          |
| Dashboard card art   | `4:3`        | `1152x864 ( 4:3 )`           |
| Square icon/avatar   | `1:1`        | `1024x1024 ( 1:1 )`          |
| Mobile banner        | `9:16`       | `864x1536 ( 9:16 )`          |

### Per-Bot Themes (future expansion)

As bots develop web frontends, each can have a signature accent pulled from
the rainbow palette. Current assignments:

| Bot          | Primary Accent | Shadow Tint   | Motif Notes                   |
|--------------|----------------|---------------|-------------------------------|
| Ratatoskr    | `--tac-purple` | Purple glow   | Norse squirrel, event/calendar|
| Portia       | `--tac-blue`   | Blue glow     | Voice, audio waves            |
| Prism        | `--tac-green`  | Green glow    | Onboarding, welcome, growth   |
| Puck         | `--tac-orange` | Orange glow   | Streaming, broadcast, energy  |

When generating images for a specific bot, weight the prompt toward that
bot's accent color in the lighting.

### Example Prompt — Ratatoskr Dashboard Hero

```
clean modern dark-themed digital illustration of a Norse-inspired squirrel
silhouette perched on a stylized world tree, subtle purple and violet
ambient lighting, soft rainbow accent glow along branches, smooth rounded
shapes, matte dark background, professional and welcoming atmosphere,
event calendar motif integrated subtly into tree branches, no text,
no watermarks, no photorealistic faces, digital art style
```

## CSS Design Tokens (Reference)

For frontend implementations, read `references/css-tokens.md` for a
complete copy-pasteable CSS custom properties block and utility classes.

## Applying This Skill

When this skill triggers:

1. **For image generation**: Prepend the base style prompt (including
   avoidance terms) to the user's description. Choose the correct
   resolution for the use case. If a specific bot is mentioned,
   incorporate its accent color into the prompt. Default to Imagen 4.
   Remind the user that generated images land in their Windows Pictures
   directory.

2. **For UI/frontend design**: Use the color palette, shadow system, corner
   radii, and typography defined here. Reference `references/css-tokens.md`
   for implementation.

3. **For documents and presentations**: Apply the dark palette and accent
   colors to charts, headers, and decorative elements. Avoid light/white
   backgrounds.

4. **For community graphics**: Follow the image generation standards. Keep
   rainbow accents subtle and tasteful.
