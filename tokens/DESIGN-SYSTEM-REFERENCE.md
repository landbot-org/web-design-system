# Landbot Web Design System — Token Reference

> **AI-ready reference.** All values in this document are fully resolved (no aliases). Use the CSS custom properties section as the single source of truth when generating code. Never hardcode hex values — always use the variables.

---

## Quick Reference

| Property | Token | Value |
|---|---|---|
| Brand primary | `--color-brand-primary` | `#5A60F6` |
| Brand accent | `--color-brand-accent` | `#FF3F7B` |
| Brand secondary | `--color-brand-secondary` | `#33405E` |
| Text primary | `--color-text-primary` | `#3A3D5C` |
| Text secondary | `--color-text-secondary` | `#5D6079` |
| Page background | `--color-surface-page` | `#FFFFFF` |
| Card background | `--color-surface-card` | `#FBFBFC` |
| Border default | `--color-border-default` | `#E5E6EA` |
| Font family | `--font-sans` | `DM Sans, sans-serif` |
| Spacing base | `--spacing-4` | `16px` (base unit) |
| Button radius | `--radius-4` | `8px` |
| Breakpoints | `--bp-tablet` / `--bp-desktop` | `768px` / `1024px` |

**Critical rules for AI tools:**
- Font is always **DM Sans**. Always set `font-variation-settings: 'opsz' 14`.
- Heading font-weight is **400** (not bold). Negative letter-spacing on all headings.
- CTA buttons always use **`--radius-4` (8px)**. Never pill radius on buttons.
- Pill radius (`9999px`) is **only for tags, badges, and toggle tracks**.
- Three breakpoints: **mobile (< 768px)**, **tablet (768–1023px)**, **desktop (≥ 1024px)**. Grid is **4 / 8 / 12** columns.

---

## Architecture

```
01-primitives.json   →   Raw values. No references. Single source of truth.
        ↓
02-semantic.json     →   Named aliases. Reference primitives. These are the CSS custom properties.
        ↓
03-maps.json         →   Component decisions. Reference semantic tokens. Typography scale + component specs.
        ↓
04-responsive.json   →   Breakpoint overrides. Mobile vs desktop values for layout, spacing, and type scale.
```

Each layer only references the layer directly above it. Never skip layers when referencing tokens.

---

## 1. Primitives Collection

Raw color palette, spacing scale, radius, font, and elevation. No semantic meaning at this level.

### Color Palette

#### Purple (brand primary family) — PU
| Step | Hex | Role |
|---|---|---|
| 50 | `#FAFAFF` | brand-tinted white surface |
| 100 | `#EBECFF` | brand-subtle surface |
| 200 | `#CFD1FE` | |
| 300 | `#B3B5FD` | |
| 400 | `#9699FC` | primaryLight (links on dark) |
| **500** | **`#5A60F6`** | **brand primary ★** |
| 600 | `#5259E0` | text on brand-subtle surface |
| 700 | `#4047C4` | |
| 800 | `#2E35A8` | |
| 900 | `#1C228C` | |

#### Pink (brand accent / error family) — PK
| Step | Hex | Role |
|---|---|---|
| 100 | `#FFE8EF` | error surface |
| 200 | `#FFC3D6` | |
| 300 | `#FF9EBE` | |
| 300 | `#FF9EBE` | accentLight |
| 400 | `#FF6F9D` | |
| **500** | **`#FF3F7B`** | **brand accent ★ / error indicator** |
| 600 | `#E03168` | |
| 700 | `#BE2257` | text on error surface |
| 800 | `#991546` | |
| 900 | `#730937` | |

#### Green (success family) — TE
| Step | Hex | Role |
|---|---|---|
| 100 | `#DEF6DF` | success surface |
| 200 | `#BDEDBE` | |
| 300 | `#8DE090` | |
| 400 | `#64D169` | |
| **500** | **`#52CC57`** | **success indicator ★** |
| 600 | `#3CAF41` | |
| 700 | `#2A8F2F` | |
| 800 | `#1B6B1F` | text on success surface |
| 900 | `#0E4511` | |

#### Orange (warning family) — OR
| Step | Hex | Role |
|---|---|---|
| 100 | `#FEF3E0` | warning surface |
| 200 | `#FDE0B0` | |
| 300 | `#FCC97A` | |
| 400 | `#FAB03E` | |
| **500** | **`#F58B0B`** | **warning indicator ★** |
| 600 | `#D67409` | |
| 700 | `#AE5D07` | |
| 800 | `#884705` | text on warning surface |
| 900 | `#623203` | |

#### Blue (info family) — BL
| Step | Hex | Role |
|---|---|---|
| 100 | `#EEF9FD` | info surface |
| 200 | `#CEEFFA` | |
| 300 | `#A8E4F7` | |
| 400 | `#82D8F1` | |
| **500** | **`#6BCEEB`** | **info indicator ★** |
| 600 | `#4BBBD8` | |
| 700 | `#35A5C1` | |
| 800 | `#228DAA` | |
| 900 | `#12728E` | text on info surface |

#### Navy (blue-navy hue family) — NV
| Step | Hex | Role |
|---|---|---|
| 100 | `#E7EBF3` | |
| 200 | `#C9CFE5` | text on dark (secondary) |
| 300 | `#AABAD4` | |
| 400 | `#8CA5C3` | text on dark (muted) |
| 500 | `#6E83AA` | |
| 600 | `#546994` | |
| 700 | `#3F527F` | |
| 800 | `#2C3E6B` | |
| **900** | **`#33405E`** | **brand secondary ★** |
| 950 | `#252D47` | dark raised surface |
| 1000 | `#1B2139` | dark section background |

