# Web Design Guidelines for Landing Pages

Apply these rules when generating landing page HTML/CSS/JS.

## Accessibility

- Icon-only buttons need `aria-label`
- Form controls need `<label>` or `aria-label`
- Interactive elements need keyboard handlers (`onKeyDown`/`onKeyUp`)
- `<button>` for actions, `<a>` for navigation (not `<div onClick>`)
- Images need `alt` (or `alt=""` if decorative)
- Decorative icons need `aria-hidden="true"`
- Use semantic HTML (`<button>`, `<a>`, `<label>`, `<table>`) before ARIA
- Headings hierarchical `<h1>`–`<h6>`; include skip link for main content
- `scroll-margin-top` on heading anchors

## Icons

- Load icon libraries via CDN `<script>` or `<link>` (consistent with Google Fonts pattern)
- Use one icon library per page for visual consistency (Lucide, Phosphor, or Tabler)
- Icon-only buttons need `aria-label`; decorative icons need `aria-hidden="true"`
- Size icons consistently using CSS (`font-size` for webfonts, `width`/`height` for SVG)
- Match icon stroke weight to typography weight when possible

## Focus States

- Interactive elements need visible focus: `outline` or `box-shadow` on `:focus-visible`
- Never `outline: none` without a focus replacement
- Use `:focus-visible` over `:focus` (avoid focus ring on click)

## Forms

- Inputs need `autocomplete` and meaningful `name`
- Use correct `type` (`email`, `tel`, `url`) and `inputmode`
- Never block paste
- Labels clickable (`for` attribute or wrapping control)
- Disable spellcheck on emails/codes (`spellcheck="false"`)
- Submit button stays enabled until request starts; spinner during request
- Errors inline next to fields
- Placeholders end with `…` and show example pattern

## Animation

- Honor `prefers-reduced-motion` (provide reduced variant or disable)
- Animate `transform`/`opacity` only (compositor-friendly)
- Never `transition: all` — list properties explicitly
- Set correct `transform-origin`
- Animations should be interruptible

## Typography

- `…` not `...`
- Curly quotes `"` `"` not straight `"`
- Non-breaking spaces: `10&nbsp;MB`, `⌘&nbsp;K`
- Loading states end with `…`
- `font-variant-numeric: tabular-nums` for number columns
- Use `text-wrap: balance` or `text-pretty` on headings

## Content Handling

- Text containers handle long content: `text-overflow: ellipsis`, `overflow-wrap: break-word`, or `-webkit-line-clamp`
- Handle empty states — don't render broken UI for empty data
- Anticipate short, average, and very long user-generated content

## Images

- `<img>` needs explicit `width` and `height` (prevents CLS)
- Below-fold images: `loading="lazy"`
- Above-fold hero images: `fetchpriority="high"`

## Performance

- Add `<link rel="preconnect">` for CDN/font domains
- Critical fonts: `<link rel="preload" as="font">` with `font-display: swap`
- Minimize render-blocking resources

## Touch & Interaction

- `touch-action: manipulation` on interactive elements (prevents double-tap delay)
- Hover states: buttons/links need `hover:` visual feedback
- Interactive states increase contrast: hover/active/focus more prominent than rest

## Dark Mode & Theming

- If using dark theme: `color-scheme: dark` on `<html>`
- `<meta name="theme-color">` matches page background

## Content & Copy

- Active voice: "Get started" not "Getting started will be possible"
- Title Case for headings/buttons
- Numerals for counts: "8 features" not "eight features"
- Specific button labels: "Start Free Trial" not "Continue"
- `&` over "and" where space-constrained

## Anti-patterns to Avoid

- `user-scalable=no` or `maximum-scale=1` disabling zoom
- `transition: all`
- `outline: none` without `:focus-visible` replacement
- `<div>` or `<span>` with click handlers (should be `<button>`)
- Images without dimensions
- Form inputs without labels
- Icon buttons without `aria-label`
- Hardcoded date/number formats (use `Intl.*`)
