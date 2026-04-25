# AIforBusinessBanking — Brand System

> **AI Built · Human Directed**

This repository is the single source of truth for the AIforBusinessBanking brand. It contains two files that work together as a complete portable brand system — one for visual execution, one for brand intelligence.

---

## What's in this repo

| File | Purpose | Used by |
|---|---|---|
| `brand-tokens.css` | CSS custom properties for colour, typography, spacing, and theming | Websites, admin panels, web apps |
| `brand-system.json` | Brand positioning, tone, design rules, and AI instructions | Claude, ChatGPT, Framer, Netlify Functions, any AI tool |

---

## CDN URLs

Both files are served via [jsDelivr](https://www.jsdelivr.com/) — a free, fast, global CDN that automatically serves any public GitHub repo.

### Always latest (recommended for development)
```
https://cdn.jsdelivr.net/gh/satyam78-web/brand-system@main/brand-tokens.css
https://cdn.jsdelivr.net/gh/satyam78-web/brand-system@main/brand-system.json
```

### Pinned to a version (recommended for production)
```
https://cdn.jsdelivr.net/gh/satyam78-web/brand-system@v1.0/brand-tokens.css
https://cdn.jsdelivr.net/gh/satyam78-web/brand-system@v1.0/brand-system.json
```

> Pinned URLs never change even if you update the brand. Safe for live sites.

---

## How to use `brand-tokens.css`

### In any HTML file
Add this to your `<head>` — before your own stylesheet:

```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/satyam78-web/brand-system@main/brand-tokens.css">
<link rel="stylesheet" href="your-styles.css">
```

### Light mode (default)
No extra setup needed. Light theme is applied automatically.

### Dark mode
Add `data-theme="dark"` to your `<html>` tag:

```html
<html data-theme="dark">
```

### Toggle with JavaScript
```javascript
function toggleTheme() {
  const html = document.documentElement;
  const current = html.getAttribute('data-theme') || 'light';
  const next = current === 'light' ? 'dark' : 'light';
  html.setAttribute('data-theme', next);
  localStorage.setItem('theme', next);
}

// Restore saved preference on load
const saved = localStorage.getItem('theme') || 'light';
document.documentElement.setAttribute('data-theme', saved);
```

### Using the tokens in your CSS
Once linked, all tokens are available as CSS custom properties:

```css
/* Colours */
.my-heading {
  color: hsl(var(--foreground));
  background: hsl(var(--background));
}

/* Brand accent */
.highlight {
  color: var(--color-purple);
}

/* Typography */
body {
  font-family: var(--font-sans);
  font-size: var(--text-base);
}

/* Spacing */
.card {
  padding: var(--space-6);
  border-radius: var(--radius-xl);
  border: 1px solid hsl(var(--border));
  box-shadow: var(--shadow-md);
}
```

### Ready-to-use utility classes
The token file includes pre-built utility classes you can use directly in HTML:

```html
<!-- Surfaces -->
<div class="bg-card">...</div>
<div class="bg-muted">...</div>

<!-- Text -->
<p class="text-muted">Caption text</p>

<!-- Badges -->
<span class="badge badge-blue">Commercial Lending</span>
<span class="badge badge-green">Active</span>
<span class="badge badge-purple">Pro</span>

<!-- Buttons -->
<button class="btn btn-primary">Primary action</button>
<button class="btn">Secondary</button>

<!-- Inputs -->
<input class="input" placeholder="Enter value…">

<!-- Cards -->
<div class="card">...</div>

<!-- Shadows -->
<div class="shadow-md">...</div>

<!-- Border radius -->
<div class="rounded-xl">...</div>
```

---

## How to use `brand-system.json`

### With Claude (recommended)
Attach `brand-system.json` to any conversation with Claude before asking it to build, write, or design anything for AIforBusinessBanking. Claude will use it as the source of truth for tone, colours, design rules, and AI guardrails.

**Example prompt:**
> "Using the attached brand-system.json, write an article summary for the homepage. Follow the tone and content guidelines."

### With ChatGPT
Upload the file via the paperclip icon and reference it in your prompt:
> "Refer to the brand-system.json I've attached. Write a case study introduction following the brand voice."

### With Framer or other AI design tools
Paste the JSON content into the AI prompt context or attach the file where supported.

### In a Netlify Function
Fetch the brand system at runtime to drive AI-generated content:

```javascript
// netlify/functions/generate-content.js
export async function handler() {
  const brand = await fetch(
    'https://cdn.jsdelivr.net/gh/satyam78-web/brand-system@main/brand-system.json'
  ).then(r => r.json());

  // Use brand.ai_usage.default_instruction as system prompt
  // Use brand.content.style.voice for tone guidance
  // Use brand.content.focus_areas to scope topics
}
```

### Key fields reference

| Field | What it contains |
|---|---|
| `brand.positioning` | Audience, description, tone |
| `brand.tagline` | "Re-architecting Business Banking with AI" |
| `design.color_usage` | Which colours to use and when |
| `design.typography` | Font choice and style rules |
| `design.logo` | Logo treatment rules |
| `content.style` | Voice and what to avoid |
| `content.focus_areas` | Topics this brand covers |
| `ai_usage.rules` | AI guardrails — what AI tools must follow |
| `ai_usage.default_instruction` | Drop this into any AI system prompt |

---

## Projects using this brand system

| Project | Repo | Environment |
|---|---|---|
| AIforBusinessBanking.com | `satyam78-web/AlforBusinessBanking` | Netlify |
| Admin Panel | Same repo `/admin` | Netlify |

> Add new projects here as they are created.

---

## Versioning

When making significant brand changes (new colours, updated tone, new logo rules):

1. Make changes in `main` branch
2. Test across existing projects
3. Create a GitHub Release and tag it (e.g. `v1.1`)
4. Update pinned URLs in production sites when ready

This ensures live sites never break from brand updates unless you choose to upgrade.

---

## Token reference

### Core colours
| Token | Light | Dark | Usage |
|---|---|---|---|
| `--background` | `#ffffff` | `#08101e` | Page background |
| `--foreground` | `#0a0f1e` | `#f0f4f8` | Body text |
| `--card` | `#ffffff` | `#0e1829` | Card surfaces |
| `--border` | `#dde3ed` | `#1e2d47` | Dividers, borders |
| `--muted-foreground` | `#6b7a99` | `#7d8faa` | Secondary text |

### Brand accent colours
| Token | Hex | Usage |
|---|---|---|
| `--color-blue` | `#2563eb` | Topics, links, primary info |
| `--color-purple` | `#9333ea` | AI accent, CTAs, brand moments |
| `--color-green` | `#16a34a` | Active, success, positive |
| `--color-red` | `#ef4444` | Error, destructive, alert |
| `--color-amber` | `#f59e0b` | Warning, regulation topics |

### Typography
| Token | Value |
|---|---|
| `--font-sans` | Inter, system-ui |
| `--font-mono` | ui-monospace, Menlo |
| `--text-sm` | 14px |
| `--text-base` | 16px |
| `--text-xl` | 20px |
| `--text-2xl` | 24px |

---

## Footer signature

Use this line in footers, decks, reports, and brand moments:

```
AI Built · Human Directed
```

---

*AIforBusinessBanking Brand System — maintained by Satyam Agrawal*