#### Status families (resolved)
| Color | Surface (100) | Indicator (500) | Text on surface |
|---|---|---|---|
| Success (green) | `#DEF6DF` | `#52CC57` | `#1B6B1F` |
| Warning (orange) | `#FEF3E0` | `#F58B0B` | `#884705` |
| Error (pink) | `#FFE8EF` | `#FF3F7B` | `#BE2257` |
| Info (blue) | `#EEF9FD` | `#6BCEEB` | `#12728E` |
| Stars (amber) | `#FFF8E7` | `#F59E0B` | `#B45309` |

#### Neutral (text · surface · border scale)
| Step | Hex | Usage |
|---|---|---|
| 0 | `#FFFFFF` | page background |
| 10 | `#FBFBFC` | card background |
| 20 | `#F7F7F8` | hover state / subtle border |
| 30 | `#EFEFF2` | page chrome |
| 40 | `#E5E6EA` | border default |
| 50 | `#CECFD6` | |
| 100 | `#9596A7` | disabled text |
| 200 | `#898B9D` | |
| 300 | `#7D7F93` | |
| 400 | `#73758B` | |
| 500 | `#676A81` | |
| **600** | **`#5D6079`** | **text secondary ★** |
| 700 | `#50526E` | |
| 800 | `#444764` | |
| **900** | **`#3A3D5C`** | **text primary ★** |

### Spacing Scale

8pt base. Keys map directly to Tailwind spacing.

| Token | Value | Tailwind equiv |
|---|---|---|
| `--spacing-1` | `4px` | `p-1` |
| `--spacing-2` | `8px` | `p-2` |
| `--spacing-3` | `12px` | `p-3` |
| `--spacing-4` | `16px` | `p-4` |
| `--spacing-5` | `24px` | `p-6` |
| `--spacing-6` | `32px` | `p-8` |
| `--spacing-7` | `40px` | `p-10` |
| `--spacing-8` | `48px` | `p-12` |
| `--spacing-9` | `64px` | `p-16` |
| `--spacing-10` | `80px` | `p-20` |
| `--spacing-11` | `96px` | `p-24` |
| `--spacing-12` | `128px` | `p-32` |

### Border Radius

| Token | Value | Usage |
|---|---|---|
| `--radius-0` | `0px` | none |
| `--radius-1` | `2px` | inline code chips |
| `--radius-2` | `4px` | small badges |
| `--radius-3` | `6px` | small buttons, nav links |
| **`--radius-4`** | **`8px`** | **CTA buttons, inputs, standard cards** |
| `--radius-5` | `12px` | large cards, feature boxes |
| `--radius-6` | `16px` | hero blocks, page banners |
| `--radius-pill` | `9999px` | tags, badges, toggles only |

### Elevation (Box Shadows)

All shadows use `rgba(51,64,94,0.08)` — navy at 8% opacity.

| Token | CSS value |
|---|---|
| `--elevation-1` | `0 1px 1px rgba(51,64,94,0.08), 0 2px 2px 1px rgba(51,64,94,0.08)` |
| `--elevation-2` | `0 2px 2px rgba(51,64,94,0.08), 0 4px 4px rgba(51,64,94,0.08), 0 8px 8px rgba(51,64,94,0.08)` |
| `--elevation-3` | `0 4px 4px rgba(51,64,94,0.08), 0 8px 8px rgba(51,64,94,0.08), 0 16px 16px rgba(51,64,94,0.08)` |
| `--elevation-4` | `0 4px 4px rgba(51,64,94,0.08), 0 8px 8px rgba(51,64,94,0.08), 0 16px 16px rgba(51,64,94,0.08), 0 32px 32px rgba(51,64,94,0.08)` |

**Usage:** elevation-1 → cards · elevation-2 → dropdowns/nav · elevation-3 → modals/drawers · elevation-4 → floating elements

### Motion (code-only — not in Figma JSON files)

| Token | Value | Usage |
|---|---|---|
| `--duration-fast` | `150ms` | hover states, toggles, icon swaps |
| `--duration-normal` | `250ms` | panels, menus, reveals |
| `--duration-slow` | `400ms` | hero animations, full-screen overlays |
| `--ease-out` | `cubic-bezier(0.0, 0.0, 0.2, 1)` | default — elements leaving |
| `--ease-in` | `cubic-bezier(0.4, 0.0, 1.0, 1)` | elements entering |
| `--ease-in-out` | `cubic-bezier(0.4, 0.0, 0.2, 1)` | sliders, tab indicators |
| `--ease-spring` | `cubic-bezier(0.34, 1.56, 0.64, 1)` | modals, drawers, tooltips |

### Z-Index Scale (code-only — not in Figma JSON files)

| Token | Value | Layer |
|---|---|---|
| `--z-base` | `0` | |
| `--z-raised` | `10` | |
| `--z-dropdown` | `100` | dropdowns, popovers |
| `--z-sticky` | `200` | sticky headers |
| `--z-overlay` | `300` | background scrims |
| `--z-modal` | `400` | modals, drawers |
| `--z-toast` | `500` | toast notifications |
| `--z-tooltip` | `600` | tooltips |

---

## 2. Alias / Semantic Collection

Named tokens that give meaning to primitives. These map directly to `:root` CSS custom properties. **Always use these in components, never raw primitives.**

### Brand Colors (resolved)

