# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Single-file static portfolio site (`index.html`). No build step, no package manager, no framework — Tailwind CSS is loaded via CDN.

To preview: open `index.html` directly in a browser, or use any static file server (e.g. `npx serve .` or VS Code Live Server).

## Customization: Placeholders to Replace

| Placeholder | Where |
|---|---|
| `[YOUR_NAME]` | `<title>`, nav logo `<a>`, footer `<p>`, JS `const NAME` |
| `[INTRO_LINE_1]`, `[INTRO_LINE_2]` | About section `<p>` tags |
| `[EMAIL]` | Contact `mailto:` link |
| `[GITHUB]` | Contact GitHub `<a href>` + `PROJECTS` array `github` URLs |
| `YN` | `#avatar-fallback` div (initials shown when avatar image fails) |
| `assets/avatar.jpg` | `<img src>` in About section |

## JS Data Objects

All content data lives in the inline `<script>` block at the bottom of `index.html`:

- **`SKILLS`** (line ~335): Object with `frontend`, `backend`, `tools` arrays — rendered as badge pills.
- **`PROJECTS`** (line ~341): Array of objects with `title`, `description`, `tags`, `github`, `live`, `color` (`'blue'|'purple'|'green'`), `icon` (emoji).

## Architecture

Everything is in one file. The structure:

1. **`<head>`** — Tailwind CDN config (custom font + blink animation), then CDN script, then `<style>` with custom CSS (scrollbar, scroll-reveal, card hover, etc.)
2. **HTML sections** — `#navbar` → `#hero` → `#about` → `#skills` → `#projects` → `#contact` → `<footer>`
3. **Inline `<script>`** — Data (`SKILLS`, `PROJECTS`), then DOM rendering functions, then behavior (mobile menu, navbar scroll, scroll-spy via IntersectionObserver, scroll-reveal, typing animation, smooth scroll).

Skill badges and project cards are **rendered via JS** into `#skills-frontend`, `#skills-backend`, `#skills-tools`, and `#projects-grid` — they are not in the HTML markup.

## Styling Conventions

- Dark theme: `bg-slate-900` body, `bg-slate-800` cards, `border-slate-700` borders.
- Accent gradient: `from-blue-500 to-purple-500` (indigo/purple theme).
- Project card colors (`blue`, `purple`, `green`) control `COLOR_MAP` classes for tags and buttons, and `card-accent` top bar gradient.
- `.reveal` class + IntersectionObserver handles scroll-in animations. Add `class="reveal"` to any new section element to get the fade-up effect.
- `@media (prefers-reduced-motion: reduce)` disables animations for accessibility.
