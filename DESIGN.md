# MarkMade — Design System v2

Aktualisiert: April 2026 — Refresh auf "Editorial Cream" Look der Startseite.
Vorgängerversion (DESIGN v1) liegt im Git-Verlauf vor diesem Commit. Unterseiten nutzen weiterhin v1.

## 0. CSS-Architektur (wichtig)

Es gibt **zwei getrennte Token-Welten**, die strikt nicht überlappen:

| Datei | Lädt von | Token-Welt | Genutzt durch |
|---|---|---|---|
| `src/styles/global.css` | `BaseLayout.astro` | v1: `--surface*`, `--primary*`, `--secondary*`, `--on-surface*`, `--dust` | Alle Unterseiten |
| `src/styles/landing.css` | `LandingLayout.astro` | v2: `--cream*`, `--ink*`, `--bordeaux*`, `--sage`, `--olive`, `--rule*`, `--muted` | NUR Startseite |

`LandingLayout.astro` importiert **NICHT** `global.css`. `BaseLayout.astro` importiert **NICHT** `landing.css`. Komponenten, die in beiden Welten gerendert werden (`CookieBanner.astro`, `Chatbot.astro`), nutzen CSS-Variable-Fallbacks, z.B. `var(--ink, var(--primary))`.

## 1. Farben (v2 — Cream Look)

| Token | Hex | Verwendung |
|---|---|---|
| --cream | #F5F1EA | Haupthintergrund |
| --cream-2 | #EFEAE0 | Sektionswechsel (Steps, FAQ) |
| --cream-3 | #E7E1D4 | Footer-Hintergrund |
| --ink | #1A1814 | Haupttext, Headlines |
| --ink-2 | #3A352D | Sekundärtext |
| --muted | #6E665A | Eyebrows, Labels |
| --rule | #D9D2C2 | Trennlinien subtil |
| --rule-2 | #C7BFAC | Trennlinien stärker |
| --bordeaux | #A8174D | Brand-Akzent (CTAs, Italics) |
| --bordeaux-deep | #7E0F39 | Hover-States |
| --sage | #D4DDB8 | CTA-Card-Hintergrund |
| --olive | #9C9678 | Schritt-Nummern, Italic-Akzente |

## 2. Typografie

| Rolle | Familie |
|---|---|
| Headlines | Roboto Slab |
| Italic-Akzente | Instrument Serif |
| Body, UI | Inter |

Italic-Highlight-Pattern für hervorgehobene Worte:
`font-family: var(--serif-italic); font-weight: 400; color: var(--bordeaux);`

Schriften werden ausschließlich via `@import` in `landing.css` geladen — Unterseiten ziehen sie nicht.

## 3. Komponenten der Startseite

Naming-Konvention: alles, was zur Cream-Welt gehört, bekommt das `Landing`-Präfix. Komponenten ohne Präfix gibt es nur, wenn keine Namens-Kollision mit der v1-Welt existiert (Topstrip, Nav, Principle waren in v1 nicht vorhanden).

| Komponente | Datei | Zweck |
|---|---|---|
| Topstrip | src/components/Topstrip.astro | Live-Indicator + Marquee |
| Nav | src/components/Nav.astro | Sticky-Nav, Glassmorphism |
| LandingHero | src/components/LandingHero.astro | Display-Headline + Stat-Bar |
| LandingWasKiMacht | src/components/LandingWasKiMacht.astro | Steps mit Sticky-Sidebar |
| Principle | src/components/Principle.astro | Ledger 3-spaltig |
| LandingFaq | src/components/LandingFaq.astro | Accordion |
| LandingCta | src/components/LandingCta.astro | Sage-Card |
| LandingFooter | src/components/LandingFooter.astro | 5-Spalten-Footer (NUR Startseite) |

Die Komponenten enthalten ausschließlich Markup — alle CSS-Regeln liegen zentral in `landing.css`. Das matched 1:1 die HTML-Referenz unter `_design/Markmade_Landing.html` und vermeidet Astro-Scoping-Konflikte für klassenübergreifende Selektoren (`.btn`, `.kicker`, `.zone`, `.brand`).

**Komponenten ohne Landing-Präfix** (`Hero.astro`, `Cta.astro`, `Faq.astro`, `Rechner.astro`, `Beweis.astro`, `Angebot.astro`, `Prozess.astro`, `VierFragen.astro`, `Header.astro`, `Footer.astro`) gehören weiter zur v1-Welt und werden ausschließlich von Unterseiten via `BaseLayout` gerendert. Niemals auf der Startseite einbinden — und Landing*-Komponenten niemals in einer Unterseite einbinden.

## 4. Layouts

- **LandingLayout.astro** — NUR Startseite (kein Header/Footer im Layout, kommt aus index.astro). Importiert `landing.css`.
- **BaseLayout.astro** — alle Unterseiten (UNVERÄNDERT, alte Schriften, alter Header/Footer). Importiert `global.css`.

## 5. Don'ts

- Keine anderen Schriften als Roboto Slab / Instrument Serif / Inter (auf der Startseite)
- Niemals reines Schwarz oder reines Weiß
- Bordeaux nur für 1–2 Wörter als Italic-Highlight, nicht für ganze Sätze
- Keine drop-shadows außer denen in der HTML-Referenz definiert
- Backup der Vorgänger-Komponenten liegt in `src/components/_legacy/` — nicht löschen ohne Rücksprache
- Wer auf der Startseite eine v1-Komponente einbindet (z.B. das alte `Header.astro`), bricht das Design. Andersrum genauso.
