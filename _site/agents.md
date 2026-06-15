# AGENTS.md — MoSAIC-P38 Website

## Mission

Build a functional, polished, and good-looking website for the **MoSAIC-P38** computer architecture system.

- Source project: https://github.com/lbnlcomputerarch/MoSAIC-P38
- The site MUST be built with Jekyll using the **jekyll-theme-yat** theme: https://github.com/jeffreytse/jekyll-theme-yat
- The landing page MUST visually replicate the provided reference image (logo bar across the top, large "MoSAIC-P38" title, and the two hero images below), then EXTEND it with a navigation bar (Home, Documentation, Tutorials, Test Cases, etc.) placed directly beneath the logo bar.
- Leave clearly-marked placeholders/spaces where the provided logos and images will be inserted.

---

## 1. Hard Constraints (do not violate)

1. **Theme**: Use `jekyll-theme-yat` ONLY. Do not swap themes.
2. **Color palette**: Use ONLY the four LBNL brand colors below. No other colors are permitted (except pure white `#FFFFFF` for page background and near-black text fallbacks where a brand color is unsuitable for body text — prefer Dark Blue for body text).
3. **Banner / header bar**: The top banner MUST be **Teal `#007681`**.
4. **Font**: ALL text MUST use **Libre Franklin** (a free Google Font). Provide a system/web-safe fallback stack.
5. **Layout fidelity**: The landing page hero MUST look like the reference image (logo row up top, big centered title, two images side-by-side below).
6. **Placeholders**: Every logo and image must be a clearly-labeled placeholder so a human can drop in the real asset later.

---

## 2. LBNL Color Palette (the ONLY allowed colors)

| Name        | PMS           | HEX       | RGB             |
|-------------|---------------|-----------|-----------------|
| Dark Blue   | PMS 547       | `#00313C` | 0, 49, 60       |
| Teal        | PMS 7474      | `#007681` | 0, 118, 129     |
| Light Gray  | Cool Gray 5   | `#B1B3B3` | 177, 179, 179   |
| Dark Gray   | Cool Gray 10  | `#63666A` | 99, 102, 106    |

Define these as CSS variables and reference them everywhere. Do NOT hardcode other hex values.

```scss
:root {
  --lbnl-dark-blue:  #00313C;
  --lbnl-teal:       #007681;
  --lbnl-light-gray: #B1B3B3;
  --lbnl-dark-gray:  #63666A;
  --lbnl-white:      #FFFFFF;
}
```

Recommended usage:
- **Banner/header background**: Teal `#007681`
- **Banner text & nav links**: White `#FFFFFF`
- **Body text & headings**: Dark Blue `#00313C`
- **Secondary text / captions**: Dark Gray `#63666A`
- **Borders / dividers / subtle backgrounds**: Light Gray `#B1B3B3`
- **Hover/active states**: Dark Blue `#00313C` on Teal, or Teal on white

---

## 3. Typography — Libre Franklin

All text uses **Libre Franklin**, a free, open-source Google Font (a Franklin Gothic–style typeface). It can be loaded directly from Google Fonts — no licensed files needed.

1. Add the Google Fonts link to the `<head>`. The easiest place is `_includes/head.html` (copy yat's version into your repo if it doesn't exist), or inject via the head. Add:

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Libre+Franklin:wght@400;500;600;700&display=swap" rel="stylesheet">
```

2. Set Libre Franklin as the global font with a fallback stack and override yat's defaults:

```scss
$global-font-family: "Libre Franklin", "Franklin Gothic Medium",
                     "Arial Narrow", Arial, sans-serif;