| Semantic token | CSS var | Resolved value |
|---|---|---|
| `color.brand.primary` | `--color-brand-primary` | `#5A60F6` |
| `color.brand.primaryLight` | `--color-brand-primary-light` | `#9699FC` |
| `color.brand.secondary` | `--color-brand-secondary` | `#33405E` |
| `color.brand.accent` | `--color-brand-accent` | `#FF3F7B` |
| `color.brand.accentLight` | `--color-brand-accent-light` | `#FF9EBE` |

### Text Colors (resolved)

| Semantic token | CSS var | Resolved value | WCAG on white |
|---|---|---|---|
| `color.text.primary` | `--color-text-primary` | `#3A3D5C` | 11.4:1 ✅ |
| `color.text.secondary` | `--color-text-secondary` | `#5D6079` | — |
| `color.text.disabled` | `--color-text-disabled` | `#9596A7` | exempt |
| `color.text.inverse` | `--color-text-inverse` | `#FFFFFF` | on colored bg |
| `color.text.onDark` | `--color-text-on-dark` | `#FFFFFF` | headings on dark |
| `color.text.onDarkSecondary` | `--color-text-on-dark-secondary` | `#C9CFE5` | 9.6:1 ✅ |
| `color.text.onDarkMuted` | `--color-text-on-dark-muted` | `#8CA5C3` | 6.0:1 ✅ |
| `color.text.onBrandSubtle` | `--color-text-on-brand-subtle` | `#5259E0` | 4.65:1 ✅ |
| `color.text.onSuccess` | `--color-text-on-success` | `#1B6B1F` | 5.80:1 ✅ |
| `color.text.onWarning` | `--color-text-on-warning` | `#884705` | 6.36:1 ✅ |
| `color.text.onError` | `--color-text-on-error` | `#BE2257` | 5.08:1 ✅ |
| `color.text.onInfo` | `--color-text-on-info` | `#12728E` | 5.12:1 ✅ |

### Surface Colors (resolved)

| Semantic token | CSS var | Resolved value |
|---|---|---|
| `color.surface.page` | `--color-surface-page` | `#FFFFFF` |
| `color.surface.card` | `--color-surface-card` | `#FBFBFC` |
| `color.surface.chrome` | `--color-surface-chrome` | `#EFEFF2` |
| `color.surface.hover` | `--color-surface-hover` | `#F7F7F8` |
| `color.surface.dark` | `--color-surface-dark` | `#1B2139` |
| `color.surface.darkRaised` | `--color-surface-dark-raised` | `#252D47` |
| `color.surface.brandSubtle` | `--color-surface-brand-subtle` | `#EBECFF` |
| `color.surface.brandMedium` | `--color-surface-brand-medium` | `#FAFAFF` |
| `color.surface.success` | `--color-surface-success` | `#DEF6DF` |
| `color.surface.warning` | `--color-surface-warning` | `#FEF3E0` |
| `color.surface.error` | `--color-surface-error` | `#FFE8EF` |
| `color.surface.info` | `--color-surface-info` | `#EEF9FD` |

### Gradients (resolved)

| Token | CSS value |
|---|---|
| `gradient.brand` | `linear-gradient(135deg, #FF3F7B 0%, #5A60F6 100%)` |
| `gradient.dark` | `linear-gradient(135deg, #33405E 0%, #1B2139 100%)` |
| `gradient.purpleSoft` | `linear-gradient(135deg, #EBECFF 0%, #F4F4FF 60%, #FFFFFF 100%)` |
| `gradient.glowPurple` | `radial-gradient(ellipse 80% 60% at 70% -10%, rgba(90,96,246,0.22) 0%, transparent 65%)` |
| `gradient.glowPink` | `radial-gradient(ellipse 60% 50% at 30% 110%, rgba(255,63,123,0.16) 0%, transparent 60%)` |
| `gradient.glowGreen` | `radial-gradient(ellipse 80% 60% at 70% -10%, rgba(82,204,87,0.18) 0%, transparent 65%)` |

### Radius Aliases (resolved)

| Alias | Resolved | Usage |
|---|---|---|
| `radius.none` | `0px` | |
| `radius.xs` | `2px` | |
| `radius.sm` | `4px` | |
| `radius.md` | `6px` | small buttons, nav links |
| **`radius.lg`** | **`8px`** | **CTA buttons, inputs** |
| `radius.xl` | `12px` | cards |
| `radius.2xl` | `16px` | hero blocks |
| `radius.full` | `9999px` | tags, badges, toggles |

### Focus Rings

| Token | Value | Usage |
|---|---|---|
| `focus.ring` | `0 0 0 3px rgba(90,96,246,0.45)` | `box-shadow` style (most components) |
| `focus.ringInput` | `0 0 0 3px rgba(90,96,246,0.15)` | `box-shadow` style on input fields |
| `focus.ringDark` | `0 0 0 3px rgba(255,255,255,0.55)` | `box-shadow` on dark surfaces |
| `focus.ringOffset` | `2px` | `outline-offset` value |
| `focus.ringDefault` | `#5A60F6` | solid color for `outline: 3px solid …` style focus (e.g. segmented toggle) |

---

## 3. Maps Collection

Component-level token decisions. Where semantic tokens are assigned to specific component properties.

### Typography Scale (fully resolved)

All styles: `font-family: DM Sans, sans-serif` · `font-variation-settings: 'opsz' 14`

