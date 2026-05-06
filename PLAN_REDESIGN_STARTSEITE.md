# Plan: Re-Design Startseite markmade.de

> **Output-Hinweis:** Mark hat als finalen Plan-Pfad `PLAN_REDESIGN_STARTSEITE.md` im Repo-Root angefordert. Dieser Plan-System-Datei-Pfad ist eine Pflicht-Zwischenstation während Plan-Mode. Nach ExitPlanMode + Approval wird derselbe Inhalt nach `/Users/markbergenthal/Claude-Projekte/markmade/PLAN_REDESIGN_STARTSEITE.md` geschrieben.

---

## 1. Context

Der erste Versuch (Phase 1A–C, 13 Commits lokal) hat eine strukturell korrekte aber visuell durchschnittliche Startseite produziert. Marks Browser-Test-Diagnose:

1. **Hero zu schwach** — Stats-Bar wirkt wie generischer Werbe-Banner
2. **Reihenfolge verwirrend** — Eigene Projekte vor Standard-Services lässt User raten was Skriptgenerator/Garage sind
3. **Service-Tiles wirken wie Eingabefelder** — cream-2 Hintergrund + Border + uniformes Padding = Form-Input-Optik, nicht Service-Tiles
4. **Texte zu groß** — Hero-H1 96 px max, Zone-H2 64 px max — schreit, statt zu sprechen
5. **Alignment-Mix unruhig** — manche Sektionen left-aligned, manche zentriert, kein Schema
6. **Editorial-Charakter fehlt** — sieht aus wie eine durchschnittliche Agentur-Site, kein durchdachter Magazin-Eindruck

**Job der Seite (unverändert):** "Beweise in 30 Sekunden dass MarkMade kompetent ist." Demonstrations-Modus, kein Akquise-Trichter. Hauptsuchanfrage: "KI Agentur Stuttgart". Personas: GF / Marketing / Solo-Selbstständige.

**Was bleibt:** Cream-Look-Tokens (`--cream`, `--bordeaux`, `--olive`, `--ink`-Familie, `--rule`/`--rule-2`), Typografie-System (Roboto Slab + Inter + Instrument Serif — siehe **Sektion 6: Offene Fragen** wegen Brand-Foundation-Diskrepanz), URL-Struktur, alle anderen 33 Pages der Site.

**Was sich ändert:** Sektions-Reihenfolge, visuelle Komposition jeder Sektion, Typografie-Skala (kleiner), Alignment-Disziplin, Klassen-Lexikon (neue Klassen für Editorial-Patterns).

---

## 2. Editorial-Direction (Commitment)

Eine starke Idee — beibehalten über die ganze Seite:

**„Editorial Magazine, nicht Tile-Grid. Typografie und Whitespace machen die Arbeit. Hairlines als Struktur, nicht Dekoration. Asymmetrie als bewusste Komposition. Cream-Look bleibt — aber feiner, ruhiger, knapper."**

Konkrete Disziplin:

| Regel | Anwendung |
|---|---|
| **Whitespace ist Luxus** (Brand-Foundation Prinzip 1) | Section-Padding hochziehen, max-width Content-Spalten enger setzen, vertikale Atem-Pausen zwischen H2 und Body |
| **Typografie macht die Arbeit** (Prinzip 5) | Keine Icons. Keine dekorativen Boxen. Numerale (Nº 01) und italic-bordeaux Akzente sind das Inventar |
| **Konsistente Alignment-Disziplin** | Hero, Sektionen 2–5 **alle left-aligned** (Headlines + Body). Sektion 6 (CTA) **bewusst centered** — als „closing moment" gerahmt durch Sage-Card |
| **Bordeaux sparsam** (Prinzip 3) | Bordeaux nur für: (a) `.btn` background, (b) italic-em in Headlines, (c) `.kicker .rule` 1-px-Strich, (d) Eyebrow-Numerale „Nº 01" in Editorial-Listen, (e) `.faq-q .qnum` |
| **Asymmetrie, kein Symmetrie-Grid** | Vertikale Editorial-Listen statt 4-Tile-Cards. Magazin-Spread mit alternierendem Bild/Text statt 2-Card-Side-by-Side |
| **Texte kleiner** | H1 / H2 / Body um 15–20 % runter — editorial heißt feiner, nicht fetter |

**AI-Slop-Test:** Keine identischen Card-Grids mit „Icon → Headline → Pitch" Pattern. Keine Glassmorphism. Keine Rounded-Border-Highlights. Keine Center-Stack-Layouts.

---

## 3. Neue Sektions-Reihenfolge

```
1. Hero
2. Was wir bauen — Standard (3 Services)        ← User sieht sofort was er bekommen kann
3. Was sonst möglich ist — Eigene Projekte      ← Custom-Beweis als „und was sonst noch geht"
4. Wie wir arbeiten (3 Schritte)
5. Häufige Fragen (FAQ)
6. Dein nächster Schritt (CTA)
```

Logik: Standard zuerst (Erwartbare Services) → Eigenes danach (Custom-Beweis). Die alte „Custom-Lösung"-Tile entfällt; sie wird durch die Eigenen Projekte abgedeckt.

---

## 4. Section-by-Section Design

