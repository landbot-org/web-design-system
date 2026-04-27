# Landbot Web Design System

The single source of truth for Landbot's marketing website. Tokens, components, and patterns, plus a Claude skill so the design system applies automatically when you use Claude to build or review web work.

Maintainer: [@niklaspuertolas-cmd](https://github.com/niklaspuertolas-cmd) (Niklas Puertolas).

## What's in this repo

```
tokens/
  DESIGN-SYSTEM-REFERENCE.md   Canonical token reference. Read this first when using tokens.
  01-primitives.json           Raw values: every hex, every px, every duration.
  02-semantic.json             Named aliases (e.g. brand.primary → primitives.purple.500).
  03-maps.json                 Component-level decisions (button sizes, card specs).
  04-responsive.json           Mobile vs desktop overrides.
docs/
  index.html                   The full live showcase. Sidebar nav, all tokens, all components.
  components/                  CSS+HTML snippets for each component (extracted from index.html).
  assets/                      Local image files referenced by index.html (logos, icons, etc.).
SKILL.md                       The Claude skill definition. Loaded automatically when installed.
```

## Browse the design system

Hosted at: **https://landbot.github.io/web-design-system/**

You must be signed in to GitHub and a member of the `landbot-org` organization to view it. If you can see this README, you can see the hosted version.

## Use it in Claude

This repo doubles as a Claude skill. Once installed, Claude will automatically apply Landbot's design tokens and components whenever you ask it to build or review web UI for Landbot.

### Install (one-time setup)

1. Clone the repo to your machine:
   ```bash
   git clone git@github.com:landbot-org/web-design-system.git ~/landbot/web-design-system
   ```

2. Symlink (or copy) it into your Claude skills folder:
   ```bash
   # Cowork / Claude Desktop
   mkdir -p ~/.claude/skills
   ln -s ~/landbot/web-design-system ~/.claude/skills/landbot-web-design-system

   # Claude Code (per-project)
   mkdir -p .claude/skills
   ln -s ~/landbot/web-design-system .claude/skills/landbot-web-design-system
   ```

3. Restart Claude (or reload the skills list). You should see `landbot-web-design-system` appear in your available skills.

### Stay up to date

```bash
cd ~/landbot/web-design-system && git pull
```

### Use it without installing

If you don't want to install the skill, you can still use the design system inside any Claude project by attaching `docs/index.html` directly, or pasting the hosted URL into a Cowork project (Claude will fetch it via WebFetch as long as you're signed in to GitHub on the same machine — note that this path is unreliable for private Pages sites; the skill route is the recommended approach).

## Use it without Claude

The hosted URL is the human-friendly browseable version. The sidebar navigates between sections.

To copy a component into your own code: open the relevant file in `docs/components/`, copy the HTML and CSS, and make sure your project includes the design tokens (the `:root` block at the top of `docs/index.html`).

## Suggest a change

This repo is read-only for the team. Only the maintainer can edit it directly.

If you spot something missing, broken, or worth changing:

1. **Send Niklas a message** (Slack, email, wherever) describing what you'd change and why.
2. Include before/after screenshots if it's a visual change.
3. Niklas reviews and pushes it.

Tokens are stable contracts. Adding new ones is fine. Renaming or removing them breaks downstream consumers (every Landbot teammate's Claude skill, every Webflow theme, every PR Claude has ever generated). The maintainer reviews these changes carefully.

## License

Internal Landbot project. All rights reserved.