| Style | Class | Size | Line-height | Weight | Letter-spacing | Usage |
|---|---|---|---|---|---|---|
| Display XL | `.text-display-xl` | 80px | 96px | 400 | −3px | Full-bleed hero, one per page |
| Display | `.text-display` | 64px | 80px | 400 | −2px | Hero headline |
| H1 | `.text-h1` | 48px | 64px | 400 | −2px | Page title, one per page |
| H2 | `.text-h2` | 40px | 56px | 400 | −2px | Section headline |
| H3 | `.text-h3` | 32px | 40px | 400 | −2px | Sub-section, card headlines |
| H4 | `.text-h4` | 28px | 36px | 400 | −1px | Modal/card/sidebar headings |
| H5 | `.text-h5` | 24px | 32px | 400 | −1px | Settings panels, group labels |
| H6 | `.text-h6` | 20px | 28px | 400 | 0 | Accordion triggers, sub-labels |
| SH1 | `.text-sh1` | 32px | 44px | 400 | −2px | Editorial subheading (looser leading than H3) |
| SH2 | `.text-sh2` | 28px | 40px | 400 | −1px | Marketing sub-section |
| SH3 | `.text-sh3` | 24px | 36px | 400 | −1px | Content column subheading |
| P1 | `.text-p1` | 20px | 32px | 400 | 0 | Hero body copy |
| P2 | `.text-p2` | 18px | 28px | 400 | 0 | Editorial body copy |
| P | `.text-p` | 16px | 24px | 400 | 0 | Default UI body |
| LAB1 | `.text-lab1` | 14px | 24px | 500 | 0 | Form labels, table headers |
| LAB2 | `.text-lab2` | 12px | 20px | 700 | 0.06em | Overlines, tags (always uppercase) |

### Button Component (fully resolved)

**Base:** `font-family: DM Sans` · `font-weight: 500` · `line-height: 1`

#### Sizes

| Size | Padding | Font size | Radius | Tailwind |
|---|---|---|---|---|
| Large | `18px 32px` | `18px` | `8px` | `.cta-large` |
| Medium | `16px 32px` | `16px` | `8px` | `.cta-medium` |
| Small | `12px 24px` | `14px` | `6px` | `.cta-small` |

#### Variants

| Variant | Background | Text color | Border | Notes |
|---|---|---|---|---|
| `primary` | `linear-gradient(90deg, #FF3F7B 0%, #5A60F6 100%)` | `#FFFFFF` | none | Hero CTAs only. P1 priority. |
| `purple` | `#5A60F6` | `#FFFFFF` | none | Standard primary action. |
| `white` | `#FFFFFF` | `#33405E` | none | On dark backgrounds. |
| `outline` | `#FFFFFF` | `#5A60F6` | `2px solid #5A60F6` | Secondary action on light bg. |
| `altPurple` | `#EBECFF` | `#5259E0` | none | Soft secondary action. |
| `textLink` | transparent | `#FF3F7B` | none | Font-weight 700. |
| `textLinkPurple` | transparent | `#5A60F6` | none | Font-weight 700. |

#### Hover / Active states
```css
.btn:hover  { filter: brightness(0.92); transform: translateY(-1px); }
.btn:active { filter: brightness(0.85); transform: translateY(0); }
.btn:disabled { opacity: 0.45; cursor: not-allowed; filter: none; transform: none; }
```

### Card Component (fully resolved)

| Property | Light card | Dark card |
|---|---|---|
| Background | `#FFFFFF` | `#252D47` |
| Border | `1px solid #E5E6EA` | `1px solid rgba(255,255,255,0.10)` |
| Border radius | `16px` | `16px` |
| Box shadow | `elevation-1` | none |

### Input Component (fully resolved)

| Property | Value |
|---|---|
| Background | `#FFFFFF` |
| Border | `1.5px solid #E5E6EA` |
| Border radius | `8px` |
| Height | `48px` |
| Font | `DM Sans, 16px, weight 400` |
| Padding | `0 16px` (textarea: `12px 16px`) |
| Text color | `#3A3D5C` |
| Placeholder color | `#9596A7` |
| Focus border | `#5A60F6` |
| Focus ring | `box-shadow: 0 0 0 3px rgba(90,96,246,0.15)` |
| Error border | `#FF3F7B` |
| Error ring | `box-shadow: 0 0 0 3px rgba(255,63,123,0.12)` |
| Disabled | `background: #F7F7F8; color: #9596A7; border-color: #F7F7F8` |

### Tag / Badge Component (fully resolved)

Tags come in two types and three size tiers. **Status tags** are bold system labels. **Content tags** are softer category classifiers. All use `border-radius: 9999px`.

#### Type 1 — Status & Badge Tags

**Base (`.tag`):** `padding: 4px 12px` · `font-size: 12px` · `font-weight: 700` · `text-transform: uppercase` · `letter-spacing: 0.3px`

Use for: system states, feature flags, bold labels (New, Beta, Pro, From our customers).

| Variant | Background | Text |
|---|---|---|
| `purple` | `#5A60F6` | `#FFFFFF` |
| `pink` | `#BE2257` | `#FFFFFF` |
| `green` | `#DEF6DF` | `#1B6B1F` |
| `orange` | `#AE5D07` | `#FFFFFF` |
| `info` | `#6BCEEB` | `#3A3D5C` |
| `navy` | `#33405E` | `#FFFFFF` |
| `outlinePurple` | `#EBECFF` | `#5259E0` + border `1px solid #CFD1FE` |
| `outlinePink` | `#FFE8EF` | `#BE2257` + border `1px solid #FFC3D6` |

#### Type 2 — Content & Category Tags

**Base (`.content-tag`):** `padding: 3px 10px` · `font-size: 11px` · `font-weight: 500` · `text-transform: none` (sentence case) · `letter-spacing: 0.02em`

Use for: blog categories, card labels, inline content classifiers (Product, Case study, Guide).

