# Gyserguiden — Projektbibel

Dansk horrorsite uden CMS. Alt er statisk HTML/CSS/JS, hosted på Netlify eller GitHub Pages.

## Hvad er Gyserguiden?

Et redaktionelt horrorsite på dansk der dækker film, serier, spil, bøger og brætspil. Blanding af nyheder (tidssensitiv) og evergreen-indhold (guides, anmeldelser, tools). Tonen er seriøs og vidende — ikke fanzine, ikke clickbait.

## Teknisk stack

- **HTML/CSS/JS** — ingen frameworks, ingen build-trin
- **Hosting**: Netlify eller GitHub Pages (statiske filer)
- **Billeder**: `/assets/img/` — filnavne på engelsk, kebab-case
- **Ingen CMS** — Claude er redaktionelt og teknisk hjælp

## Mappestruktur

```
gyserguiden/
├── index.html                    # Forside
├── CLAUDE.md                     # Denne fil
├── design-log.md                 # Designbeslutninger og changelog
├── _templates/                   # Skabeloner — kopier herfra til nye sider
│   ├── anmeldelse.html
│   ├── nyhed.html
│   └── guide.html (kommer)
├── assets/
│   ├── css/
│   │   ├── base.css              # Design tokens, reset, typografi, prose
│   │   └── components.css        # Header, footer, alle UI-komponenter
│   ├── js/
│   │   └── main.js               # Mobile menu, evt. fremtidig JS
│   └── img/                      # Alle billeder her
├── film/
│   ├── index.html                # Film-oversigt (mangler)
│   ├── klassikere/
│   ├── nye/
│   ├── subgenrer/
│   ├── skjulte-perler/
│   └── dansk/
├── serier/
├── spil/
├── boeger/
├── braetspil/
├── nyheder/
│   └── index.html                # Nyhedsoversigt (mangler)
├── anmeldelser/
│   ├── index.html                # Anmeldelsesoversigt (mangler)
│   ├── film/
│   ├── serier/
│   ├── spil/
│   ├── boeger/
│   └── braetspil/
├── guides/
│   └── index.html                # Guide-oversigt (mangler)
├── tools/                        # Interaktive HTML-tools
├── om.html                       # Om Gyserguiden (mangler)
├── cookies.html                  # (mangler)
└── privatliv.html                # (mangler)
```

## Navnekonventioner

### Filer
- Danske navne på URLs: `anmeldelser/film/solhverv.html`
- Ingen æ/ø/å i filnavne: brug `ae`, `oe`, `aa` → `boeger/`, `braetspil/`
- Bindestreg som separator: `skjulte-perler.html`
- Dato-prefix på nyheder: `nyheder/2026-05-19-ari-aster.html`

### Billeder
- Kebab-case, engelsk: `midsommar-poster.jpg`, `solhverv-still-01.jpg`
- Anmeldelses-covers: `[kategori]-[slug]-cover.jpg`, fx `film-solhverv-cover.jpg`

## Indholdstyper

### 1. Nyhed
- Tidssensitiv, 300–600 ord
- Fil: `nyheder/ÅÅÅÅ-MM-DD-slug.html`
- Skabelon: `_templates/nyhed.html`
- Meta: dato, kategori (Film/Spil/Serier/Bøger/Brætspil)

### 2. Anmeldelse
- Evergreen, 600–1200 ord
- Fil: `anmeldelser/[kategori]/[slug].html`
- Skabelon: `_templates/anmeldelse.html`
- Meta: karakter (1–6), genre, år, instruktør/forfatter

### 3. Guide / Feature
- Evergreen, 800–2500 ord
- Fil: `guides/[slug].html`
- Skabelon: `_templates/guide.html` (mangler — lav ved behov)
- Ingen karakter-system

### 4. Interaktivt tool
- HTML + JavaScript, selfcontained
- Fil: `tools/[slug].html`

## Tone of Voice

Se `tone-of-voice.md` for den fulde guide. Kort version:

- Skriv til den **vidende entusiast** — forklar ikke det åbenlyse
- Reference: **IGN/Eurogamer på sit bedste** — engageret, specifik, med holdning
- **Aldrig:** clickbait-overskrifter, akademisk passiv form, teatralsk sprog, uformel slang
- Første sætning skal ramme. Kom til sagen med det samme.

## Karakterskala (anmeldelser)

Gyserguiden bruger en **1–6-skala** (ikke 5 eller 10):
- **6/6** — Masterværk. Sjælden. Tøv ikke.
- **5/6** — Stærk anbefaling med lille forbehold.
- **4/6** — Solid, mere godt end dårligt.
- **3/6** — Blandet — interessant men ufuldstændig.
- **2/6** — Skuffer. Kun for dedikerede fans.
- **1/6** — Undgå.

## CSS-arkitektur

To delte filer — alle sider linker til begge:

```html
<link rel="stylesheet" href="/assets/css/base.css">
<link rel="stylesheet" href="/assets/css/components.css">
```

**base.css** indeholder:
- CSS custom properties (design tokens)
- Reset
- Typografi og `.prose`-klasse til langt indhold
- Layout utilities (`.container`, `.section`)

**components.css** indeholder:
- Header, nav, dropdown, hamburger, mobile-menu
- Hero
- Review-cards, news-list, guide-cards, tool-cards
- Footer, kontaktformular
- Page header (indersider med breadcrumb)
- Responsive breakpoints

**Tilføj aldrig inline `<style>` i HTML-filer.** Sæt ny styling i components.css.

## Design tokens (must not change without updating design-log.md)

```
--bg:            #0a0908   (næsten sort baggrund)
--bg-elevated:   #14110f   (kort, sektioner)
--bg-card:       #1a1614   (tool-cards)
--text:          #ede4d3   (varm hvid)
--text-muted:    #8a8175   (brødtekst, excerpts)
--text-dim:      #5a5247   (meta, labels)
--accent:        #a01818   (blodrød — borders, highlights)
--accent-bright: #c42323   (hover-tilstande, links)
--gold:          #b89968   (karakterskala, em-tekst)
--border:        #2a2420
--border-strong: #3a322c
```

Font: **Inter** (Google Fonts) — bruges til alt: display, body og mono via CSS-variabler.

## Workflow: tilføj nyt indhold

### Ny nyhed
1. Kopier `_templates/nyhed.html` til `nyheder/ÅÅÅÅ-MM-DD-slug.html`
2. Udfyld alle UDFYLD-kommentarer
3. Tilføj artiklen til `nyheder/index.html` (øverst i listen)
4. Opdater forsiden `index.html` — erstat ældste nyhed i news-sektionen

### Ny anmeldelse
1. Kopier `_templates/anmeldelse.html` til `anmeldelser/[kategori]/[slug].html`
2. Udfyld alle UDFYLD-kommentarer
3. Tilføj kortet til `anmeldelser/index.html`
4. Overvej om den skal fremhæves på forsiden (erstat ældste review-card)

### Opdater forside
Forsiden `index.html` er **manuel kuratorering** — hold den fri for automatik.
Trending-listen opdateres manuelt baseret på skøn.

## SEO-principper

- `<title>`: "[TITEL] — Gyserguiden" (max 60 tegn)
- `<meta name="description">`: 120–155 tegn, naturlig sætning
- Brug semantisk HTML: `<article>`, `<header>`, `<nav>`, `<main>`, `<aside>`, `<footer>`
- Billeder altid med `alt`-attribut

## Hvad mangler (prioriteret)

1. `nyheder/index.html` — oversigt over alle nyheder
2. `anmeldelser/index.html` — oversigt over alle anmeldelser
3. `film/index.html` + de andre kategori-indekser
4. `guides/index.html`
5. `om.html` — om sitet og redaktionen
6. `_templates/guide.html` — guideskabelon
7. Rigtige billeder i `/assets/img/`
8. Tools: horrorfilm-matcher, subgenre-finder, skrækkalenderen
9. Git-repo + Netlify-deploy
