# MarkMade — Projekt- & Datei-Übersicht

**Letzte Aktualisierung:** April 2026 (nach Cream-Look-Redesign + UI-Polish)
**Zweck:** Diese Datei beantwortet die Frage "wo liegt was" für alle MarkMade-bezogenen Projekte. Sie ist die erste Quelle der Wahrheit für jeden zukünftigen Chat.

---

## Übersicht aller MarkMade-Projekte

Es gibt **drei separate Projekte** unter dem Namen MarkMade:

| # | Projekt | Pfad / Repo | Zweck |
|---|---|---|---|
| 1 | Astro-Webseite | `~/Claude-Projekte/markmade/` | Die öffentliche Webseite markmade.de |
| 2 | Chatbot-Backend | `~/Claude-Projekte/markmade-chatbot/` | Express-Server der den Chatbot ausliefert |
| 3 | Automation-Setup | `~/markmade/` | n8n-Workflow für Instagram/Facebook-Posting |

**Wichtig:** Wenn jemand "MarkMade-Projekt" sagt, ist meistens die Webseite gemeint. Bei Unsicherheit: Webseite ist Astro, Chatbot ist Express+JS, Automation ist Python/n8n.

---

## 1. Astro-Webseite (markmade.de)

### Pfad

```
/Users/markbergenthal/Claude-Projekte/markmade/
```

### Was es ist

Die öffentliche Webseite **markmade.de** — Astro-Projekt, statisch generiert, automatisch deployed auf Vercel.

### Stack

- **Framework:** Astro
- **Hosting:** Vercel
- **Domain:** markmade.de (DNS bei All-inkl., zeigt auf Vercel)
- **Git-Remote:** `git@github.com:onlinemaster711/markmade1.git` (SSH)
- **Branch:** `main` (jeder Push triggert ein automatisches Vercel-Deployment)

### Aktueller Design-Status (April 2026)

Die Seite läuft seit dem Cream-Look-Redesign mit **zwei parallelen Design-Systemen**:

- **Cream-Look (v2)** — derzeit auf 3 Seiten: `index.astro`, `ki-steuerberater.astro`, `ki-automatisierung-workflow.astro`. Roboto Slab + Inter + Instrument Serif. Cream-Hintergrund, Bordeaux-Akzente, Sage-CTA. Minimaler Header (Logo + CTA-Button), kein Topstrip, kein Menu, kein Ratgeber-Link.
- **Original-Look (v1)** — Auf allen ~33 Unterseiten. Noto Serif + Manrope. Off-White-Hintergrund, klassisches MarkMade-Design.

Beide Welten sind sauber getrennt — sie teilen sich nur den Chatbot und CookieBanner.

### Ordnerstruktur

```
markmade/
├── _design/                  ← .gitignore-d, lokale HTML-Referenzen
│   └── Markmade_Landing.html ← HTML-Entwurf der Startseite
├── src/
│   ├── pages/                ← 36 Seiten total (3 Cream-Look + 33 Original-Look)
│   │   ├── index.astro                       ← Startseite (CREAM-LOOK)
│   │   ├── ki-steuerberater.astro            ← CREAM-LOOK
│   │   ├── ki-automatisierung-workflow.astro ← CREAM-LOOK
│   │   ├── chatbot-handwerker.astro          ← Original-Look
│   │   ├── ki-aerzte.astro                   ← Original-Look
│   │   ├── webdesign-stuttgart.astro         ← Original-Look
│   │   ├── ratgeber/                         ← Ratgeber-Unterseiten
│   │   └── ... (alle anderen Original-Look)
│   ├── components/
│   │   ├── LandingHero.astro            ← NUR Startseite
│   │   ├── LandingWasKiMacht.astro      ← NUR Startseite
│   │   ├── LandingFaq.astro             ← NUR Startseite
│   │   ├── LandingCta.astro             ← NUR Startseite
│   │   ├── LandingFooter.astro          ← NUR Startseite (5-Spalten-Akkordeon)
│   │   ├── Nav.astro                    ← NUR Startseite (minimal: Logo + CTA)
│   │   ├── Topstrip.astro               ← Liegt im Repo, NICHT mehr eingebunden
│   │   ├── Principle.astro              ← NUR Startseite
│   │   ├── ChatbotTooltip.astro         ← NUR Startseite (8s-Bubble + Notification-Dot)
│   │   ├── Hero.astro                   ← Unterseiten (Original-Look)
│   │   ├── Cta.astro                    ← Unterseiten (Original-Look)
│   │   ├── Faq.astro                    ← Unterseiten (Original-Look)
│   │   ├── Header.astro                 ← Unterseiten (Original-Look)
│   │   ├── Footer.astro                 ← Unterseiten (Original-Look)
│   │   ├── Chatbot.astro                ← BEIDE Welten (lädt externes Script)
│   │   └── CookieBanner.astro           ← BEIDE Welten (mit CSS-Variable-Fallbacks)
│   ├── layouts/
│   │   ├── LandingLayout.astro          ← NUR Startseite (importiert landing.css)
│   │   └── BaseLayout.astro             ← Alle Unterseiten (importiert global.css)
│   └── styles/
│       ├── landing.css                  ← NUR Cream-Look
│       └── global.css                   ← Original-Look (UNVERÄNDERT seit v1)
├── public/                              ← statische Assets (Favicon, Bilder, robots.txt)
├── dist/                                ← Build-Output (NICHT committen)
├── astro.config.mjs
├── package.json
├── vercel.json
├── _archive/
│   └── PROJECT.md                       ← archivierter Original-Projektplan (vor Cream-Look)
├── DESIGN.md                            ← v1, Original-Look-Tokens + Designsystem-Philosophie
├── STYLE-REFERENCE.md                   ← Single Source of Truth für Cream-Look
└── PROJECT_OVERVIEW.md                  ← DIESE Datei
```