| Variant | Background | Text |
|---|---|---|
| `purple` | `#EBECFF` | `#5A60F6` |
| `pink` | `#FFE8EF` | `#FF3F7B` |
| `green` | `#DEF6DF` | `#1B6B1F` |

**Section overline modifier (`.content-tag-section`):** `padding: 5px 14px` · `font-size: 12px` · `font-weight: 600`

Use for: section headings on landing pages where the tag sits above a large H2 and needs more visual weight. Keeps sentence case and soft colours — distinguishes from Status tags by not being uppercase/bold. Apply alongside the base `.content-tag` class.

### Navbar Component (fully resolved)

| Property | Value |
|---|---|
| Background | `#FFFFFF` |
| Border bottom | `1px solid #E5E6EA` |
| Link color | `#33405E` |
| Link hover color | `#FF3F7B` |
| Link font-size | `15px` |
| Link font-weight | `500` |
| Link border-radius | `6px` |
| Desktop height | `72px` |
| Mobile height | `56px` |

### Icon Sizes

| Token | Size | Usage |
|---|---|---|
| `icon.xs` | `14px` | inline with LAB1/LAB2 |
| `icon.sm` | `16px` | inline with body text |
| `icon.md` | `20px` | standard UI icon |
| `icon.lg` | `24px` | feature icons, nav icons |
| `icon.xl` | `32px` | decorative feature icons |
| `icon.2xl` | `48px` | large illustrative icons |

Icon library: **Hugeicons**. Class pattern: `hgi-stroke hgi-{name}`.

---

## 4. Responsive Collection

Three breakpoints: **mobile (< 768px)**, **tablet (768–1023px)**, **desktop (≥ 1024px)**.

### Grid

| Property | Mobile (<768) | Tablet (768–1023) | Desktop (≥1024) |
|---|---|---|---|
| Columns | 4 | 8 | 12 |
| Gap (gutter) | `16px` | `24px` | `24px` |
| Margin (padding X) | `20px` | `32px` | `48px` |

Desktop content caps at **1200px** (centered); below that it's fluid with the margins above. Figma grid styles: `Grid/Mobile`, `Grid/Tablet`, `Grid/Desktop`, plus `Grid/Baseline-8px` (8px baseline helper). Column counts follow the Material 4/8/12 standard — a 3-up row (4 cols each on desktop) becomes 2-up on tablet (8 cols) and 1-up on mobile (4 cols).

### Content Widths

| Name | Value | Usage |
|---|---|---|
| `standard` | `1200px` | features, pricing, testimonials, most sections |
| `narrow` | `760px` | blog posts, articles, centered CTAs |
| full-bleed | `100%` | hero backgrounds, decorative bands |

Section backgrounds bleed full-width. Content inside always uses a `1200px` inner wrapper.

### Section Spacing

| Context | Mobile | Desktop |
|---|---|---|
| Hero / major divider (py) | `80px` | `160px` |
| Standard section (py) | `64px` | `120px` |
| Sub-section / feature block | `48px` | `80px` |
| Tight group within section | `32px` | `48px` |

### Responsive Typography (resolved)

| Style | Desktop | Mobile |
|---|---|---|
| Display XL | `80px / 96px / −3px` | `40px / 48px / −2px` |
| Display | `64px / 80px / −2px` | `36px / 44px / −2px` |
| H1 | `48px / 64px / −2px` | `32px / 40px / −1.5px` |
| H2 | `40px / 56px / −2px` | `28px / 36px / −1px` |
| H3 | `32px / 40px / −2px` | `24px / 32px / −1px` |
| H4 | `28px / 36px / −1px` | `22px / 30px / −0.5px` |
| H5 | `24px / 32px / −1px` | `20px / 28px / −0.5px` |
| H6 | `20px / 28px / 0` | `18px / 26px / 0` |
| P1 | `20px / 32px` | `18px / 28px` |
| P2 | `18px / 28px` | `16px / 24px` |
| P | `16px / 24px` | `15px / 24px` |

### Responsive Buttons

| Size | Desktop padding | Mobile padding | Desktop font | Mobile font |
|---|---|---|---|---|
| Large | `18px 32px` | `14px 24px` | `18px` | `16px` |
| Medium | `16px 32px` | `14px 24px` | `16px` | `15px` |

---

## CSS Custom Properties

Complete `:root` declaration. Paste this into your global stylesheet.