body, h1, h2, h3, h4, h5, h6, p, a, li, nav, button, input, textarea, figcaption {
  font-family: $global-font-family !important;
}
```

3. Override the yat theme's default fonts so Libre Franklin wins everywhere.

---

## 4. Repository / File Structure to Create

```
.
├── AGENTS.md
├── Gemfile
├── _config.yml
├── index.md                  # Home (hero replica + intro)
├── documentation.md
├── tutorials.md
├── test-cases.md
├── about.md
├── _layouts/
│   └── home.html             # custom hero layout (overrides yat default)
├── _includes/
│   ├── head.html             # add Google Fonts (Libre Franklin) link
│   ├── logo-bar.html         # top row of logos (replicates image)
│   └── hero.html             # big title + two hero images
├── _sass/
│   └── custom/
│       └── _lbnl.scss        # palette, fonts, banner, layout overrides
├── assets/
│   ├── css/
│   │   └── main.scss         # imports yat + _lbnl.scss
│   └── images/
│       ├── README.txt        # describes each placeholder
│       ├── logo-berkeley-lab.png        [PLACEHOLDER]
│       ├── logo-amcr.png                [PLACEHOLDER]
│       ├── logo-computer-arch-group.png [PLACEHOLDER]
│       ├── logo-swatches.png            [PLACEHOLDER]
│       ├── hero-riscv-snn.png           [PLACEHOLDER — left diagram]
│       └── hero-mosaic-block.png        [PLACEHOLDER — right block diagram]
```

---

## 5. Gemfile

```ruby
source "https://rubygems.org"
gem "jekyll", "~> 4.3"
gem "jekyll-theme-yat"
group :jekyll_plugins do
  gem "jekyll-feed"
  gem "jekyll-seo-tag"
  gem "jekyll-paginate"
end
```

---

## 6. `_config.yml`

```yaml
title: MoSAIC-P38
description: >-
  MoSAIC-P38 — a computer architecture system from the LBNL
  Computer Architecture Group (AMCR).
theme: jekyll-theme-yat
baseurl: ""
url: ""

# Brand
color_palette:
  dark_blue:  "#00313C"
  teal:       "#007681"
  light_gray: "#B1B3B3"
  dark_gray:  "#63666A"

# Navigation (rendered directly under the logo bar)
header_pages:
  - index.md
  - documentation.md
  - tutorials.md
  - test-cases.md
  - about.md

# yat theme settings
yat:
  date_format: "%b %-d, %Y"

plugins:
  - jekyll-feed
  - jekyll-seo-tag
  - jekyll-paginate

exclude:
  - AGENTS.md
  - Gemfile
  - Gemfile.lock
  - README.md
```

> NOTE: The yat banner background must be overridden to Teal `#007681` in `_sass/custom/_lbnl.scss` (see §9). The nav menu (Home, Documentation, Tutorials, Test Cases, About) must render immediately below the logo bar.

---

## 7. `_includes/logo-bar.html`

Replicate the top row of the reference image: a white band with logos arranged left and right. Use placeholder images.

```html
<!-- LOGO BAR — replicates the top row of the reference image.
     Replace placeholder images in assets/images/ with the real logos. -->
<div class="lbnl-logo-bar">
  <div class="lbnl-logo-bar__inner">
    <div class="lbnl-logo-bar__left">
      <img src="{{ '/assets/images/logo-berkeley-lab.png' | relative_url }}"
           alt="Berkeley Lab logo" class="lbnl-logo lbnl-logo--lab">
    </div>
    <div class="lbnl-logo-bar__right">
      <img src="{{ '/assets/images/logo-amcr.png' | relative_url }}"
           alt="AMCR — Applied Mathematics & Computational Research"
           class="lbnl-logo lbnl-logo--amcr">
      <img src="{{ '/assets/images/logo-computer-arch-group.png' | relative_url }}"
           alt="Berkeley Lab Computer Architecture Group"
           class="lbnl-logo lbnl-logo--cag">
      <img src="{{ '/assets/images/logo-swatches.png' | relative_url }}"
           alt="Color swatches" class="lbnl-logo lbnl-logo--swatches">
    </div>
  </div>
</div>
```

---

## 8. `_includes/hero.html`

Large centered title + two side-by-side hero images, matching the reference image.

```html
<!-- HERO — big title and the two diagram images from the reference. -->
<section class="lbnl-hero">
  <h1 class="lbnl-hero__title">MoSAIC-P38</h1>
  <div class="lbnl-hero__images">
    <figure class="lbnl-hero__fig">
      <img src="{{ '/assets/images/hero-riscv-snn.png' | relative_url }}"
           alt="RISC-V to SNN message-passing diagram">
      <figcaption class="lbnl-caption">RISC-V &harr; SNN</figcaption>
    </figure>
    <figure class="lbnl-hero__fig">
      <img src="{{ '/assets/images/hero-mosaic-block.png' | relative_url }}"
           alt="MoSAIC architecture block diagram">
      <figcaption class="lbnl-caption">MoSAIC architecture</figcaption>
    </figure>
  </div>
</section>
```

