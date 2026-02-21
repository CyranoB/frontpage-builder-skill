---
name: landing-page-builder
description: Build and deploy polished landing pages to Vercel from a text description. Use when a user asks to "build me a landing page," "create a landing page for my product," "make a website for my startup," "deploy a landing page," or describes a product/service and wants a live page. Generates a single static HTML file with distinctive design and deploys it instantly — no authentication required.
---

# Landing Page Builder

Generate a production-quality static landing page from a user's description and deploy it live to Vercel.

## Workflow

### 1. Gather Context

Extract from the user's description:
- **Product/service** — what it does, who it's for
- **Tone** — professional, playful, bold, minimal, luxury, etc.
- **Sections** — hero, features, pricing, testimonials, CTA, footer
- **Brand** — colors, fonts, logo URL if provided

If the description is vague, ask one focused clarifying question. Do not over-interrogate.

### 2. Design

Tell the user: **"Designing your page…"**

#### 2a. Propose a design direction

Analyze the product, target customers, and tone to recommend **one** design direction that best fits. Draw from this aesthetic spectrum:

- Brutally minimal, maximalist chaos, retro-futuristic, organic/natural, luxury/refined, playful/toy-like, editorial/magazine, brutalist/raw, art deco/geometric, soft/pastel, industrial/utilitarian

Present your recommendation with:
- **Name** — a short evocative label (e.g., "Neon Brutalist", "Warm Editorial")
- **Vibe** — one sentence capturing the feel
- **Key choices** — font pairing direction, color palette mood, layout approach

Ask the user to confirm this direction, or say they'd like to see alternatives. If the user wants alternatives, propose **2–3 different directions** to choose from.

#### 2b. Execute the confirmed direction

Once the user confirms, commit to the direction fully and execute with conviction:

**Typography**: Choose distinctive, characterful fonts from Google Fonts. Never default to Inter, Roboto, Arial, or system fonts. Pair a display font with a refined body font. Every landing page should use different fonts — never converge on the same choices.

**Color**: Commit to a cohesive palette. Define all tokens in a `:root` block at the top of your `<style>` tag before writing any other CSS. Every color and spacing value in the stylesheet must reference a token — no hardcoded hex values or magic pixel sizes outside `:root`.

```css
:root {
  /* Color tokens */
  --color-bg: ...;
  --color-surface: ...;
  --color-text: ...;
  --color-text-muted: ...;
  --color-primary: ...;
  --color-accent: ...;
  --color-border: ...;

  /* Scale tokens */
  --radius: ...;
  --space: ...;        /* base unit; use calc(var(--space) * N) for multiples */

  /* Typography tokens */
  --font-display: ...;
  --font-body: ...;
}
```

Dominant colors with sharp accents outperform timid, evenly-distributed palettes. Vary between light and dark themes across generations.

**Motion**: Focus on high-impact moments — one well-orchestrated page load with staggered reveals (`animation-delay`) creates more delight than scattered micro-interactions. Use scroll-triggered animations and surprising hover states. CSS-only solutions preferred.

**Layout**: Unexpected compositions. Asymmetry. Overlap. Diagonal flow. Grid-breaking elements. Generous negative space OR controlled density.

**Visual texture**: Gradient meshes, noise textures, geometric patterns, layered transparencies, dramatic shadows, decorative borders, grain overlays. No flat white backgrounds by default.

**Anti-slop rule**: Never produce generic AI aesthetics — no purple-gradient-on-white, no card grids with rounded corners and drop shadows, no cookie-cutter hero sections. Each page must feel genuinely designed for its specific context.

**Icons**: Pick one icon library per page based on the design direction:

| Library | Best for | CDN | Usage |
|---------|----------|-----|-------|
| **Lucide** | Minimal, editorial, refined | `<script src="https://unpkg.com/lucide@latest"></script>` | `<i data-lucide="icon-name"></i>` + `lucide.createIcons()` |
| **Phosphor Icons** | Playful, bold, expressive | `<script src="https://cdn.jsdelivr.net/npm/@phosphor-icons/web@2.1.2"></script>` | `<i class="ph ph-icon-name"></i>` (weights: `ph-thin`, `ph-light`, `ph`, `ph-bold`, `ph-fill`, `ph-duotone`) |
| **Tabler Icons** | Feature-heavy, all-rounder (5,400+ icons) | `<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@tabler/icons-webfont@latest/tabler-icons.min.css">` | `<i class="ti ti-icon-name"></i>` |

Match the library to the page's aesthetic. Phosphor's weight variants are especially useful for matching typographic weight. Don't litter the page with icons — use them intentionally for feature lists, navigation, or CTAs. A page with 3 well-placed icons beats one with 20 generic ones.

### 3. Build

Tell the user: **"Building your page…"**

Generate a single `index.html` file. All CSS and JS inline. The file must be self-contained and deployable with no build step.

Structure:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="theme-color" content="...">
  <title>...</title>

  <!-- SEO -->
  <meta name="description" content="...">

  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=...&display=swap" rel="stylesheet">
  <style>/* all CSS here */</style>
</head>
<body>
  <!-- semantic HTML -->
  <script>/* animations, interactions */</script>
</body>
</html>
```

Requirements:
- Fully responsive (mobile-first)
- Load Google Fonts via `<link>` with `font-display: swap`
- `<img>` tags need explicit `width`/`height` and `loading="lazy"` below fold
- Honor `prefers-reduced-motion`
- Semantic HTML: `<header>`, `<main>`, `<section>`, `<footer>`, `<nav>`
- Accessible: form labels, `aria-label` on icon buttons, `:focus-visible` states, skip link
- Include Open Graph (`og:title`, `og:description`, `og:type`) and Twitter Card (`twitter:card`, `twitter:title`, `twitter:description`) meta tags when the page is for a publicly shared product or service. Omit them for personal or internal pages, or if the user opts out.
- Include a `<script type="application/ld+json">` block in `<head>` with structured data matching the page content. Use `Organization` for company/startup pages, `Product` for product launches, `LocalBusiness` for local services, or another appropriate schema.org type. Populate `name`, `description`, and `url` (leave `url` empty — it's filled post-deploy).
- For detailed compliance rules, read `references/web-design-guidelines.md`

Write the file to a temporary project directory.

### 4. Deploy

Deploy immediately after generating the HTML. Use scripts/deploy.sh to deploy the landing page.

Present results:

```
Your landing page is live!

Preview URL: https://...vercel.app
Claim URL:   https://vercel.com/claim-deployment?code=...

Visit the Preview URL to see your page.
To transfer this deployment to your Vercel account, visit the Claim URL.
```

### Network Error Handling

If deployment fails due to network restrictions, tell the user:

```
Deployment failed due to network restrictions. To fix this:
1. Go to https://claude.ai/settings/capabilities
2. Add *.vercel.com to the allowed domains
3. Try again
```