### 4.1 Hero — Asymmetrisch links, KEINE Stats-Bar

**Visuelle Idee:** Editorial-Opener wie das Cover einer Magazin-Ausgabe. Headline links, vast Whitespace rechts. Kein Stat-Block, kein Kompositions-Crutches. Atem.

**ASCII-Skizze (Desktop):**

```
┌────────────────────────────────────────────────────────────────────┐
│                                                                       │
│  KI-AGENTUR · STUTTGART  ← caps eyebrow, kein <hr>                  │
│                                                                       │
│  KI macht                ← clamp(36, 5.2vw, 80) Roboto Slab 700      │
│  dich besser.            ← „besser." italic Instrument Serif         │
│                            color:--bordeaux                          │
│                                                                       │
│  KI-AGENTUR AUS STUTTGART ← micro caps subtitle, color:--muted       │
│                                                                       │
│  Wir bauen eigene KI-     ← italic Instrument Serif                 │
│  Anwendungen. Und über-     clamp(17, 1.8vw, 22)                    │
│  setzen das, was wir...     max-width: 50ch                         │
│                                                                       │
│  [ Gespräch buchen → ]   ← einziger primary CTA                     │
│                                                                       │
│  ↓ Was wir bauen          ← dezenter scroll-link                     │
│                                                                       │
│                                                                       │
│  (BREATH — keine Stats-Bar, kein Element rechts)                    │
│                                                                       │
└────────────────────────────────────────────────────────────────────┘
```

**Mobile:** identisches Layout, einfach in einer schmaleren Spalte. Asymmetrie → vertikales Stacking.

**Begründung:**
- Brand-Foundation: „Whitespace ist Luxus. Wenn es zu leer wirkt, ist es wahrscheinlich richtig"
- Phase-1-Hero war horizontal-zentriert mit 4-Spalten-Stats-Bar. Looked like every B2B SaaS landing
- Asymmetrische links-Komposition + leeres rechts ist editorial-Konvention (Magazin-Cover, Gallery-Wall-Text)
- Stats-Bar ist redundant: Sektion 3 (Eigene Projekte) liefert echten Beweis, statt generischer „24/7"-Behauptung

**Klassen-Strategie:**
- **Reuse:** `.hero` (section), `.hero-grid` (mit Layout-Override), `.hero-h1` (mit Größen-Override), `.hero-h1 .em`, `.hero-h1-subtitle` (Phase 1A), `.hero-sub p` (mit Größen-Override), `.hero-cta`, `.hero-scroll-link` (Phase 1A), `.btn`, `.btn-lg`, `.kicker` (Eyebrow), `.reveal`
- **Drop:** `.hero-stats`, `.stat`, `.stat .num`, `.stat .lbl` markup wegspeisen (CSS in landing.css bleibt als dead code — Phase-2-Cleanup)
- **Modify in landing.css:**
  - `.hero-grid { grid-template-columns: minmax(0, 720px); justify-content: flex-start; gap: clamp(20px, 3vw, 36px); }` — von center zu flex-start
  - `.hero-h1 { text-align: left; font-size: clamp(36px, 5.2vw, 80px); }` — von center, 96px-max zu left, 80px-max
  - `.hero-meta { justify-content: flex-start; }` — eyebrow links
  - `.hero-sub { display: block; max-width: 50ch; }` — von 3-col-grid mit hr-flanken zu plain block
  - `.hero-sub p { font-size: clamp(17px, 1.8vw, 22px); text-align: left; }` — kleiner und links
  - `.hero-cta { justify-content: flex-start; }` — buttons links
- **Neue Klassen:** keine

**Inhalts-Texte (1:1 aus aktuellem State, gut formuliert):** 
- Eyebrow: "KI-Agentur · Stuttgart"
- H1: "KI macht / dich besser." (besser. in `.em`)
- Subtitle: "KI-Agentur aus Stuttgart"
- Subline: "Wir bauen eigene KI-Anwendungen. Und übersetzen das, was wir gelernt haben, in Lösungen für deinen Betrieb."
- Primary CTA: "Gespräch buchen →"
- Scroll: "↓ Was wir bauen"

---

### 4.2 Was wir bauen — Standard (3 Services)

**Visuelle Idee:** Editorial vertikale Liste. Jeder Service ist eine ZEILE in einer numerierten Magazin-TOC. Nº 01 / Nº 02 / Nº 03 als italic-olive-Numerale links, Service-Name + Pitch in der Mitte, Capabilities + Link rechts. Hairlines trennen die Zeilen.

**Wichtig:** Reuse vom bestehenden `.steps-list` / `.step`-Pattern aus `LandingWasKiMacht.astro` (Datei nicht mehr eingebunden, CSS aber noch in landing.css). Das Pattern existiert bereits — nur Inhalt anders.

**ASCII-Skizze (Desktop, 3 Services):**

