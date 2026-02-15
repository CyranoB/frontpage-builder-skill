# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Landing Page Builder is a Claude Code skill (plugin) that generates self-contained landing pages from natural-language descriptions and deploys them to Vercel using claimable deployments (no auth required). It's distributed via the Claude Code plugin marketplace.

## Architecture

This is a no-build, no-dependencies project. There is no package.json, no compilation step, and no test framework. The entire skill is defined through markdown instructions and a bash deployment script.

```
.claude-plugin/
├── plugin.json            # Plugin manifest (name, version, description)
└── marketplace.json       # Marketplace catalog entry (owner, keywords, category)
skills/landing-page-builder/
├── SKILL.md               # Core skill: workflow steps and design instructions
├── scripts/deploy.sh      # Bash script that tars and POSTs to Vercel's deploy API
└── references/web-design-guidelines.md  # Accessibility/UX compliance rules
```

**Skill workflow (defined in SKILL.md):**
1. Gather context from user's description
2. Choose a bold, distinctive design direction (never generic)
3. Generate a single `index.html` with inline CSS/JS to `/tmp/landing-page/`
4. Run `deploy.sh` to package and deploy to Vercel, returning preview + claim URLs

**Deployment:** `scripts/deploy.sh` creates a tarball and POSTs it to `https://claude-skills-deploy.vercel.com/api/deploy`. No API keys needed.

## Key Design Constraints

- Generated pages must use **distinctive aesthetics** — no generic AI patterns (purple gradients, card grids, Inter/Roboto fonts)
- All HTML must be **accessible**: semantic elements, ARIA labels, keyboard navigation, `prefers-reduced-motion` support
- Pages are **fully self-contained**: single HTML file with inline CSS/JS and Google Fonts via CDN
- The `marketplace.json` `source` field must be `"./"` (with trailing slash) to pass schema validation

## Installation & Testing

Install in Claude Code:
```
/plugin marketplace add CyranoB/frontpage-builder-skill
/plugin install landing-page-builder@frontpage-builder-skill
```

To test the skill, prompt Claude Code with something like:
```
Build me a landing page for a dog walking app called PawPals
```