---

## 9. `_includes/head.html`

Copy yat's `head.html` into your repo (so you can extend it) and add the Libre Franklin Google Fonts links inside `<head>`. If you do not override the whole file, ensure these lines are injected into the document head:

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Libre+Franklin:wght@400;500;600;700&display=swap" rel="stylesheet">
```

---

## 10. `_sass/custom/_lbnl.scss`

This is the core styling file. It enforces palette, font, teal banner, logo bar, and hero layout.

```scss
:root {
  --lbnl-dark-blue:  #00313C;
  --lbnl-teal:       #007681;
  --lbnl-light-gray: #B1B3B3;
  --lbnl-dark-gray:  #63666A;
  --lbnl-white:      #FFFFFF;
}

$global-font-family: "Libre Franklin", "Franklin Gothic Medium",
                     "Arial Narrow", Arial, sans-serif;

/* ---- Global typography & color ---- */
body {
  font-family: $global-font-family !important;
  color: var(--lbnl-dark-blue);
  background: var(--lbnl-white);
}
h1, h2, h3, h4, h5, h6, p, a, li, nav, button, input, textarea, figcaption {
  font-family: $global-font-family !important;
}
h1, h2, h3, h4, h5, h6 { color: var(--lbnl-dark-blue); }
a { color: var(--lbnl-teal); }
a:hover { color: var(--lbnl-dark-blue); }

/* ---- Logo bar (white, sits above nav) ---- */
.lbnl-logo-bar {
  background: var(--lbnl-white);
  border-bottom: 2px solid var(--lbnl-light-gray);
  padding: 0.75rem 1.5rem;
}
.lbnl-logo-bar__inner {
  max-width: 1100px;
  margin: 0 auto;
  display: flex;
  align-items: center;
  justify-content: space-between;
  flex-wrap: wrap;
  gap: 1rem;
}
.lbnl-logo-bar__right {
  display: flex;
  align-items: center;
  gap: 1rem;
}
.lbnl-logo { height: 56px; width: auto; object-fit: contain; }
.lbnl-logo--lab      { height: 48px; }
.lbnl-logo--swatches { height: 56px; }

/* ---- NAV BANNER (TEAL, directly under logo bar) ---- */
/* Override yat's default header/nav background to LBNL teal. */
.navbar,
.site-header,
.header,
.post-top-bar,
nav.navbar {
  background-color: var(--lbnl-teal) !important;
  background-image: none !important;
}
.navbar a,
.site-header a,
.nav-link,
.navbar .menu a,
.navbar-nav .nav-item a {
  color: var(--lbnl-white) !important;
  font-family: $global-font-family !important;
  letter-spacing: 0.02em;
}
.navbar a:hover,
.nav-link:hover {
  color: var(--lbnl-dark-blue) !important;
}
.nav-link.active,
.navbar a.active {
  border-bottom: 3px solid var(--lbnl-white);
}

/* ---- HERO ---- */
.lbnl-hero {
  max-width: 1100px;
  margin: 0 auto;
  padding: 2.5rem 1.5rem 3.5rem;
  text-align: center;
}
.lbnl-hero__title {
  font-size: clamp(2.5rem, 7vw, 5rem);
  font-weight: 700;
  color: var(--lbnl-dark-blue);
  margin: 0.5rem 0 2rem;
  letter-spacing: 0.01em;
}
.lbnl-hero__images {
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  justify-content: center;
  gap: 2rem;
}
.lbnl-hero__fig {
  flex: 1 1 360px;
  max-width: 520px;
  margin: 0;
}
.lbnl-hero__fig img {
  width: 100%;
  height: auto;
  display: block;
}
.lbnl-caption {
  color: var(--lbnl-dark-gray);
  font-size: 0.95rem;
  margin-top: 0.5rem;
}

/* ---- Buttons / accents ---- */
.btn, button {
  background: var(--lbnl-teal);
  color: var(--lbnl-white);
  border: none;
}
.btn:hover, button:hover {
  background: var(--lbnl-dark-blue);
}