```
WAS WIR BAUEN

Drei Standard-Lösungen, die sich in fast jedem Betrieb rechnen.   ← left-aligned zone-h2

Standard heißt nicht von der Stange — wir richten sie auf deinen   ← lead, max-width 50ch
Betrieb ein. Mit deiner Stimme, deinem Wissen, deinem Design.

──────────────────────────────────────────────────────────────────────────────
                                                                                
  Nº 01    Telefonassistent                            · Spricht in deiner Stimme
                                                       · Termine direkt im Kalender
           Du gehst nie mehr ans Telefon. KI nimmt    · 24/7 erreichbar
           an, qualifiziert vor, schickt dir nur                                
           was wirklich wichtig ist.                  Mehr →                   
                                                                                
──────────────────────────────────────────────────────────────────────────────
                                                                                
  Nº 02    E-Mail-Automatisierung                     · Sortiert nach Wichtigkeit
                                                       · Beantwortet Standard-Anfragen
           Dein Postfach arbeitet alleine. Du         · Lernt deinen Stil
           siehst nur was deine Aufmerksamkeit                                  
           braucht.                                    Mehr →                  
                                                                                
──────────────────────────────────────────────────────────────────────────────
                                                                                
  Nº 03    Webseiten-Chatbot                          · Trainiert auf deine Inhalte
                                                       · Übergibt an dich wenn nötig
           Kunden bekommen sofort Antworten —         · Schickt qualifizierte Anfragen
           auch nachts, auch am Wochenende.                                     
                                                       Mehr →                   
                                                                                
──────────────────────────────────────────────────────────────────────────────
```

**Mobile:** stack vertikal:
- Numeral oben (klein, italic)
- Service-Name (medium serif)
- Pitch
- Capabilities-Liste
- Link

**Begründung:**
- Editorial Magazine TOC-DNA: numerierte Articles, hairline-Separator
- Phase-1-Tile-Grid wurde als „Eingabefelder" wahrgenommen → diese Lösung hat ZERO Boxes, nur Type + Hairlines
- Frontend-design Skill: „DON'T use identical card grids" + „DON'T put icons above every heading" — beide vermieden
- Reuse aus bestehendem `.step`-Pattern: keine neuen Layout-Klassen nötig (heavy class reuse)
- Capabilities als rechte Spalte gibt der Sektion narrative Tiefe ohne Card-Form

**Klassen-Strategie:**
- **Reuse:** `.zone`, `.container`, `.kicker`, `.zone-h2` (ohne `.center` — left-aligned!), `.reveal`, `.steps-list`, `.step`, `.step .index` (italic-olive Numeral), `.step .body h3`, `.step .body p`, `.project-caps` + `::before` (Bordeaux-Strich-Bullets), `.project-link`
- **Drop:** das gesamte Phase-1A-`.services`, `.services-grid`, `.service-tile`, `.service-tile--large` Klassenset wird komplett ersetzt. Markup wechselt von `<a class="service-tile">` zu `<article class="step">`.
- **Modifier-Klasse (NEU):** `.step--service` — Modifier auf `.step` für die rechte 3-Spalten-Aufteilung. Existing `.step` hat `grid-template-columns: 80px 1fr 200px` (Numeral / Body / Compact-Meta). Service-Variant braucht: `grid-template-columns: 100px 1fr 280px` (Numeral / Body / Capabilities-Spalte breiter).
- **Begründung neue Klasse:** Capability-Spalte in Services unterscheidet sich strukturell von der `.step .meta` Mini-Spalte. Eine Modifier-Klasse erlaubt Reuse von 90 % `.step` + überschreibt nur die rechte Spalten-Geometrie.
- **Drop CSS** in landing.css: `.services` (cream-2 bg), `.services-grid` (2x2 areas), `.service-tile`, `.service-tile--large`, `.service-tile .arrow` — alles weg.

**Eyebrow-Numerale „Nº 01":** Ich nutze direkt das `.step .index` Pattern (italic Instrument Serif, olive). Aber als Inhalt nicht „01" sondern „Nº 01" — kleines Magazin-Detail. Lässt sich inline im `<div class="index">` setzen.

**Inhalt:**
- Eyebrow: „Was wir bauen"
- H2: „Drei Standard-Lösungen, die sich in fast jedem Betrieb rechnen."
- Lead: „Standard heißt nicht von der Stange — wir richten sie auf deinen Betrieb ein. Mit deiner Stimme, deinem Wissen, deinem Design."
- Service 1: Nº 01 / Telefonassistent / Pitch + 3 Caps / Link `/ki-telefonassistent`
- Service 2: Nº 02 / E-Mail-Automatisierung / Pitch + 3 Caps / Link `/ki-email`
- Service 3: Nº 03 / Webseiten-Chatbot / Pitch + 3 Caps / Link `/chatbot-stuttgart`

---

### 4.3 Was sonst möglich ist — Eigene Projekte

**Visuelle Idee:** Magazin-„Feature Article". Zwei Projekte als alternierende Spreads. Skriptgenerator: Bild links 40 %, Inhalt rechts 60 %. Garage: Bild rechts 40 %, Inhalt links 60 % (zig-zag). Beide Projekte verdienen Detail-Tiefe weil sie der HAUPT-Beweis-Punkt der Seite sind.

**ASCII-Skizze (Desktop, beide Projekte):**