```css
:root {
  /* ── Brand ─────────────────────────────────── */
  --color-brand-primary:          #5A60F6;
  --color-brand-primary-light:    #9699FC;
  --color-brand-secondary:        #33405E;
  --color-brand-accent:           #FF3F7B;
  --color-brand-accent-light:     #FF9EBE;

  /* ── Text ──────────────────────────────────── */
  --color-text-primary:           #3A3D5C;
  --color-text-secondary:         #5D6079;
  --color-text-disabled:          #9596A7;
  --color-text-inverse:           #FFFFFF;
  --color-text-on-dark:           #FFFFFF;
  --color-text-on-dark-secondary: #C9CFE5;
  --color-text-on-dark-muted:     #8CA5C3;
  --color-text-on-brand-subtle:   #5259E0;
  --color-text-on-success:        #1B6B1F;
  --color-text-on-warning:        #884705;
  --color-text-on-error:          #BE2257;
  --color-text-on-info:           #12728E;
  --color-text-on-stars:          #B45309;

  /* ── Surfaces ──────────────────────────────── */
  --color-surface-page:           #FFFFFF;
  --color-surface-card:           #FBFBFC;
  --color-surface-chrome:         #EFEFF2;
  --color-surface-hover:          #F7F7F8;
  --color-surface-dark:           #1B2139;
  --color-surface-dark-raised:    #252D47;
  --color-surface-brand-subtle:   #EBECFF;
  --color-surface-brand-medium:   #FAFAFF;
  --color-surface-success:        #DEF6DF;
  --color-surface-warning:        #FEF3E0;
  --color-surface-error:          #FFE8EF;
  --color-surface-info:           #EEF9FD;
  --color-surface-stars:          #FFF8E7;

  /* ── Borders ───────────────────────────────── */
  --color-border-default:         #E5E6EA;
  --color-border-subtle:          #F7F7F8;
  --color-border-on-dark:         rgba(255, 255, 255, 0.10);

  /* ── Status ────────────────────────────────── */
  --color-status-success:         #52CC57;
  --color-status-warning:         #F58B0B;
  --color-status-error:           #FF3F7B;
  --color-status-info:            #6BCEEB;
  --color-status-stars:           #F59E0B;

  /* ── Overlay ───────────────────────────────── */
  --color-overlay-hover:          rgba(51, 64, 94, 0.15);

  /* ── Gradients ─────────────────────────────── */
  --gradient-brand:       linear-gradient(135deg, #FF3F7B 0%, #5A60F6 100%);
  --gradient-dark:        linear-gradient(135deg, #33405E 0%, #1B2139 100%);
  --gradient-purple-soft: linear-gradient(135deg, #EBECFF 0%, #F4F4FF 60%, #FFFFFF 100%);
  --gradient-glow-purple: radial-gradient(ellipse 80% 60% at 70% -10%, rgba(90,96,246,0.22) 0%, transparent 65%);
  --gradient-glow-pink:   radial-gradient(ellipse 60% 50% at 30% 110%, rgba(255,63,123,0.16) 0%, transparent 60%);
  --gradient-glow-green:  radial-gradient(ellipse 80% 60% at 70% -10%, rgba(82,204,87,0.18) 0%, transparent 65%);

  /* ── Spacing ───────────────────────────────── */
  --spacing-0:  0px;
  --spacing-1:  4px;
  --spacing-2:  8px;
  --spacing-3:  12px;
  --spacing-4:  16px;
  --spacing-5:  24px;
  --spacing-6:  32px;
  --spacing-7:  40px;
  --spacing-8:  48px;
  --spacing-9:  64px;
  --spacing-10: 80px;
  --spacing-11: 96px;
  --spacing-12: 128px;

  /* ── Border Radius ─────────────────────────── */
  --radius-0:    0px;
  --radius-1:    2px;
  --radius-2:    4px;
  --radius-3:    6px;
  --radius-4:    8px;
  --radius-5:    12px;
  --radius-6:    16px;
  --radius-pill: 9999px;

  /* ── Elevation ─────────────────────────────── */
  --elevation-1: 0px 1px 1px rgba(51,64,94,0.08), 0px 2px 2px 1px rgba(51,64,94,0.08);
  --elevation-2: 0px 2px 2px rgba(51,64,94,0.08), 0px 4px 4px rgba(51,64,94,0.08), 0px 8px 8px rgba(51,64,94,0.08);
  --elevation-3: 0px 4px 4px rgba(51,64,94,0.08), 0px 8px 8px rgba(51,64,94,0.08), 0px 16px 16px rgba(51,64,94,0.08);
  --elevation-4: 0px 4px 4px rgba(51,64,94,0.08), 0px 8px 8px rgba(51,64,94,0.08), 0px 16px 16px rgba(51,64,94,0.08), 0px 32px 32px rgba(51,64,94,0.08);

  /* ── Focus Rings ───────────────────────────── */
  --focus-ring:        0 0 0 3px rgba(90, 96, 246, 0.45);
  --focus-ring-input:  0 0 0 3px rgba(90, 96, 246, 0.15);
  --focus-ring-dark:   0 0 0 3px rgba(255, 255, 255, 0.55);
  --focus-ring-offset: 2px;

  /* ── Motion ────────────────────────────────── */
  --duration-fast:   150ms;
  --duration-normal: 250ms;
  --duration-slow:   400ms;
  --ease-out:        cubic-bezier(0.0,  0.0,  0.2, 1);
  --ease-in:         cubic-bezier(0.4,  0.0,  1.0, 1);
  --ease-in-out:     cubic-bezier(0.4,  0.0,  0.2, 1);
  --ease-spring:     cubic-bezier(0.34, 1.56, 0.64, 1);

  /* ── Z-Index ───────────────────────────────── */
  --z-base:     0;
  --z-raised:   10;
  --z-dropdown: 100;
  --z-sticky:   200;
  --z-overlay:  300;
  --z-modal:    400;
  --z-toast:    500;
  --z-tooltip:  600;
}
```

---

## Tailwind Config