### Layout-Architektur

Die zwei Design-Welten leben über zwei getrennte Astro-Layouts:

**LandingLayout.astro** (NUR Startseite)
- Importiert ausschließlich `landing.css`
- Lädt Roboto Slab + Inter + Instrument Serif
- Enthält ALLE SEO-Inhalte (Schema-LD, OG, Twitter, Favicons, Canonical)
- Bindet KEINEN Header und KEINEN Footer ein — die kommen aus `index.astro`

**BaseLayout.astro** (alle Unterseiten)
- Importiert `global.css`
- Lädt Noto Serif + Manrope
- Enthält ALLE SEO-Inhalte (identisch zu LandingLayout)
- Bindet `Header.astro` und `Footer.astro` ein
- UNVERÄNDERT seit dem Cream-Look-Redesign

**Konsequenz:** Wenn du eine Unterseite zukünftig auch auf den Cream-Look migrierst, importierst du in dieser Seite einfach `LandingLayout` statt `BaseLayout` und nutzt die `Landing*`-Komponenten.

### Aktuelle Startseiten-Struktur (Cream-Look)

Die Startseite besteht aus folgenden Sektionen in dieser Reihenfolge:

1. **Nav** — Logo links, "Gespräch buchen"-Button rechts (KEIN Menu, KEIN Ratgeber-Link, KEIN Topstrip)
2. **LandingHero** — Display-Headline "KI macht dich besser." + Stat-Bar
3. **LandingWasKiMacht** — Sektion 02 mit Sticky-Sidebar "Drei Szenen aus deinem Alltag", Headline endet mit Italic-Bordeaux *"Du wirst nicht unterbrochen."*
4. **Principle** — Sektion 03 "Keine Software. Kein Abo." (Ledger-Pattern i. ii. iii.)
5. **LandingFaq** — Sektion 04 mit Accordion (6 Fragen, 1. standardmäßig offen)
6. **LandingCta** — Sektion 05 mit Sage-Card, Headline *"Zeig uns deine Prozesse."*
7. **LandingFooter** — 5-Spalten-Footer (Mobile als Akkordeon via `<details>`-Element)

Die zwei weiteren Cream-Look-Seiten (`ki-steuerberater`, `ki-automatisierung-workflow`) folgen diesem Pattern — siehe ihre eigenen Page-Files. Verbindlicher Detail-Stand: `STYLE-REFERENCE.md`.

### Wichtige Projekt-Dokumente (im Repo)

| Datei | Inhalt |
|---|---|
| `STYLE-REFERENCE.md` | **Aktuelle** Single Source of Truth für Cream-Look — Tokens, Typografie, Wort-Limits, Patterns, Skelett |
| `DESIGN.md` | v1, beschreibt Original-Look-Tokens und historische Designsystem-Philosophie (mit Hinweis-Block) |
| `_archive/PROJECT.md` | Archivierter Original-Projektplan (vor Cream-Look) |
| `PROJECT_OVERVIEW.md` | Diese Datei |

### Dev-Workflow

