# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Is

Static GitHub Pages site for **Sunshine Techworks** (`sunshinetech.com.au`), an AI consulting business registered in Australia. The site serves two purposes:

1. **Company website** - Home, About, and Services pages for the consulting business
2. **PR Notify product page** - Landing page and privacy policy for the PR Notify Slack app

The PR Notify backend/app code lives in a separate repo: `sunshine-techworks/pr-notifier`.

## Development

No build system, package manager, or framework. Plain HTML/CSS with minimal inline JS, served by GitHub Pages from `main`.

To preview locally, open any `.html` file in a browser or use a static file server (e.g. `python3 -m http.server`).

## Deployment

Pushing to `main` deploys automatically via GitHub Pages. Custom domain `sunshinetech.com.au` is configured via the `CNAME` file. There is no CI pipeline.

## Site Structure

### Company pages (shared `styles.css`)
- `index.html` - Company homepage with hero, services overview, differentiators, CTA
- `about.html` - Company story, values, approach timeline
- `services.html` - 4 service detail sections + Formspree contact form
- `styles.css` - Shared design system (all CSS variables, components, responsive breakpoints)
- `favicon.svg` - SVG favicon (amber ST mark)

### PR Notify pages (self-contained inline styles)
- `pr-notify.html` - PR Notify landing/marketing page with "Add to Slack" OAuth flow
- `pr-notify-privacy.html` - Privacy policy for PR Notify (required by Slack app directory)

PR Notify pages use their own Slack-purple brand and have no dependency on `styles.css`.

## Design System (`styles.css`)

The CSS is organised in 15 labelled sections. Key conventions:

- **Palette:** Deep navy (`#0F172A`) primary, amber (`#F59E0B`) accent, slate scale for grays
- **Typography:** Outfit (headings) + Plus Jakarta Sans (body) via Google Fonts
- **Layout:** `.container` (1200px max), `.container-narrow` (800px), `.section` for vertical rhythm
- **Responsive:** Three breakpoints at `max-width: 1024px`, `768px`, `600px`. Hero title uses `clamp()` for fluid sizing.
- **Animations:** CSS-only hero background (gradient shift + dot grid + amber glow). Scroll reveals use `.animate-on-scroll` class toggled by an inline `IntersectionObserver` script.
- **Accessibility:** `prefers-reduced-motion` disables all animations. `.no-js` fallback on `<html>`. Skip-to-content link on every page. `:focus-visible` for keyboard-only focus styles.

## Contact Form

The contact form on `services.html` posts to Formspree (`https://formspree.io/f/{FORM_ID}`). The `{FORM_ID}` placeholder needs to be replaced with a real Formspree form ID. Formspree handles the Slack integration via its dashboard settings. A honeypot field (`_gotcha`) provides spam protection. After submission, Formspree redirects back with `?submitted=true` which triggers a JS-based success message.