```
WAS SONST MÖGLICH IST

Wenn nichts von der Stange passt — bauen wir Eigenes.   ← left-aligned zone-h2

Zwei Beispiele aus eigener Hand. Mit den gleichen Werkzeugen,
die wir für deinen Betrieb einsetzen.

──────────────────────────────────────────────────────────────────────────────
                                                                              
                                LIVE · KI-Tool für Content-Creator           
┌──────────────────────────┐                                                  
│                          │   Skriptgenerator                                
│   [Image / SVG-          │   ← clamp(40, 5vw, 56)px serif                  
│    Platzhalter]          │                                                  
│                          │   Von der Idee zum fertigen Skript in           
│   40%                    │   Minuten. Skriptgenerator schreibt             
│                          │   YouTube-, Reels- und Podcast-Skripte,         
│                          │   die nach dir klingen — nicht nach KI.         
│                          │                                                  
└──────────────────────────┘   · Personalisiert auf deinen Stil              
                               · Mehrere Plattform-Formate                   
                               · Direkt einsetzbar                           
                                                                              
                               skriptgenerator.com →                          
                                                                              
──────────────────────────────────────────────────────────────────────────────
                                                                              
   IN GESCHLOSSENER BETA · Voice-First Bordbuch                              
                                                            ┌───────────────┐
   Garage                                                   │               │
   ← clamp(40, 5vw, 56)px serif                             │  [Image / SVG]│
                                                            │               │
   Oldtimer-Sammler sprechen einen Satz, Garage erkennt    │  40%          │
   Fahrzeug, Werkstatt, Kosten und legt den Eintrag        │               │
   automatisch an. Voice-Input mit KI, die Sammler-        │               │
   Sprache versteht.                                        └───────────────┘
                                                                              
   · Sprache wird zu Datenbank-Eintrag                                       
   · Versteht Sammler-Begriffe (Pagode, Käfer)                              
   · Senior-freundliches Interface                                            
                                                                              
   (kein Link — Beta)                                                         
                                                                              
──────────────────────────────────────────────────────────────────────────────
```

**Mobile:** Bild stackt IMMER über Inhalt (kein Alternieren). Order: Skriptgenerator → Garage.

**Begründung:**
- Magazin-Feature-Article-Pattern: das stärkste Editorial-Moment der Seite verdient die meiste Visualität
- Asymmetrie via Image-Alternation = magazinhafte Komposition (Vogue, NYT-Style)
- Status-Badge wandert von Card-Foot-Pill zu Inline-Eyebrow-Tag — weniger Form-y, mehr editorial
- Project-Name kann hier RICHTIG groß sein (display-Headline-Niveau): clamp(40, 5vw, 56) — Mark wollte zwar „Texte kleiner" aber das gilt für die generischen H2; Project-Names sind die FEATURE-Headlines, da darf gepusht werden

