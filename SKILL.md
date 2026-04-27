---
name: landbot-web-design-system
description: Landbot's Web Design System. Use this skill whenever creating, editing, or reviewing any HTML, CSS, or web component intended for Landbot's marketing website or any Landbot-branded web surface. Triggers include requests to build a landing page, hero section, pricing page, blog post layout, button, card, form, navigation, or any other web UI for Landbot. Also use when applying Landbot tokens (colors, typography, spacing, radius, elevation, motion) to existing markup, or when reviewing web work for brand consistency. Do NOT trigger for non-Landbot web work or for the in-product app UI (the design system covers the marketing site only).
---

# Landbot Web Design System

The single source of truth for Landbot's marketing website. Tokens, components, and patterns.

## How to use this skill

When building or reviewing any web UI for Landbot's marketing site:

1. **Read `tokens/DESIGN-SYSTEM-REFERENCE.md` first.** This is the canonical token reference — every color, spacing, radius, elevation, gradient, focus-ring, and motion token, with values and usage rules. Read it before generating or reviewing any code.

2. **Use `docs/index.html` as the visual reference.** It's the rendered showcase: one big page with anchor sections for each token group and component (`#colors`, `#typography`, `#buttons`, `#cards`, `#forms`, etc.). The `:root` block at the top of this file mirrors the tokens defined in the markdown reference and is what gets copied into consumer projects.

3. **Pull component snippets from `docs/components/`.** Each file is a self-contained CSS+HTML fragment for one component (buttons, cards, navigation, forms, etc.). Components reference tokens via `var(--name)`, so the tokens (from `:root` of `docs/index.html`) must be present in any project that uses these snippets.

## Token cheat sheet

Full list in `tokens/DESIGN-SYSTEM-REFERENCE.md`. The most important ones:

- **Brand colors:** `--color-brand-primary` (#5A60F6), `--color-brand-secondary` (#33405E), `--color-brand-accent` (#FF3F7B)
- **Text:** `--color-text-primary` (#3A3D5C), `--color-text-secondary` (#5D6079), `--color-text-inverse` (#FFFFFF)
- **Surfaces:** `--color-surface-page` (#FFFFFF), `--color-surface-card` (#FBFBFC), `--color-surface-dark` (#1B2139)
- **Status:** `--color-status-success`, `--color-status-warning`, `--color-status-error`, `--color-status-info`, plus matching surfaces and accessible text colors
- **Spacing scale:** `--spacing-0` through `--spacing-12` (0px to 128px, doubling-style)
- **Radius scale:** `--radius-0` through `--radius-6`, plus `--radius-pill` (9999px)
- **Elevation:** `--elevation-1`, `--elevation-2`, `--elevation-3`
- **Gradients:** `--gradient-brand`, `--gradient-dark`, `--gradient-purple-soft`, plus glow variants
- **Typography:** DM Sans, weights 300 to 700

All color tokens have been AA-checked for WCAG contrast. Stick to the tokens. Don't introduce new colors.

## Components available

The `docs/components/` folder contains extracted snippets for:

buttons, cards, colors, dark-surfaces, elevation, focus-states, forms, gradients, icons, imagery, labels-tags, layout-grid, motion, navigation, spacing-radius, toggle, tooltips, typography

Each file has a header comment pointing back to the source lines in `docs/index.html`.

## Rules for output

When generating Landbot web UI:

1. Use the design tokens by name. Never hardcode hex values that already have a token.
2. Use DM Sans for all text.
3. Default radius for cards and buttons: `--radius-4` (8px) for buttons, `--radius-5` (12px) for cards.
4. Default elevation for cards: `--elevation-1`. Use `--elevation-2` only on hover or for emphasis.
5. Brand gradient (`--gradient-brand`) is the primary accent. Use it sparingly, on heroes and primary CTAs.
6. For dark sections, use `--color-surface-dark` as the background and the on-dark text tokens (`--color-text-on-dark`, `--color-text-on-dark-secondary`, `--color-text-on-dark-muted`).
7. All icons use Hugeicons (stroke rounded). The CSS is loaded from `https://cdn.hugeicons.com/font/hgi-stroke-rounded.css`.

## Source of truth

This repo is the canonical version. The hosted browseable URL is `https://landbot.github.io/web-design-system/` (Landbot org members only). Any change to tokens, components, or patterns must go through this repo.