```js
// tailwind.config.js
module.exports = {
  theme: {
    extend: {
      colors: {
        brand: {
          primary:   'var(--color-brand-primary)',   // #5A60F6
          secondary: 'var(--color-brand-secondary)', // #33405E
          accent:    'var(--color-brand-accent)',    // #FF3F7B
        },
        text: {
          primary:   'var(--color-text-primary)',
          secondary: 'var(--color-text-secondary)',
          disabled:  'var(--color-text-disabled)',
          inverse:   'var(--color-text-inverse)',
        },
        surface: {
          page:        'var(--color-surface-page)',
          card:        'var(--color-surface-card)',
          chrome:      'var(--color-surface-chrome)',
          dark:        'var(--color-surface-dark)',
          darkRaised:  'var(--color-surface-dark-raised)',
          brandSubtle: 'var(--color-surface-brand-subtle)',
          success:     'var(--color-surface-success)',
          warning:     'var(--color-surface-warning)',
          error:       'var(--color-surface-error)',
          info:        'var(--color-surface-info)',
        },
        border: {
          DEFAULT: 'var(--color-border-default)',
          subtle:  'var(--color-border-subtle)',
        },
        status: {
          success: 'var(--color-status-success)',
          warning: 'var(--color-status-warning)',
          error:   'var(--color-status-error)',
          info:    'var(--color-status-info)',
        },
      },
      fontFamily: {
        sans: ['DM Sans', 'sans-serif'],
      },
      fontSize: {
        'display-xl': ['80px', { lineHeight: '96px', letterSpacing: '-3px' }],
        'display':    ['64px', { lineHeight: '80px', letterSpacing: '-2px' }],
        'h1':         ['48px', { lineHeight: '64px', letterSpacing: '-2px' }],
        'h2':         ['40px', { lineHeight: '56px', letterSpacing: '-2px' }],
        'h3':         ['32px', { lineHeight: '40px', letterSpacing: '-2px' }],
        'h4':         ['28px', { lineHeight: '36px', letterSpacing: '-1px' }],
        'h5':         ['24px', { lineHeight: '32px', letterSpacing: '-1px' }],
        'h6':         ['20px', { lineHeight: '28px', letterSpacing: '0' }],
        'p1':         ['20px', { lineHeight: '32px' }],
        'p2':         ['18px', { lineHeight: '28px' }],
        'p':          ['16px', { lineHeight: '24px' }],
        'lab1':       ['14px', { lineHeight: '24px' }],
        'lab2':       ['12px', { lineHeight: '20px', letterSpacing: '0.06em' }],
      },
      spacing: {
        '1':  '4px',
        '2':  '8px',
        '3':  '12px',
        '4':  '16px',
        '5':  '24px',
        '6':  '32px',
        '7':  '40px',
        '8':  '48px',
        '9':  '64px',
        '10': '80px',
        '11': '96px',
        '12': '128px',
      },
      borderRadius: {
        'none': '0px',
        'xs':   '2px',
        'sm':   '4px',
        'md':   '6px',
        'lg':   '8px',   // buttons, inputs
        'xl':   '12px',  // cards
        '2xl':  '16px',  // hero blocks
        'full': '9999px', // tags, badges only
      },
      boxShadow: {
        'elevation-1': 'var(--elevation-1)',
        'elevation-2': 'var(--elevation-2)',
        'elevation-3': 'var(--elevation-3)',
        'elevation-4': 'var(--elevation-4)',
      },
      screens: {
        'md': '768px',  // tablet
        'lg': '1024px', // desktop
      },
    },
  },
}
```

---

## Code Examples

### Button variants

```html
<!-- Primary gradient CTA (hero sections only) -->
<button class="btn cta-primary cta-large">Get started free</button>

<!-- Standard purple CTA -->
<button class="btn cta-purple cta-medium">Start building</button>

<!-- Outline (secondary action) -->
<button class="btn cta-outline cta-medium">See pricing</button>

<!-- White (on dark backgrounds) -->
<button class="btn cta-white cta-medium">Learn more</button>

<!-- Soft purple (tertiary) -->
<button class="btn cta-alt-purple cta-medium">View docs</button>

<!-- Text links -->
<button class="btn cta-textlink">Learn more →</button>
<button class="btn cta-textlink-purple">See all features →</button>
```

```css
/* Button base */
.btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
  font-family: 'DM Sans', sans-serif;
  font-variation-settings: 'opsz' 14;
  font-weight: 500;
  line-height: 1;
  border: none;
  cursor: pointer;
  text-decoration: none;
  white-space: nowrap;
  transition: filter var(--duration-fast) var(--ease-out),
              transform var(--duration-fast) var(--ease-out);
}
.btn:hover  { filter: brightness(0.92); transform: translateY(-1px); }
.btn:active { filter: brightness(0.85); transform: translateY(0); }
.btn:disabled, .btn[aria-disabled="true"] {
  opacity: 0.45;
  cursor: not-allowed;
  filter: none;
  transform: none;
}

/* Sizes */
.cta-large  { padding: 18px 32px; border-radius: var(--radius-4); font-size: 18px; }
.cta-medium { padding: 16px 32px; border-radius: var(--radius-4); font-size: 16px; }
.cta-small  { padding: 12px 24px; border-radius: var(--radius-3); font-size: 14px; }

/* Variants */
.cta-primary    { background: linear-gradient(90deg, var(--color-brand-accent) 0%, var(--color-brand-primary) 100%); color: #fff; letter-spacing: -0.36px; }
.cta-purple     { background: var(--color-brand-primary); color: #fff; letter-spacing: -0.36px; }
.cta-white      { background: #fff; color: var(--color-brand-secondary); letter-spacing: -0.24px; }
.cta-outline    { background: #fff; color: var(--color-brand-primary); border: 2px solid var(--color-brand-primary); }
.cta-alt-purple { background: var(--color-surface-brand-subtle); color: var(--color-text-on-brand-subtle); }
.cta-textlink        { background: transparent; color: var(--color-brand-accent); font-weight: 700; padding: 0; }
.cta-textlink-purple { background: transparent; color: var(--color-brand-primary); font-weight: 700; padding: 0; }
```

### Dark section

```css
.section-dark {
  background: var(--color-surface-dark);
  position: relative;
}
/* Purple glow overlay */
.section-dark::before {
  content: '';
  position: absolute;
  inset: 0;
  background: var(--gradient-glow-purple);
  pointer-events: none;
}

/* Text on dark */
.section-dark h2 { color: var(--color-text-on-dark); }          /* #FFFFFF */
.section-dark p  { color: var(--color-text-on-dark-secondary); } /* #C9CFE5 */
.section-dark .overline { color: var(--color-text-on-dark-muted); } /* #8CA5C3 */
```