/* ---- Footer ---- */
.site-footer, footer {
  background: var(--lbnl-dark-blue) !important;
  color: var(--lbnl-light-gray) !important;
}
.site-footer a, footer a { color: var(--lbnl-light-gray) !important; }

/* ---- Responsive ---- */
@media (max-width: 700px) {
  .lbnl-logo-bar__inner { justify-content: center; }
  .lbnl-logo-bar__right { justify-content: center; }
}
```

---

## 11. `assets/css/main.scss`

```scss
---
---
@import "yat";
@import "custom/lbnl";
```

> If yat's import name differs, inspect the installed gem and import its main partial, THEN import `custom/lbnl` so the LBNL overrides take precedence.

---

## 12. `_layouts/home.html`

Custom home layout that places the logo bar, then nav (theme nav), then the hero, then content.

```html
---
layout: default
---
{% include logo-bar.html %}
{% include hero.html %}
<div class="page-content">
  <div class="wrapper">
    {{ content }}
  </div>
</div>
```

> Ensure the theme's `default` layout renders the navbar between the logo bar and hero. If the yat `default` layout places its navbar at the very top, modify the layout (or use a copy in `_layouts/`) so the order is: **(1) logo bar → (2) teal nav → (3) hero → (4) content**.

---

## 13. Page Stubs

### `index.md`
```markdown
---
layout: home
title: Home
---

MoSAIC-P38 is a computer architecture system developed by the
LBNL Computer Architecture Group (AMCR). [Brief overview text here.]
```

### `documentation.md`
```markdown
---
layout: page
title: Documentation
permalink: /documentation/
---

# Documentation
[Architecture overview, build instructions, API/reference docs go here.]
```

### `tutorials.md`
```markdown
---
layout: page
title: Tutorials
permalink: /tutorials/
---

# Tutorials
[Step-by-step guides go here.]
```

### `test-cases.md`
```markdown
---
layout: page
title: Test Cases
permalink: /test-cases/
---

# Test Cases
[Validation suites, benchmarks, example runs go here.]
```

### `about.md`
```markdown
---
layout: page
title: About
permalink: /about/
---

# About
[Project background, team, links to the GitHub repo, citation info.]
```

---

## 14. Placeholder Asset Notes (`assets/images/README.txt`)

```
Replace these placeholder files with the real assets (keep the same filenames):

  logo-berkeley-lab.png         -> Berkeley Lab logo (top-left of logo bar)
  logo-amcr.png                 -> AMCR logo
  logo-computer-arch-group.png  -> Berkeley Lab Computer Architecture Group logo
  logo-swatches.png             -> color swatch image (far right of logo bar)
  hero-riscv-snn.png            -> left hero diagram (RISC-V <-> SNN)
  hero-mosaic-block.png         -> right hero diagram (MoSAIC block diagram)

Recommended: transparent-background PNG or SVG for logos.
```

Until real files are supplied, generate simple placeholder images (solid Light Gray `#B1B3B3` rectangles with centered Dark Gray label text) at appropriate aspect ratios so the layout renders correctly.

---

## 15. Build & Verify

Run locally and confirm:

```bash
bundle install
bundle exec jekyll serve
```

Verification checklist:
- [ ] Logo bar appears at the very top with 1 left logo + 3 right logos (placeholders OK).
- [ ] Teal `#007681` navigation banner sits directly below the logo bar.
- [ ] Nav contains: Home, Documentation, Tutorials, Test Cases, About.
- [ ] Large "MoSAIC-P38" title is centered below the nav.
- [ ] Two hero images sit side-by-side below the title.
- [ ] Every visible color is one of the four LBNL palette colors (plus white background).
- [ ] All text renders in Libre Franklin (loaded from Google Fonts).
- [ ] Layout is responsive (logos stack/center on mobile; hero images wrap).
- [ ] No theme other than jekyll-theme-yat is used.

---

## 16. Strict Reminders for the Agent

- Do NOT introduce colors outside the four-color LBNL palette.
- Do NOT replace `jekyll-theme-yat`.
- Do NOT use any font other than Libre Franklin (with the specified fallback stack).
- Keep the banner Teal `#007681`.
- Keep all image/logo insertions as clearly-named placeholders.
- Preserve the visual order: logo bar → teal nav → big title → two hero images → content.