**Klassen-Strategie:**
- **Reuse:** `.zone`, `.container`, `.kicker`, `.zone-h2` (ohne `.center`), `.reveal`, `.project-media` + img/svg-styles, `.project-pitch`, `.project-caps`, `.project-link`, `.project-status`, `.status-live`, `.status-beta`
- **Drop:** `.projects-head`, `.projects-grid`, `.project-card`, `.project-tag`, `.project-foot`, `.project-name` (alle aus Phase 1A — die werden durch das neue Spread-Pattern ersetzt)
- **Neue Klassen (5):**
  - `.proj-spread` — Container für ein Projekt-Spread (grid 2-Spalten 40 / 60)
  - `.proj-spread--mirror` — Modifier für das 2. Projekt (image-rechts, content-links)
  - `.proj-feature-name` — sehr große Display-Headline für Project-Name (clamp(40, 5vw, 56))
  - `.proj-meta` — Inline-Eyebrow-Zeile mit Status + Tagline (z. B. „LIVE · KI-Tool für Content-Creator")
  - `.proj-spread > .project-media` Override — das image hat hier 40 % Container-Höhe statt 16:10 Aspect (lass mich das nochmal prüfen — vielleicht reicht 16:10 mit 100 % der Spalten-Width)

Begründung: Spread-Layout ist strukturell verschieden vom alten Card-Grid. Reuse von `.project-pitch` / `.project-caps` / `.project-link` aus Phase 1A bleibt — diese Type-Klassen sind ortsunabhängig.

**Mobile-Override:** Bei `< 760px` löst `.proj-spread` und `.proj-spread--mirror` zu `display: flex; flex-direction: column` auf. Image immer oben, Content unten.

**Inhalt:**
- Eyebrow: „Was sonst möglich ist"
- H2: „Wenn nichts von der Stange passt — bauen wir Eigenes."
- Lead: „Zwei Beispiele aus eigener Hand. Mit den gleichen Werkzeugen, die wir für deinen Betrieb einsetzen."
- Skriptgenerator: SVG-Platzhalter aus Phase 1B bleibt; Tagline „LIVE · KI-Tool für Content-Creator"; Pitch/Caps/Link aus aktuellen Texten
- Garage: SVG-Platzhalter; Tagline „IN GESCHLOSSENER BETA · Voice-First Bordbuch"; Pitch/Caps; kein Link

---

### 4.4 Wie wir arbeiten

**Visuelle Idee:** Editorial vertikale Liste mit Numeral + Headline + Body + Duration als rechte Marginalia. Strukturell ähnlich zu Sektion 4.2 — aber bewusst SCHMALER weil 3 Schritte (nicht 3 Services), und kein „mehr →"-Link. Process, nicht Sales.

**Differenzierung gegenüber 4.2:** Sektion 4.2 hat 3 Spalten (Num / Body / Caps+Link). Sektion 4.4 hat 2 Spalten (Num / Body) mit Duration als Marginalia rechts oben (nicht als eigene Spalte). Subtil andere Rhythmik vermeidet „zwei numerierten Listen direkt hintereinander = monoton".

**ASCII-Skizze (Desktop):**

```
WIE WIR ARBEITEN

Keine Software. Kein Abo. Keine Überraschungen.   ← left-aligned

──────────────────────────────────────────────────────────────────────────────
                                                                                
  i.       Du sagst uns wie du arbeitest.            30 MIN ERSTGESPRÄCH        ← marginalia rechts oben
                                                                                
           Erstgespräch. Du erzählst was bei dir Zeit frisst, wir hören        
           zu. Am Ende weißt du was KI bei dir konkret übernehmen kann.        
                                                                                
──────────────────────────────────────────────────────────────────────────────
                                                                                
  ii.      Wir bauen die KI die das übernimmt.        1–3 WOCHEN AUFBAU         
                                                                                
           Wir richten die Lösung ein, mit deinem Wissen, deiner               
           Stimme, deinem Design. Du musst nichts selbst tun.                  
                                                                                
──────────────────────────────────────────────────────────────────────────────
                                                                                
  iii.     Einmal bezahlt. Dauerhaft im Einsatz.      AB TAG 1 PRODUKTIV        
                                                                                
           Faire einmalige Investition statt monatliches Abo. Wenn sich        
           bei dir was ändert, passen wir die KI an. Das gehört dazu.          
                                                                                
──────────────────────────────────────────────────────────────────────────────
```

Numeral als `i. / ii. / iii.` (Cream-Look-DNA, behalten), italic Instrument Serif, olive. Größer als bisher (von 14 px → ~24 px italic).

**Mobile:** Numeral klein oben, dann Headline, dann Body, Duration als kleines Caps-Tag drunter.

**Begründung:**
- Die aktuelle Phase-1-Variante (`.ledger-rich` mit 3-Spalten-Grid-Border-Frame) erbt von der alten Ledger-Optik — wirkt wie eine Bilanz-Tabelle
- Editorial vertikale Liste mit hairline-Separators ist konsistenter mit Sektion 4.2 — einheitlicher Rhythmus
- Duration als Marginalia (rechts oben, nicht als eigene Bottom-Spalte) ist Magazin-Konvention für „Sidebar-Fact"

**Klassen-Strategie:**
- **Reuse:** `.zone`, `.container`, `.principle`, `.kicker`, `.reveal`
- **Drop:** das gesamte `.ledger`, `.ledger > div`, `.ledger .step-num`, `.ledger .step-text`, `.ledger-rich` und alle Modifikator-Klassen aus Phase 1A. Wir nutzen NICHT mehr das 3-Spalten-Grid mit border-frame.
- **Neue Klassen (3):**
  - `.principle-list` — vertikaler List-Container (analog zu `.steps-list` aber spezifisch für Process)
  - `.principle-row` — eine Zeile (Numeral + Body, Duration als ::before oder dedicated span)
  - `.principle-num` — italic Instrument Serif, olive, Roman Numeral
  - `.principle-meta` — Duration als small Caps Bordeaux, rechts oben in der Row positioniert

Alternative: stark `.step`-Pattern wiederverwenden mit Modifier `.step--principle`. Spart 2 neue Klassen aber forciert Naming-Inkonsistenz (Process != Step in semantischer Hinsicht).

**Empfehlung:** kleines neues Klassen-Set für Klarheit. 3 neue Klassen sind moderat.

**Inhalt:** unverändert aus Phase 1A — Texte sind brand-konform.

---

### 4.5 FAQ

**Visuelle Idee:** Single-column Editorial-Liste. Headline links, Lead darunter (nicht 2-spaltig). Item-Rendering bleibt im Kern wie Phase 1A, aber Headline-Bruch behoben und Eyebrow-Nummer raus.

**ASCII-Skizze:**

```
HÄUFIGE FRAGEN

Häufige Fragen.    ← left-aligned, KEIN .num im Eyebrow mehr ("04" raus)

Sechs Fragen, die wir in fast jedem Erstgespräch hören. Wenn deine
fehlt — frag uns einfach.    ← lead darunter, single-column

──────────────────────────────────────────────────────────────────────────────
  Nº 01    Was kann man alles mit KI bearbeiten?                    [+]   ← no permanent bordeaux
──────────────────────────────────────────────────────────────────────────────
  Nº 02    Wie hilft mir das tatsächlich in meinem Alltag?          [+]
──────────────────────────────────────────────────────────────────────────────
  Nº 03    Ich bin kein Technik-Experte — geht das trotzdem?        [+]
──────────────────────────────────────────────────────────────────────────────
  ...
```

**Begründung:**
- Mark hat den 2-Spalten-Head (Headline links + Lead rechts) als „unentschieden" markiert
- Single-column-Head ist konsistent mit den anderen left-aligned Sektionen
- „Nº 01" Numeral statt nackter „01" Nummer = Editorial-Konsistenz mit Sektion 4.2

**Klassen-Strategie:**
- **Reuse:** `.zone`, `.container`, `.kicker`, `.zone-h2`, `.faq-list`, `.faq-item`, `.faq-q`, `.faq-q .qnum`, `.faq-q .qtxt`, `.faq-q .icon`, `.faq-a`, `.faq-a-inner`, `.reveal`
- **Drop:** das aktuelle `.faq-head { grid-template-columns: 1fr 1fr }` 2-spaltige Layout
- **Modify in landing.css:**
  - `.faq-head { display: block; max-width: 720px; }` — aus 2-Spalten-Grid wird Block
  - `.faq-head .lead { justify-self: unset; max-width: 50ch; margin-top: 12px; }` — Lead unter H2 statt rechts
  - `.kicker .num` Span im LandingFaq.astro Markup entfernen
- **Numerale-Format:** Inhalt der `.qnum` von „01" auf „Nº 01" ändern (Konsistenz mit Sektion 4.2)
- **Bordeaux-Hover-Bug:** check ob das ein CSS-Bug ist (`.faq-item.open .qtxt` hat dauerhaft bordeaux?). Wahrscheinlich Markup-Initialzustand — lese im Build-Output
- **Neue Klassen:** keine

**Inhalt:** unverändert.

---

### 4.6 CTA — bewusst zentriert als „closing moment"

**Visuelle Idee:** Sage-Card als visueller Frame der den Alignment-Wechsel rechtfertigt. Inhalt zentriert wie Phase 1A. Nur Typografie-Skala leicht reduzieren.

**Begründung für Alignment-Bruch:**
- Mark sagte: „kein Mix INNERHALB einer Sektion". Across-section-Wechsel ist OK wenn intentional
- CTA ist das Closing-Moment — die zentrale Frame-Struktur (Sage-Card) signalisiert visuell „hier ist es anders, hier passiert was"
- Centered im Sage-Card vs. Left-aligned im Cream-BG = klarer Kontrast = klarer Effekt

**Klassen-Strategie:**
- **Reuse:** alle bestehenden `.cta-zone`, `.cta-card`, `.cta-grid`, `.cta-grid h2` (mit kleinerem font-size), `.cta-grid p`, `.cta-promise` (Phase 1A), `.actions`, `.cta-meta`, `.btn`, `.btn-lg`
- **Modify:** `.cta-grid h2 { font-size: clamp(36px, 5vw, 64px); }` (von 80px max auf 64px max — Reduktion analog Sektionen 2–5)
- **Neue Klassen:** keine

**Inhalt:** unverändert aus Phase 1A.

---

## 5. Typografie-Skala — Reduktions-Tabelle

Mark: „Texte zu groß insgesamt. Editorial heißt feiner, nicht fetter."

| Token / Klasse | Phase 1A (current) | Re-Design (proposed) | Reduktion |
|---|---|---|---|
| `.hero-h1` | `clamp(40px, 6vw, 96px)` | `clamp(36px, 5.2vw, 80px)` | -17 % max |
| `.hero-sub p` | `clamp(20px, 2.4vw, 26px)` | `clamp(17px, 1.8vw, 22px)` | -15 % max |
| `.zone-h2` | `clamp(36px, 5.4vw, 64px)` | `clamp(32px, 4.5vw, 52px)` | -19 % max |
| `.cta-grid h2` | `clamp(40px, 6vw, 80px)` | `clamp(36px, 5vw, 64px)` | -20 % max |
| `.principle h2` | `clamp(36px, 5.5vw, 64px)` | (alias auf `.zone-h2` setzen) | konsistent |
| `.proj-feature-name` (NEU) | — | `clamp(40px, 5vw, 56px)` | (Display-Niveau für Feature) |

Body-Größen bleiben unverändert (15.5 px etc.).

---

## 6. Offene Fragen — bitte vor Implementierung klären

### 6.1 Typografie-Diskrepanz Brand-Foundation vs. landing.css ⚠️

**Brand Foundation v1.0 sagt:** Headlines = Noto Serif, Body = Manrope.
**Tatsächliche `landing.css` lädt:** Roboto Slab + Inter + Instrument Serif (via Google Fonts `@import` in landing.css:8).
**Marks Brief sagt:** „Typografie-System bleibt (Noto Serif, Manrope)" — basiert auf Brand-Foundation, nicht auf aktueller Implementation.

**Dieser Plan geht aktuell aus von:** Beibehalt der **landing.css-Implementation** (Roboto Slab + Inter + Instrument Serif). Begründung: Font-Migration ist ein eigenes größeres Projekt und nicht Teil eines Re-Designs der Komposition.

**Bitte klären:** Soll der Re-Design die `landing.css`-Schriften (Roboto Slab + Inter + Instrument Serif) behalten, oder gleichzeitig auf Brand-Foundation-Schriften (Noto Serif + Manrope) migrieren?

**Empfehlung:** Behalte Roboto Slab + Inter + Instrument Serif für dieses Re-Design. Dokumentiere die Brand-Foundation-Diskrepanz als separates Phase-3-Item. Wenn migriert wird, muss STYLE-REFERENCE.md, DESIGN.md UND Brand-Foundation v1.0 alle aktualisiert werden — Single Source of Truth braucht Konsistenz.

### 6.2 Section-Padding hochziehen?

Brand-Foundation: „Whitespace ist Luxus". Aktueller `--section-pad: clamp(72px, 10vw, 160px)`. Vorschlag: hochziehen auf `clamp(96px, 12vw, 200px)` für mehr editorialen Atem. **Ist das gewollt oder zu viel?**

### 6.3 LandingWasKiMacht.astro endgültig löschen?

Im Plan-Update Phase 1 wurde die Datei behalten („eventuelle Wiederverwendung"). Mit dem Re-Design ist sie endgültig obsolet. **Jetzt löschen oder weiter behalten?** Empfehlung: löschen, der Code lebt im Git-Verlauf.

### 6.4 Editorial-Numerale „Nº 01" ja/nein?

Magazin-Konvention. Subtil-italic-olive. Verleiht der Seite klaren Editorial-DNA. **Aber:** könnte für ungeübte Leser pretentiös wirken. Alternative: einfach „01" (ohne Nº). **Bitte entscheiden.**

### 6.5 Hero — wirklich keine Stats / kein Element rechts?

Mark sagt: „nichts — Atem reicht". Das ist mutig. Risk: User scrollt direkt weiter ohne Hero-Inhalt aufzunehmen. **Mitigation-Optionen:**
- (A) Wirklich nichts — purer Whitespace
- (B) Ein einzelnes Pull-Quote rechts unten (z. B. von einem Bestandskunden, oder ein Brand-Slogan-Echo)
- (C) Eine kleine vertikale Side-Marginalia rechts mit „SINCE 2024" oder „STUTTGART · DACH"

**Empfehlung:** (A) erstmal. Im Browser-Test entscheiden ob (C) als feines Detail nötig ist.

---

## 7. CSS-Strategie zusammengefasst

**Token-Welt unverändert:** Alle Cream-Look-Tokens in `:root` bleiben. Nur `--section-pad` evtl. hochziehen (Frage 6.2).

**Reuse-Bilanz:** 

| Sektion | Bestehende Klassen wiederverwendet | Neue Klassen |
|---|---|---|
| Hero | 11 | 0 |
| Standard-Services | 13 | 1 (`.step--service`) |
| Eigene Projekte | 11 | 5 (`.proj-spread`, `--mirror`, `.proj-feature-name`, `.proj-meta`, override-styles) |
| Wie wir arbeiten | 5 | 4 (`.principle-list`, `.principle-row`, `.principle-num`, `.principle-meta`) |
| FAQ | 13 | 0 |
| CTA | 9 | 0 |
| **Total** | **62 reuse** | **10 neu** |

**Drop-Bilanz:** Phase 1A neue Klassen die wegfallen:
- `.services`, `.services-grid`, `.service-tile`, `.service-tile--large`, `.service-tile .arrow` — alle weg (Standard-Services rebuild)
- `.projects-head` (Pool mit `.services-head`), `.projects-grid`, `.project-card`, `.project-tag`, `.project-foot` — weg (Spread-Pattern)
- `.ledger-rich`, `.ledger-step`, `.ledger-meta`, `.ledger-rich > .ledger-step` Mobile-Block — weg (Editorial-List)
- `.hero-stats`, `.stat`, `.stat .num`, `.stat .lbl` Markup weg; CSS bleibt zunächst als dead code (Phase-2-Cleanup)

**Aufräum-Bilanz nach Re-Design:**
- Netto NEUE Klassen seit Phase-1-Start: ~13 (statt aktuell ~22)
- `landing.css` wird leichter, nicht schwerer

---

## 8. Implementation Order

Pro Commit ein Schritt — klar reviewbar. Keine Big-Bang-Commits außer den initialen Layout-Refactors.

1. **Commit:** Hero-Refactor (`LandingHero.astro` + `landing.css` Hero-Block left-align + smaller scale + drop stats markup)
2. **Commit:** Standard-Services-Rebuild (`LandingServices.astro` neu auf `.step`-Pattern, `.step--service` Modifier, Drop alte Tile-CSS)
3. **Commit:** Eigene-Projekte-Rebuild (`LandingProjects.astro` neu mit Spread-Pattern, neue 5 Klassen, Drop alte Card-CSS)
4. **Commit:** Principle-Rebuild (`Principle.astro` von `.ledger-rich` zu `.principle-list`, neue 4 Klassen, Drop alte Ledger-CSS)
5. **Commit:** FAQ-Fix (`LandingFaq.astro` Eyebrow-Nummer raus, Numerale auf „Nº 01"-Format, `.faq-head` von 2-col zu single-col, Bordeaux-Hover-Bug analysieren)
6. **Commit:** CTA-Type-Reduktion (`landing.css` `.cta-grid h2` font-size runter)
7. **Commit:** Sektions-Reordering in `index.astro` (LandingServices VOR LandingProjects)
8. **Commit:** Typografie-Skala-Reduktion (alle other H1/H2 Werte runter wenn nicht schon in obigen Schritten erledigt)
9. **Commit:** STYLE-REFERENCE.md update (neue Patterns dokumentieren, alte Patterns entfernen)
10. **Commit:** Optional `LandingWasKiMacht.astro` löschen (offene Frage 6.3)

Build-Verifikation nach jedem Commit. Browser-Test durch Mark nach Commit 7 (Sektions-Reordering = erste vollständige neue Seite). Iteration bei Bedarf vor Phase 1B.

---

## 9. Risk Analysis & Backout

| Risiko | Wahrscheinlichkeit | Mitigation | Backout |
|---|---|---|---|
| Editorial vertikale Liste in Sektion 4.2 + 4.4 wirkt repetitiv | mittel | Strukturelle Subtilität: 4.2 hat 3 Spalten + Caps + Link, 4.4 hat 2 Spalten + Marginalia-Duration. Inhalts-Tonalität different (Sales vs. Process) | Falls visuell zu monoton: 4.4 zurück auf horizontalen Ledger (alte Optik), reverse `Principle.astro` Commit |
| Asymmetrisch-links Hero wirkt "leer" / unprofessionell | mittel | Brand-Foundation Prinzip 1 schützt. Aber falls Browser-Test zu kritisch: Option (C) aus Frage 6.5 — kleine Marginalia rechts hinzufügen | Reverse Commit 1 zurück auf Phase-1A-Hero |
| Magazin-Spread für Eigene Projekte wirkt zu opulent | niedrig | Spreads kommen erst NACH Standard-Services — User hat Service-Kontext und versteht „dieses Projekt ist ein Beispiel was wir können" | Option B: zurück auf einfaches 2-Card-Side-by-Side |
| Drop der Stats-Bar verliert „Proof"-Element | niedrig | Eigene Projekte ersetzen Stats mit echtem Beweis. Stats waren generisch („24/7" sagt nichts) | — kein Backout nötig, Stats bringen nichts |
| Typografie-Reduktion macht die Seite zu zurückhaltend | niedrig | -15-20 % ist moderat. Editorial-Magazin-Look braucht keine 96 px H1 | Erhöhe um +10 % falls zu schwach |
| Brand-Foundation-Schrift-Diskrepanz wird zur Reibungsfläche | mittel | Frage 6.1 jetzt klären, NICHT auf später schieben | — Plan-Frage zuerst beantworten |

---

## 10. Verification

Nach jedem Commit:
- `npm run build` exit 0
- `dist/index.html` grep auf erwartete Klassen + Inhalt
- Nur betroffene Files in der Stage

Nach Commit 7 (Sektions-Reordering):
- `npm run dev` lokal starten
- Browser-Test durch Mark: Desktop, 768 px, 375 px
- DevTools Console: keine Errors
- Smoke-Tests: Reveal-Animationen funktionieren, alle Hover-States, alle Links klickbar, FAQ-Accordion funktioniert

Nach allen Commits + Browser-Approval:
- Optional Push nach Vercel — Mark entscheidet
- Phase 1B (Schema.org JSON-LD) als separater Schritt

---

## 11. Critical Files

**Modify:**
- `/Users/markbergenthal/Claude-Projekte/markmade/src/components/LandingHero.astro` (komplettes File, ~30 Zeilen statt 47)
- `/Users/markbergenthal/Claude-Projekte/markmade/src/components/LandingServices.astro` (komplettes Re-Build)
- `/Users/markbergenthal/Claude-Projekte/markmade/src/components/LandingProjects.astro` (komplettes Re-Build, SVG-Platzhalter behalten)
- `/Users/markbergenthal/Claude-Projekte/markmade/src/components/Principle.astro` (komplettes Re-Build)
- `/Users/markbergenthal/Claude-Projekte/markmade/src/components/LandingFaq.astro` (Markup-Anpassung: Eyebrow-Nummer raus, Numerale-Format)
- `/Users/markbergenthal/Claude-Projekte/markmade/src/styles/landing.css` (großer Refactor: drop Phase-1A-Klassen-Sets, neue Editorial-Patterns)
- `/Users/markbergenthal/Claude-Projekte/markmade/src/pages/index.astro` (Reihenfolge LandingServices VOR LandingProjects)
- `/Users/markbergenthal/Claude-Projekte/markmade/STYLE-REFERENCE.md` (am Ende)

**Optional delete:** `/Users/markbergenthal/Claude-Projekte/markmade/src/components/LandingWasKiMacht.astro` (Frage 6.3)

**Read-only references:**
- `MarkMade_Brand_Foundation.md` (Tone, Prinzipien, Slogans)
- `DESIGN.md` (Token-Tabelle)
- `STYLE-REFERENCE.md` (existing Patterns)
- frontend-design Skill (DON'Ts)

---

## 12. Phase 1B (nach Re-Design) — Schema.org JSON-LD

Wie im ursprünglichen `PLAN_STARTSEITE_UPDATE.md` (Sektion 4.4) geplant:
- `LocalBusiness` Schema mit Stuttgart-Adresse, Telefon, Geo-Koordinaten (Mark füllt Daten ein)
- `FAQPage` Schema mit allen 6 FAQ-Items (1:1 aus `LandingFaq.astro`)
- Inline in `index.astro` (nicht in `LandingLayout`, da andere Pages das Layout teilen)

Phase 1B startet erst NACH Re-Design + Browser-Approval.