### Gradient text (hero H1 only)

```css
.gradient-text {
  background: var(--gradient-brand);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}
```

### Card

```css
.card {
  background: var(--color-surface-page);
  border: 1px solid var(--color-border-default);
  border-radius: var(--radius-6);
  box-shadow: var(--elevation-1);
}
.card-dark {
  background: var(--color-surface-dark-raised);
  border: 1px solid var(--color-border-on-dark);
}
```

### Input

```css
.form-input {
  background: var(--color-surface-page);
  border: 1.5px solid var(--color-border-default);
  border-radius: var(--radius-4);
  height: 48px;
  padding: 0 16px;
  font-family: 'DM Sans', sans-serif;
  font-size: 16px;
  color: var(--color-text-primary);
  transition: border-color var(--duration-fast) var(--ease-out),
              box-shadow var(--duration-fast) var(--ease-out);
}
textarea.form-input { height: auto; padding: 12px 16px; resize: vertical; min-height: 100px; line-height: 24px; }
.form-input::placeholder { color: var(--color-text-disabled); }
.form-input:focus {
  outline: none;
  border-color: var(--color-brand-primary);
  box-shadow: var(--focus-ring-input);
}
.form-input.is-error {
  border-color: var(--color-brand-accent);
  box-shadow: 0 0 0 3px rgba(255, 63, 123, 0.12);
}
.form-input:disabled {
  background: var(--color-surface-hover);
  color: var(--color-text-disabled);
  border-color: var(--color-border-subtle);
  cursor: not-allowed;
}
```

### Responsive typography

```css
/* All headings: always DM Sans, weight 400, negative tracking */
h1, .text-h1 {
  font-family: 'DM Sans', sans-serif;
  font-variation-settings: 'opsz' 14;
  font-weight: 400;
  font-size: 32px;          /* mobile */
  line-height: 40px;
  letter-spacing: -1.5px;
}
@media (min-width: 768px) {
  h1, .text-h1 {
    font-size: 48px;
    line-height: 64px;
    letter-spacing: -2px;
  }
}

h2, .text-h2 {
  font-size: 28px; line-height: 36px; letter-spacing: -1px;    /* mobile */
}
@media (min-width: 768px) {
  h2, .text-h2 { font-size: 40px; line-height: 56px; letter-spacing: -2px; }
}
```

### Tag / Badge

```css
.tag {
  display: inline-flex;
  align-items: center;
  padding: 4px 12px;
  border-radius: var(--radius-pill);
  font-size: 12px;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.3px;
}
.tag-purple { background: var(--color-brand-primary);       color: #fff; }
.tag-green  { background: var(--color-surface-success);     color: var(--color-text-on-success); }
.tag-orange { background: #AE5D07;                          color: #fff; }
.tag-info   { background: var(--color-status-info);         color: var(--color-text-primary); }
.tag-outline-purple { background: var(--color-surface-brand-subtle); color: var(--color-text-on-brand-subtle); border: 1px solid #CFD1FE; }
```

---

## Usage Guidelines

### Rules AI tools must follow

**Colors**
- Never use raw hex values in components. Always use `var(--color-*)`.
- `--color-brand-accent` (`#FF3F7B`) for CTAs, accents, and error-adjacent actions. Not a general error color — use `--color-status-error` for that.
- `--color-text-on-brand-subtle` (`#5259E0`) — not `--color-brand-primary` — when text sits on `--color-surface-brand-subtle`. The primary purple fails contrast there.
- On dark backgrounds, use `--color-text-on-dark` for headings and `--color-text-on-dark-secondary` for body text. Never `--color-text-primary`.

**Typography**
- Font weight on headings is **400**. Bold (700) is only for `LAB2`, `tag`, inline emphasis, and text links.
- Always include `font-variation-settings: 'opsz' 14` on DM Sans elements.
- Gradient text (`background-clip: text`) only on hero H1 or Display. Never on body copy or subheadings.

**Buttons**
- Primary gradient button is **hero CTAs only**. One per above-the-fold section.
- All CTA buttons use `--radius-4` (8px). Never `--radius-pill` on buttons.
- Disabled state: `opacity: 0.45`. Do not change colors on disabled — only opacity.

**Radius**
- `--radius-pill` (9999px) is **exclusively** for tags, badges, toggle tracks, and pill-shaped decorative elements.
- Cards use `--radius-6` (16px). Hero blocks use `--radius-6` (16px).

**Spacing**
- Section vertical padding: `64px` mobile / `120px` desktop. Hero sections: `80px` / `160px`.
- Never use arbitrary spacing values. Always reference `--spacing-*` tokens.

**Responsive**
- Three breakpoints, mobile-first: base (mobile), `md:` `768px` (tablet), `lg:` `1024px` (desktop). Grid is **4 / 8 / 12** columns. Avoid `sm:`/`xl:`/`2xl:` unless a real need arises.
- On mobile, full-width CTA buttons inside hero/banner sections only.

**Dark sections**
- Dark background: `--color-surface-dark` (`#1B2139`).
- Cards on dark: `--color-surface-dark-raised` (`#252D47`) with `--color-border-on-dark` border.
- Never use `--color-surface-card` or light borders on dark sections.

**Icons**
- Always use Hugeicons with `hgi-stroke hgi-{name}`. Never `hgi-stroke-rounded`.
- Never serve icon pages via `file://` — always via HTTP.
