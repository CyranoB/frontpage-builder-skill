# Landing Page Builder

A [Claude Code skill](https://docs.anthropic.com/en/docs/claude-code/skills) that generates polished, distinctive landing pages from a text description and deploys them live to Vercel — no authentication required.

## What it does

1. Takes a natural-language description of a product, service, or idea
2. Generates a self-contained `index.html` with inline CSS/JS
3. Deploys it instantly to Vercel and returns a live preview URL

## Example prompts

- "Build me a landing page for a dog walking app called PawPals"
- "Create a website for my SaaS product that does invoice automation"
- "Deploy a landing page for a coffee subscription service, dark luxury aesthetic"

## Design philosophy

Every generated page follows an opinionated design approach:

- **No AI slop** — no purple-gradient-on-white, no generic card grids, no cookie-cutter hero sections
- **Bold aesthetics** — each page commits to a specific direction (brutalist, editorial, retro-futuristic, luxury, etc.)
- **Distinctive typography** — characterful Google Fonts pairings, never Inter/Roboto/Arial
- **Production quality** — responsive, accessible, semantic HTML, `prefers-reduced-motion` support

Design guidelines are adapted from [Anthropic's frontend-design skill](https://github.com/anthropics/skills/tree/main/skills/frontend-design) and [Vercel's Web Interface Guidelines](https://github.com/vercel-labs/web-interface-guidelines).

## Skill structure

```
landing-page-builder/
├── SKILL.md                              # Workflow and design instructions
├── scripts/deploy.sh                     # Vercel deployment (claimable, no auth)
└── references/web-design-guidelines.md   # Accessibility and UX compliance rules
```

## Installation

Download `landing-page-builder.skill` from [Releases](../../releases) or from the repo root, then add it to your Claude Code skills.

## Credits

Built on top of:
- [frontend-design](https://github.com/anthropics/skills/tree/main/skills/frontend-design) by Anthropic — aesthetic direction and anti-slop principles
- [web-design-guidelines](https://github.com/vercel-labs/agent-skills/tree/main/skills/web-design-guidelines) by Vercel — accessibility and UX compliance rules
- [vercel-deploy-claimable](https://github.com/vercel-labs/agent-skills/tree/main/skills/claude.ai/vercel-deploy-claimable) by Vercel — zero-auth deployment script

## License

MIT
