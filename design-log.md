# Design Log — Gyserguiden

Kronologisk log over designbeslutninger. Nye beslutninger tilføjes øverst.

---

## 2026-05-19 — Initial design + CSS-arkitektur

**Beslutning:** Splittet CSS fra index.html til to delte filer — `base.css` og `components.css`.

**Hvorfor:** Alle fremtidige sider skal have identisk design. Ét sted at ændre = konsistens uden duplikering.

**Konsekvens:** Alle HTML-filer linker til `/assets/css/base.css` og `/assets/css/components.css`. Aldrig inline `<style>` i HTML.

---

## 2026-05-19 — Grundlæggende designsystem fastlagt

### Visuel identitet

**Stemning:** Seriøs, redaktionel. Tænk *The Wire* møder et godt magasin — ikke Halloween-kitsch.
**Reference:** Mørke editorielle medier (Criterion, Pitchfork, The Ringer) med horrorens æstetik.

### Farvepalette

| Token | Hex | Brug |
|---|---|---|
| `--bg` | `#0a0908` | Sidebaggrund |
| `--bg-elevated` | `#14110f` | Sektioner, guide-cards |
| `--bg-card` | `#1a1614` | Tool-cards |
| `--text` | `#ede4d3` | Primær tekst (varm, ikke kold hvid) |
| `--text-muted` | `#8a8175` | Brødtekst, excerpts |
| `--text-dim` | `#5a5247` | Meta-info, labels, dato |
| `--accent` | `#a01818` | Blodrød — borders, hover-baggrunde |
| `--accent-bright` | `#c42323` | Hover-tilstande, aktive links |
| `--gold` | `#b89968` | Karakterskala, `<em>` i headings |
| `--border` | `#2a2420` | Subtile skillelinjer |
| `--border-strong` | `#3a322c` | Tydeligere borders, input-felter |

**Regel:** Aldrig ren hvid (`#ffffff`) eller ren sort (`#000000`). Alt er varmt og dæmpet.

### Typografi

**Font:** Inter (Google Fonts) — ét font-family til alt. Adskillelse sker via vægt og letter-spacing:
- Display/overskrifter: `font-weight: 700–800`, `letter-spacing: -0.03em`
- Brødtekst: `font-weight: 400`, normal letter-spacing
- Labels/mono-look: `font-weight: 500`, `letter-spacing: 0.15–0.2em`, `text-transform: uppercase`

**Beslutning om ét font-family:** Holder sitet enkelt og undgår font-clash. Inter er skalerbar nok til alle roller.

### Karakterskala

**1–6 (ikke 5 eller 10).**

Begrundelse: 10-skalaen giver falsk præcision. 5-skalaen er for grov. 6 er det danske skolesystems logik — folk forstår intuitivt at 4/6 er solidt men ikke fremragende.

### Grain-overlay

Subtil `body::before` med SVG-støj, `opacity: 0.04`, `mix-blend-mode: overlay`. Tilføjer filmisk atmosfære uden at kompromittere læsbarhed. Må ikke øges.

### Hjørner

Næsten ingen `border-radius`. Skarpe hjørner giver en præcis, redaktionel følelse. Eneste undtagelse: nav-links har `border-radius: 2px` (nærmest usynlig).

### Animationer

- **Logo-dot:** Puls, 3s, `opacity: 0.5–1`. Subtil livsindikator.
- **Hero-indhold:** `fadeUp`, stagger 0.1s delay per element. Kun ved sideindlæsning.
- **Hover-states:** Transitions på 0.2–0.3s. Aldrig over 0.4s.
- **Guide-card top-border:** Width 0→100% på hover, 0.35s. Karakteristisk micro-interaction.

---

## Fremtidige designspørgsmål (uafklarede)

- **Billeder:** Når vi begynder at bruge rigtige fotos/posters — hvilken aspect-ratio er standard for review-cards? (Nuværende: 4/5 for film/spil/bøger, 4/3 for nyhedslisten)
- **Dark mode / light mode:** Ingen planer om det. Sitet er designet som dark-only.
- **Farvet accent per kategori?** Film = rød, Spil = blå, Bøger = guld? Beslutning: nej foreløbig — ét accent-system er renere.
- **Hero på forsiden:** Nuværende hero er generisk/atmosfærisk. Overvej: skal den vise fremhævet indhold (fx ugens store anmeldelse)?