```bash
cd /Users/markbergenthal/Claude-Projekte/markmade

git status                # Lage checken
npm run dev               # Dev-Server auf http://localhost:4321
npm run build             # Build testen, sollte 36 Seiten bauen

git add <dateien>
git commit -m "..."
git push                  # → Vercel deployed automatisch
```

### Vercel-URLs

- **Production:** https://www.markmade.de
- **Vercel-Dashboard:** https://vercel.com/dashboard

### Konventionen für Änderungen

**An der Startseite (Cream-Look):**

1. CSS-Änderungen kommen in `src/styles/landing.css` (NICHT in global.css)
2. Komponenten-Änderungen in den `Landing*.astro`-Komponenten
3. Cross-Welt-Konflikte sind unmöglich da Subpages `landing.css` nicht laden

**An den Unterseiten (Original-Look):**

1. Nutzen weiter `BaseLayout.astro` und `Header.astro` / `Footer.astro`
2. Ihre Komponenten (`Hero.astro`, `Cta.astro`, `Faq.astro` ohne Landing-Präfix) leben im `src/components/`-Wurzelverzeichnis
3. KEINE der `Landing*`-Komponenten verwenden

**Wenn eine Unterseite auf Cream-Look migriert wird:**

1. In der Page-Datei `BaseLayout` durch `LandingLayout` ersetzen
2. Statt der alten Komponenten `Nav`, `LandingHero` etc. importieren
3. CSS aus `landing.css` greift automatisch

---

## 2. Chatbot-Backend

### Pfad

```
/Users/markbergenthal/Claude-Projekte/markmade-chatbot/
```

### Was es ist

Express-Server der das **chatbot.js**-Widget ausliefert. Wird in der Hauptseite über `https://markmade-chatbot.onrender.com/chatbot.js` geladen.

### Stack

- **Server:** Express.js (Node)
- **Hosting:** Render.com (Auto-Deploy bei Push)
- **Git-Remote:** `git@github.com:onlinemaster711/markmade-chatbot.git` (SSH)
- **Branch:** `main`

### Wichtige Dateien

| Datei | Zweck |
|---|---|
| `chatbot.js` | Client-Code (Greeting, Quick-Replies, UI-Markup, Backend-Calls) |
| `server.js` | Express-Server der `chatbot.js` ausliefert + Backend-Logik |
| `server-original.js` | Backup-Version des Servers |
| `package.json` | Express, cors, dotenv |

### Wo Texte geändert werden

In `chatbot.js` Zeilen 8-14 leben die statischen Texte:

```js
var BOT_NAME = 'MarkMade KI';
var GREETING = 'Hey! Ich bin der KI-Assistent von MarkMade. Was kann KI bei dir übernehmen? 👋';
var QUICK_REPLIES_INITIAL = [
  'Wo kann KI mir Zeit sparen?',
  'Was kann KI für meinen Betrieb tun?',
  'Wie schnell ist eine KI einsatzbereit?',
  'Wie läuft ein Erstgespräch ab?',
];
```

**Wichtig:** Sonderzeichen werden als Unicode-Escapes gespeichert (`\u00fc`, `\u00e4`). Das Format beibehalten beim Editieren.

### Dev-Workflow

```bash
cd ~/Claude-Projekte/markmade-chatbot
# chatbot.js editieren
git add chatbot.js
git commit -m "..."
git push                  # → Render deployt automatisch (~1-2 Min)
```

---

## 3. Automation-Setup (Instagram/Facebook-Posting)

### Pfad

```
/Users/markbergenthal/markmade/
```

### Was es ist

Das **n8n-basierte Automatisierungssystem** für tägliche Instagram-Karussell-Posts. Komplett separates Projekt — **kein Git-Repo**, läuft nur lokal auf dem Mac.

### Stack

- **n8n** (lokal auf `localhost:5678`, Auto-Start beim Mac-Boot)
- **Puppeteer** für PNG-Export der Slides (1080×1080px)
- **Imgur** als Image-Host (imgbb funktioniert nicht mit Meta)
- **Instagram Graph API** + **Facebook Graph API**
- **Google Sheets** (Service Account) für Tracking
- **Claude API** für Content-Generation

### Wichtige Dateien

| Datei | Zweck |
|---|---|
| `markmade_workflow.json` | Hauptworkflow für n8n |
| `export_slides.js` | Puppeteer-Script für PNG-Rendering |
| `export_journal_slides.js` | Variante für Journal-Format |
| `start.sh` | Startscript |
| `config.env` | API-Keys & Tokens |
| `google_credentials.json` | Service-Account-Credentials für Sheets |
| `fonts/` | Lokal gehostete Noto Serif + Manrope |

### Aktive Credentials (Stand April 2026)

- **Meta Page Access Token:** Ablauf Mai 2026 — manuelle Renewal über `developers.facebook.com/tools/explorer`
- **Facebook App ID:** `945434278191822`
- **Facebook Page ID:** `1060455320488726`
- **Instagram Business Account ID:** `17841433587352622`
- **Google Sheet ID:** `1PQnD-wbqL8R9WKgyNxzYb-aLtGeDHT2nH_SfejKOLEo`
- **Service Account:** `markmade-sheet@subtle-tooling-146223.iam.gserviceaccount.com`

### Posting-Schedule

Cron: `0 8,11,17,19 * * *` mit Day-of-Week-Filter — ein Post pro Tag zu rotierenden Zeiten.

### Wichtige Hinweise

- **Kein Git** — Änderungen direkt im Ordner, kein Versions-Tracking
- **TEST_MODUS-Flag** in den Scripts verhindert Live-Posts während Entwicklung

---

## Schnell-Diagnose: "In welchem Ordner bin ich?"

```bash
pwd                        # zeigt aktuellen Pfad
ls -la
cat package.json
```

| Indiz | Welches Projekt |
|---|---|
| `astro.config.mjs`, `src/pages/`, ~314 Bytes package.json | **Astro-Webseite** |
| `chatbot.js`, `server.js`, ~kleine package.json | **Chatbot-Backend** |
| `markmade_workflow.json`, `export_slides.js`, kein `.git/` | **Automation** |

---

## Andere MarkMade-Pfade auf dem System (Kontext)

| Pfad | Was |
|---|---|
| `~/Claude-Projekte/markmade-ssg/` | Älteres/alternatives Astro-Projekt — **nicht aktiv** |
| `~/Claude-Projekte/_Archive/Homepage-Mark-Docs/` | Alte Versionen, archiviert |
| `~/Claude-Projekte/markmade/Content Auto/` | Worktree, nicht aktiv |

---

## TODOs für zukünftige Chats

1. **Topstrip-Komponente** liegt unbenutzt im Repo (`src/components/Topstrip.astro`) — kann gelöscht werden falls sicher dass Reaktivierung nicht erwünscht
2. **PROJECT.md** wurde nach `_archive/PROJECT.md` verschoben (April 2026), weil sie aktiv irreführenden Workflow-Text enthielt ("BaseLayout für jede neue Seite"). Inhalt zur historischen Referenz erhalten
3. **Migrations-Plan** für Subpages auf Cream-Look — nach Traffic-Priorität, eine Seite pro Iteration
4. **DESIGN.md v1** wurde durch v2 ersetzt — falls nötig, aus Git-Verlauf vor Commit `bfb23c5` rekonstruierbar

---

## Wichtige Commits (Cream-Look-Phase, April 2026)

| Commit | Was |
|---|---|
| `d8ba43f` | Sektion "Was KI heute schon macht" v1 |
| `0081229` | Toten CSS-Code aus index.astro entfernt |
| `bfb23c5` | **Komplettes Cream-Look-Redesign der Startseite** |
| `265bd46` | Headline "Du wirst nicht unterbrochen." |
| `ab90fdd` | Mobile-Footer als Akkordeon |
| `14bccc5` | Footer-Bugfix v1 |
| `56153e1` | **Footer-Fix endgültig** (open-Attribut + JS-Toggle) |
| `ff7c14c` | Topstrip entfernt + Mobile-Sidebar Active-State |
| `724302a` | ChatbotTooltip-Komponente |
| `9974dae` | CTA-Headline: "Zeig uns deine Prozesse" |
| `e5d4531` | Ratgeber-Link aus Header entfernt |
| `3eefc3b` | Header-Menu komplett entfernt (Logo + CTA-Button bleiben) |
| `1f63834` | **Cleanup: 14 Zeilen toter CSS-Code entfernt** |

Im Chatbot-Repo:

| Commit | Was |
|---|---|
| `4aa350a` | Quick-Replies + Greeting auf KI-Agentur-Positionierung |

---

*Diese Datei liegt im Astro-Projekt unter `/Users/markbergenthal/Claude-Projekte/markmade/PROJECT_OVERVIEW.md` und sollte mit committed werden.*
