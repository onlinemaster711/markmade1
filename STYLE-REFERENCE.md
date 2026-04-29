# MarkMade Cream-Look — Style Reference

> ## ⚠️ Geltungsbereich
>
> Diese Reference gilt **ausschließlich** für den **Cream-Look** der markmade.de-Webpräsenz. Aktuell nutzen drei Seiten dieses System:
>
> - `/` (Startseite)
> - `/ki-steuerberater`
> - `/ki-automatisierung-workflow`
>
> Alle anderen ~33 Seiten der Webseite (Branchenseiten wie ki-aerzte, ki-handwerker, ki-kanzlei; Service-Seiten wie ki-telefonassistent, ki-email, ki-social-media; Webdesign-Seiten; Ratgeber-Seiten; Legal-Seiten) verwenden den **Original-Look** über `BaseLayout` + `src/styles/global.css`.
>
> Der Original-Look hat ein eigenes Farbsystem (Material-Style-Tokens wie `--surface`, `--primary`, `--secondary`, `--on-surface`) das NICHT in dieser Reference dokumentiert ist. Wer eine Original-Look-Seite bearbeitet oder neu baut, schaut in `src/styles/global.css` direkt nach.
>
> **Aktueller Stand (April 2026):** Beide Systeme bleiben parallel im Einsatz. Eine Migration ist nicht beschlossen.

---

Single source of truth für alle Cream-Look-Landingpages (analog zu `src/pages/index.astro` und `src/pages/ki-steuerberater.astro`). Wer eine neue Branchenseite baut, soll diese Datei lesen statt in `landing.css` zu graben.

**Scope:** Cream-Look v2 Design. Lebt in `src/styles/landing.css` und wird ausschließlich von `src/layouts/LandingLayout.astro` geladen. `global.css` und alle Subpages via `BaseLayout` sind davon NICHT betroffen.

**Goldene Regel:** Keine neuen CSS-Klassen erfinden. Keine Anpassungen an `landing.css` oder Landing*-Komponenten. Wenn eine Sektion nicht passt, weil deine Inhalte zu lang sind: Inhalte kürzen, nicht CSS biegen.

---

## 1. Tokens (CSS Custom Properties)

Aus `:root` in `landing.css`. Keine Schatten- oder Radius-Tokens — Schatten/Radien werden komponenten-lokal gesetzt.

### Farben — Surfaces (Hintergründe)

| Variable | Wert | Verwendung |
|---|---|---|
| `--cream` | `#F5F1EA` | body-Background, Hero-Sektion, Principle, Topstrip |
| `--cream-2` | `#EFEAE0` | Sektions-Wechsel: `.steps`, `.faq`. Hover für `.menu a` (history). |
| `--cream-3` | `#E7E1D4` | Footer-Hintergrund |

### Farben — Ink (Text)

| Variable | Wert | Verwendung |
|---|---|---|
| `--ink` | `#1A1814` | Body-Default, Headlines, `.kicker .num`, `.stat .num`, `.faq-q .qtxt`, `.foot .col h4` |
| `--ink-2` | `#3A352D` | Sekundärtext: `.hero-sub`, `.step .body p`, `.foot .col a`, `.cta-grid p`, alle Body-Paragraphen |
| `--muted` | `#6E665A` | Eyebrows, Labels, Captions: `.kicker`, `.stat .lbl`, `.foot .col h4`, `.cta-meta`, `.foot-bottom` |

### Farben — Lines

| Variable | Wert | Verwendung |
|---|---|---|
| `--rule` | `#D9D2C2` | subtile Hairlines: `.topstrip` border, `.hero-stats` borders, `.stat` border-right, `.principle .ledger` borders, `.faq` borders, `footer` border-top |
| `--rule-2` | `#C7BFAC` | stärkere Hairlines: `.hero-meta hr`, `.hero-sub hr`, `.steps-list` border-top, `.step` border-bottom, `.faq-list` border-top, `.faq-item` border-bottom, `.btn-ghost` border |

### Farben — Brand-Akzente

| Variable | Wert | Verwendung |
|---|---|---|
| `--bordeaux` | `#A8174D` | Brand-Primärakzent: `.btn` background, `.brand .made`, `.brand .dot`, `.live .dot`, `.hero-h1 .em`, `.kicker .rule`, italic-em-Pattern, `.faq-q:hover .qtxt`, `::selection` |
| `--bordeaux-deep` | `#7E0F39` | Hover-Variante: `.btn:hover` background, manuelle hover für italic-Akzente |
| `--sage` | `#D4DDB8` | **NUR** `.cta-card` background |
| `--olive` | `#9C9678` | Italic-Numerale: `.step .index`, `.ledger .step-num` (FAQ-Numerale wurden auf `--bordeaux` umgestellt für bessere Sichtbarkeit) |

### Schriften

| Variable | Wert | Verwendung |
|---|---|---|
| `--serif` | `"Roboto Slab", Georgia, serif` | alle Headlines, `.brand`, `.stat .num`, `.kicker .num`, `.ledger .step-text`, `.faq-q .qtxt` |
| `--serif-italic` | `"Instrument Serif", Georgia, serif` | italic-Akzente: `.hero-h1 .em`, `.hero-sub p`, `.step .index`, `.ledger .step-num`, `.faq-q .qnum` (italic + bordeaux), alle inline-em-Pattern |
| `--sans` | `"Inter", system-ui, -apple-system, "Segoe UI", Helvetica, Arial, sans-serif` | body Default, alle Body-Paragraphen, UI (Buttons, Footer-Links, Eyebrows) |

Schriften werden via `@import` in `landing.css` von Google Fonts geladen — Subpages ziehen sie nicht.

### Layout-Tokens

| Variable | Wert | Verwendung |
|---|---|---|
| `--max` | `1280px` | Container-max-width für `.container`, `.nav-inner`, `.topstrip-inner`, `.hero-grid`, `.foot`, `.foot-bottom` |
| `--gutter` | `clamp(20px, 4vw, 56px)` | horizontaler Padding für `.container`, alle Sektionen, `.nav-inner`, `.topstrip-inner` |
| `--section-pad` | `clamp(72px, 10vw, 160px)` | vertikaler Padding für `section.zone` |

---

## 2. Typografie

Alle Headline- und Body-Klassen mit konkreten Werten und Beispiel-Inhalten aus `index.astro`. Klassen ohne `.foo {}`-Selektor sind kontextabhängige Descendant-Selektoren (z.B. `.step .body h3`).

### Display + Headline

| Klasse | Family | font-size | line-height | letter-spacing | weight | Wofür | Beispiel (index.astro) |
|---|---|---|---|---|---|---|---|
| `.hero-h1` | `--serif` | `clamp(40px, 6vw, 96px)` | `0.92` | `-0.035em` | `700` | Display-Headline (Hero only) — von urspr. `clamp(64px, 12vw, 188px)` zweimal reduziert (zwischenzeitlich `clamp(48px, 8vw, 124px)`), um Hero-Wirkung ruhiger und Schrift-Hierarchie ausgewogen zu halten | „KI macht dich besser." |
| `.hero-h1 .em` | `--serif-italic` | inherit | inherit | `-0.01em` | `400 italic`, color `--bordeaux` | italic-Bordeaux-Akzent in Hero | „besser." |
| `.zone-h2` | `--serif` | `clamp(36px, 5.4vw, 64px)` | `1.04` | `-0.025em` | `700`, color `--ink` | Section-Headline (zone-Sektionen) | „Dein Kunde bekommt sofort eine Antwort. Du wirst nicht unterbrochen." |
| `.principle h2` | `--serif` | `clamp(36px, 5.5vw, 64px)` | `1.05` | `-0.025em` | `700` | Section-Headline in Principle (h2 ohne Klasse, via Cascade) | „Keine Software. Kein Abo. Keine Überraschungen." |
| `.cta-grid h2` | `--serif` | `clamp(40px, 6vw, 80px)` | `1` | `-0.025em` | `700`, max-width `14ch` | CTA-Card-Headline (h2 ohne Klasse, via Cascade) | „Zeig uns deine Prozesse." |

### Subheading + Body in Sektionen

| Klasse | Family | font-size | line-height | letter-spacing | weight | Wofür | Beispiel |
|---|---|---|---|---|---|---|---|
| `.hero-sub p` | `--serif-italic` | `clamp(20px, 2.4vw, 26px)` | `1.3` | (default) | `400 italic`, color `--ink-2` | Hero-Subline | „Eine Person mit KI schlägt ein Team ohne." |
| `.step .body h3` | `--serif` | `clamp(22px, 2.4vw, 30px)` | `1.2` | `-0.015em` | `700`, max-width `24ch` | Titel je Step-Zeile | „Dein Kunde bekommt seinen Termin bestätigt — innerhalb von Minuten." |
| `.step .body p` | inherits `--sans` | `15.5px` | inherit (1.55) | (default) | `400`, color `--ink-2`, max-width `50ch` | Beschreibung je Step-Zeile | „Egal ob er um 9 Uhr morgens fragt oder um 23 Uhr abends." |
| `.faq-q .qtxt` | `--serif` | `clamp(20px, 2.1vw, 26px)` | `1.25` | `-0.015em` | `600`, color `--ink` | FAQ-Frage | „Was kann man alles mit KI bearbeiten?" |
| `.faq-a-inner p` | inherits `--sans` | `15.5px` | inherit (1.55) | (default) | `400`, color `--ink-2`, max-width `62ch` | FAQ-Antwort | „Telefon. E-Mails. Angebote. …" |
| `.faq-head .lead` | inherits `--sans` | `15px` | inherit | (default) | `400`, color `--ink-2`, max-width `42ch` | Lead-Text neben FAQ-Headline | „Sechs Fragen, die wir … hören." |
| `.cta-grid p` | inherits `--sans` | `17px` | inherit | (default) | `400`, color `--ink-2`, max-width `46ch` | CTA-Body-Text | „10 Minuten Gespräch. Wir zeigen dir welche Prozesse …" |
| `.ledger .step-text` | `--serif` | `18px` | (default) | `-0.01em` | `500` | Ledger-Stichwort je Zelle | „Du sagst uns wie du arbeitest." |

### Numerale, Eyebrows, Stat-Bar

| Klasse | Family | font-size | line-height | letter-spacing | weight | Wofür | Beispiel |
|---|---|---|---|---|---|---|---|
| `.kicker` | `--sans` | `13px` | (inherit) | `0.14em` | (inherit), uppercase, color `--muted` | Sektions-Eyebrow | „02 Was KI heute schon macht" |
| `.kicker .num` | `--serif` | `14px` | inherit | `0` | `600`, color `--ink` | Numeral im Kicker | „02" |
| `.kicker .rule` | — | (1px height, 36px width, color `--bordeaux`) | — | — | — | Bordeaux-Strich vor Kicker | (visuell) |
| `.stat .num` | `--serif` | `clamp(28px, 3vw, 40px)` | `1` | `-0.02em` | `700`, color `--ink` | Stat-Wert | „24" / „8" / „< 5" / „1×" |
| `.stat .num .unit` | inherit | `0.55em` (relativ) | inherit | `0` | `500`, color `--muted` | Unit-Suffix nach Stat-Wert | „/ 7" / „statt 40" / „Min." / „bezahlt" |
| `.stat .lbl` | inherit `--sans` | `13px` | inherit | `0.14em` | `400`, uppercase, color `--muted` | Stat-Label | „Erreichbarkeit" / „Mails am Tag" |
| `.step .index` | `--serif-italic` | `clamp(48px, 6vw, 72px)` | `1` | `-0.01em` | `400 italic`, color `--olive` | Step-Numeral (links in Zeile) | „01" / „02" / „03" |
| `.step:hover .index` | — | inherit | inherit | inherit | color `--bordeaux` (transition) | Hover-Color der Step-Numerale | — |
| `.step .meta` | inherit `--sans` | `13px` | inherit | `0.14em` | `400`, uppercase, color `--muted` | rechte Meta-Spalte (label + bold value) | „Reaktionszeit / < 5 Min." |
| `.step .meta b` | inherit | `13px` | inherit | inherit | `600`, color `--ink` | bolder Wert in `.step .meta` | „< 5 Min." |
| `.ledger .step-num` | `--serif-italic` | `14px` | (default) | (default) | `400 italic`, color `--olive` | Numeral in Ledger-Zelle | „i." / „ii." / „iii." |
| `.faq-q .qnum` | `--serif-italic` | `20px` | (default) | (default) | `400 italic`, color `--bordeaux` | Numeral vor FAQ-Frage — sichtbarer visueller Anker | „01" |

### Buttons

| Klasse | Padding | Font | Background | Color | Hover | Wofür |
|---|---|---|---|---|---|---|
| `.btn` | `11px 18px`, border-radius `999px` | `14px / 500` | `--bordeaux` | `#fff` | `--bordeaux-deep`, `translateY(-1px)` | Primary CTA |
| `.btn-lg` | `16px 26px` (override) | `15px` | (inherits btn) | (inherits btn) | (inherits btn) | Größere CTA-Variante |
| `.btn-ghost` | (inherits btn) | (inherits btn) | `transparent` | `--ink`, border `1px solid --rule-2` | bg `--cream-2`, border `--ink` | Sekundäre CTA |

### Footer-Spezifika

| Klasse | font-size | letter-spacing | weight | color | max-width |
|---|---|---|---|---|---|
| `.foot .col h4` | `11px` | `0.18em` uppercase | `600` | `--muted` | — |
| `.foot .col a` | `14px` | (default) | (default) | `--ink-2`, hover `--bordeaux` | — |
| `.foot .about p` | `13px` | (default) | (default) | `--ink-2`, line-height `1.55` | `24ch` |
| `.foot-bottom` | `12px` | (default) | (default) | `--muted` | — |

### Klassen die NICHT existieren (häufige Annahmen)

- `.body`, `.body p` als standalone Klassen — gibt es nicht. `.step .body p` ist Descendant-Selektor.
- `.lede` — gibt es nicht. Lead-Text ist `.faq-head .lead` (kontextual).
- `.step-link` — JS-Marker-Klasse, **kein** CSS. Wird vom IntersectionObserver via `data-step` adressiert; Style läuft über `.steps-aside ol li.active`.

---

## 3. Sektions-Patterns

Alle wiederkehrenden Sektionsmuster auf `index.astro`, mit empirisch ermittelten Wort-Limits aus den existierenden Inhalten.

### Pattern 1 — Hero mit Stat-Bar

**Komponente:** `LandingHero.astro`
**Sinn:** Display-Headline mit Italic-Bordeaux-Punchline, dezente italic-Subline zwischen zwei Hairlines, primary CTA, vier Stat-Kacheln als Beweis.

**HTML-Skeleton:**
```html
<section class="hero">
  <div class="hero-grid">
    <div class="hero-meta reveal"><hr><span class="tag"><span class="pin"></span>Eyebrow</span><hr></div>
    <h1 class="hero-h1 reveal">Headline. <span class="em">Italic-Akzent.</span></h1>
    <div class="hero-sub reveal"><hr><p>Italic-Subline.</p><hr></div>
    <div class="hero-cta reveal">
      <a class="btn btn-lg" href="#cta">Primary CTA <span class="arrow">→</span></a>
      <a class="btn btn-ghost btn-lg" href="#waski">Sekundär</a>
    </div>
    <div class="hero-stats reveal">
      <div class="stat"><div class="num">24<span class="unit">/ 7</span></div><div class="lbl">Label</div></div>
      <!-- … 4 Stats total auf Desktop, sonst entstehen leere Grid-Zellen -->
    </div>
  </div>
</section>
```

**Inhalts-Limits (empirisch, aus index.astro):**
- `.hero-h1`: 4 Wörter (z.B. „KI macht dich besser.") — bei mehr Wörtern aggressives Wrapping. Italic-Akzent meist 1-2 Wörter.
- `.hero-sub p`: ~8 Wörter, ein Satz, max-width 780px.
- `.hero-cta`: 1-2 Buttons, primary + ghost.
- `.stat .num`: 1 Token (Zahl/Symbol), `.unit` 1-2 Tokens, `.lbl` 1-3 Wörter uppercase.
- **Anzahl Stats: GENAU 4** (Grid ist `repeat(4,1fr)`). Bei 3 Stats bleibt eine Zelle leer und sichtbar.

**⚠️ EINSCHRÄNKUNG — Wortlänge:**

`.hero-h1` skaliert mit `clamp(48px, 8vw, 124px)`. Auf großen Viewports rendert Roboto Slab Bold breit — sehr lange Einzelwörter können den Viewport sprengen.

**Faustregel:** Kein Einzelwort in der Hero-Headline länger als **~13 Glyphen**.

| Status | Beispiel | Max-Glyphen |
|---|---|---|
| ✅ funktioniert | „KI macht dich besser." | 6 |
| ✅ funktioniert | „KI für Steuerberater." | 13 |
| ⚠️ knapp | „Standardaufgaben" | 15 |
| ❌ bricht | „Mandantenanfragen" | 17 |
| ❌ bricht | „Verwaltungsaufgaben" | 19 |

Bei langen Branchen-Bezeichnungen oder Compound-Wörtern: entweder Headline anders formulieren oder das lange Wort in die Subline verschieben (`.hero-sub p` ist deutlich kleiner und verträgt 13+ Glyphen problemlos).

*(Die Faustregel galt bei der ursprünglichen `clamp(64px, 12vw, 188px)`-Größe als ~10 Glyphen. Mit der reduzierten Hero-Größe verträgt das Pattern jetzt ~13 Glyphen sicher.)*

### Pattern 2 — Sticky-Sidebar mit Steps

**Komponente:** `LandingWasKiMacht.astro`
**Sinn:** Vertikale Liste konkreter Szenen/Schritte. Linke Sidebar trackt aktiven Step beim Scrollen via IntersectionObserver. Drei Zeilen passen rhythmisch in den editorial-Look.

**HTML-Skeleton:**
```html
<section class="zone steps" id="anchor">
  <div class="container">
    <div class="steps-head reveal">
      <div class="kicker"><span class="rule"></span><span class="num">02</span><span>Eyebrow</span></div>
      <h2 class="zone-h2">Headline. <em style="font-family:var(--serif-italic); font-weight:400; color:var(--bordeaux);">Italic-Punchline.</em></h2>
    </div>
    <div class="steps-grid">
      <aside class="steps-aside reveal">
        <span class="label">Sidebar-Label</span>
        <ol>
          <li class="step-link active" data-step="1">Kurz</li>
          <li class="step-link" data-step="2">Kurz</li>
          <li class="step-link" data-step="3">Kurz</li>
        </ol>
      </aside>
      <div class="steps-list">
        <article class="step reveal" data-step="1">
          <div class="index">01</div>
          <div class="body"><h3>Titel des Schritts.</h3><p>Beschreibung.</p></div>
          <div class="meta"><span>Label</span><b>Wert</b></div>
        </article>
        <!-- weitere .step articles -->
      </div>
    </div>
  </div>
</section>
```

**Inhalts-Limits (empirisch):**
- `.zone-h2` (Headline): ~10 Wörter, mehrzeilig durch `max-width:14ch`. Italic-Punchline am Ende = 2-4 Wörter.
- `.steps-aside li`: 2-4 Wörter pro Eintrag (z.B. „Termin in Minuten").
- `.step .body h3`: **10-15 Wörter, möglichst ein Satz**. Über 15 → wirkt überladen.
- `.step .body p`: **8-13 Wörter**, ein knapper Satz. Über 15 → quetscht den `auto`-meta-Slot.
- `.step .meta`: **1 Label-Wort + 1-2 Wert-Tokens** (z.B. „Reaktionszeit / < 5 Min."). Über 2 Wörter im `<b>` → Layout-Risiko.
- **Anzahl Steps: 3** auf der Startseite. Mehr ist möglich, aber rhythmisch wirken 3-4 am stärksten.
- **JS-Voraussetzung:** Steps-Active-Observer im Page-Script (siehe Abschnitt 8) — ohne ihn bleibt die Sidebar statisch auf Step 1.

### Pattern 3 — Principle-Ledger

**Komponente:** `Principle.astro`
**Sinn:** Drei kurze Stichworte/Manifest-Sätze in horizontaler 3-Spalten-Bilanz. Sehr knapp gehalten — keine Beschreibungen.

**HTML-Skeleton:**
```html
<section class="zone principle">
  <div class="container">
    <div class="reveal" style="display:flex; justify-content:center">
      <div class="kicker"><span class="rule"></span><span class="num">03</span><span>Eyebrow</span></div>
    </div>
    <h2 class="reveal">Headline. <em style="font-family:var(--serif-italic); font-weight:400; color:var(--bordeaux);">Italic-Punchline.</em></h2>
    <div class="ledger reveal">
      <div><span class="step-num">i.</span><span class="step-text">Stichwort 1.</span></div>
      <div><span class="step-num">ii.</span><span class="step-text">Stichwort 2.</span></div>
      <div><span class="step-num">iii.</span><span class="step-text">Stichwort 3.</span></div>
    </div>
  </div>
</section>
```

**Inhalts-Limits (empirisch):**
- `.principle h2`: ~6 Wörter, max-width `18ch`, zentriert. Italic-Punchline = 2-4 Wörter.
- `.ledger .step-num`: römische Ziffer, 1-3 Zeichen.
- `.ledger .step-text`: **5-9 Wörter pro Zelle**. Spaltenbreite ist `max-width:880px / 3 = ~290px`, abzüglich `padding:32px 24px` → ~242px effektive Textbreite. Mehr → Zeilenumbruch in 1-2-Wort-Zeilen, kollabiertes Layout.
- **Anzahl Zellen: GENAU 3** (Grid `repeat(3, 1fr)`).
- Wenn du Beschreibungen brauchst, ist das **das falsche Pattern** — nimm Pattern 2 (Steps).

### Pattern 4 — FAQ-Accordion

**Komponente:** `LandingFaq.astro`
**Sinn:** Klassisches Akkordeon mit Plus/Minus-Icon. Erstes Item öffnet automatisch beim Page-Load. Bordeaux-Hover auf der Frage.

**HTML-Skeleton:**
```html
<section class="zone faq">
  <div class="container">
    <div class="faq-head reveal">
      <div>
        <div class="kicker"><span class="rule"></span><span class="num">04</span><span>Häufige Fragen</span></div>
        <h2 class="zone-h2">Häufige Fragen</h2>
      </div>
      <p class="lead">Lead-Text neben der Headline.</p>
    </div>
    <div class="faq-list">
      <div class="faq-item reveal">
        <button class="faq-q" aria-expanded="false">
          <span class="qnum">01</span>
          <span class="qtxt">Frage?</span>
          <span class="icon" aria-hidden="true"></span>
        </button>
        <div class="faq-a"><div><div class="faq-a-inner"><p>Antwort-Absatz.</p></div></div></div>
      </div>
      <!-- weitere faq-items -->
    </div>
  </div>
</section>
```

**Inhalts-Limits (empirisch):**
- `.faq-head .lead`: ~16 Wörter, ein-zwei Sätze, max-width `42ch`.
- `.faq-q .qtxt`: **5-10 Wörter**, ein Satz mit Fragezeichen.
- `.faq-a-inner p`: **30-50 Wörter pro Antwort**, max-width `62ch`. Mehrere Sätze möglich.
- **Anzahl Items: 6** auf der Startseite. Flexibel — 4-8 funktionieren editorial.
- **JS-Voraussetzung:** FAQ-Accordion-Toggle (siehe Abschnitt 8).

### Pattern 5 — CTA-Card

**Komponente:** `LandingCta.astro`
**Sinn:** Großer Sage-grüner Block mit zentrierter Headline, kurzer Erklärung, ein primary + optional ein ghost CTA. Soll am Ende der Page als „Final-Cliff" wirken.

**HTML-Skeleton:**
```html
<section class="cta-zone" id="cta">
  <div class="cta-card reveal">
    <div class="cta-grid">
      <div class="kicker"><span class="rule"></span><span class="num">05</span><span>Dein nächster Schritt</span></div>
      <h2>Headline. <em style="font-family:var(--serif-italic); font-weight:400; color:var(--bordeaux);">Italic.</em></h2>
      <p>Untertext, ein-zwei Sätze.</p>
      <div class="actions">
        <a class="btn btn-lg" href={CALENDLY} target="_blank" rel="noopener noreferrer">Primary CTA <span class="arrow">→</span></a>
        <a class="btn btn-ghost btn-lg" href="#" style="background:rgba(255,255,255,.4)">Sekundär</a>
      </div>
    </div>
    <div class="cta-meta">
      <span>— KOSTENLOS · UNVERBINDLICH</span>
      <span>10 MIN.</span>
    </div>
  </div>
</section>
```

**Inhalts-Limits (empirisch):**
- `.cta-grid h2`: 4-6 Wörter, max-width `14ch` zentriert. Italic = 1-3 Wörter.
- `.cta-grid p`: **10-15 Wörter**, max-width `46ch`.
- `.actions`: 1-2 Buttons.
- `.cta-meta`: 2 sehr kurze Spans (uppercase Mikrotext) absolut positioniert am unteren Card-Rand.

---

## 4. Farben in der Anwendung

### Cream-Layer-Wechsel
Sektionen alternieren zwischen Cream-Tönen für visuellen Rhythmus:
- **`--cream`** = Default (body), Hero, Principle, CTA-Zone
- **`--cream-2`** = `.zone.steps`, `.zone.faq` — gibt diesen Sektionen einen leicht dunkleren Hintergrund mit Hairlines top/bottom
- **`--cream-3`** = `footer` (dunkelster Cream, Abschluss)

Der Wechsel ist der einzige Background-Indikator für „neue Sektion" — keine Kästen, keine Cards (außer CTA).

### Ink-Hierarchie für Text
- **`--ink`** für alles, was beim Scrollen zuerst gesehen wird: Headlines, Numerale (`.kicker .num`), Stat-Werte, FAQ-Fragen
- **`--ink-2`** für Lese-Text: Body-Paragraphen, Footer-Links, FAQ-Antworten, Sub-Headlines
- **`--muted`** für Mikrotext: Eyebrows, Labels, Stat-Units, Footer-Headings, Foot-Bottom

### Bordeaux — sparsam und gezielt
Bordeaux ist das einzige Brand-Signal. Nie für ganze Sätze, nie als Hintergrundfläche (außer Buttons). Konkret:
- Italic-Akzent in Headlines (1-3 Wörter via `.em` oder inline-em)
- Primary-Button (`.btn`) Hintergrund
- 36px-Strich vor dem Kicker (`.kicker .rule`)
- Live-Dot im Topstrip (legacy, aktuell nicht eingebunden)
- Logo-Akzent: „made" in mark**made** und der `.brand .dot`
- `.faq-q:hover .qtxt`-Hover-Color
- `::selection`-Highlight

`--bordeaux-deep` ausschließlich für `.btn:hover`.

### Olive — Italic-Numerale
`--olive` (#9C9678) wird für italic-Numerale verwendet, NICHT für Hintergrundflächen:
- `.step .index` (große italic Step-Nummer)
- `.ledger .step-num` (kleine italic römische Ziffer)

Bei `.step:hover` wechselt `.index` von Olive zu Bordeaux. `.faq-q .qnum` wurde aus dieser Gruppe herausgenommen und auf `--bordeaux` umgestellt — die FAQ-Nummer war als visueller Anker zu unscheinbar in Olive.

### Sage — exklusiv für CTA
`--sage` (#D4DDB8) wird **nur** für `.cta-card` verwendet. Nicht in andere Sektionen kopieren — Sage ist das visuelle Signal „Ende der Story, jetzt handeln".

### Rules
- `--rule` (zarter): `.topstrip` border, `.hero-stats` borders, `.principle .ledger` borders, `.faq` borders, `footer` border-top
- `--rule-2` (kräftiger): `.hero-meta hr`, `.hero-sub hr`, `.steps-list` border-top, `.step` border-bottom, `.faq-list` border-top, `.faq-item` border-bottom, `.btn-ghost` border

---

## 5. Layout & Container

### Globale Tokens
```css
--max:         1280px;
--gutter:      clamp(20px, 4vw, 56px);
--section-pad: clamp(72px, 10vw, 160px);
```

### Per-Sektion Max-Widths
| Element | max-width | Gibt's wo |
|---|---|---|
| `.container`, `.nav-inner`, `.topstrip-inner`, `.hero-grid`, `.foot`, `.foot-bottom` | `1280px` (`--max`) | global |
| `.hero-sub` | `780px` | Hero-Subline |
| `.principle .ledger` | `880px` | Principle Bilanz |
| `.cta-card` | `1080px` | CTA |
| `.zone-h2` | `14ch` | sub-Hero Headlines |
| `.principle h2` | `18ch` | Principle-Headline |
| `.cta-grid h2` | `14ch` | CTA-Headline |
| `.step .body h3` | `24ch` | Step-Titel |
| `.step .body p` | `50ch` | Step-Beschreibung |
| `.cta-grid p` | `46ch` | CTA-Body |
| `.faq-head .lead` | `42ch` | FAQ-Lead |
| `.faq-a-inner p` | `62ch` | FAQ-Antwort |
| `.foot .about p` | `24ch` | Footer-About |

### Vertikale Sektion-Paddings
| Sektion | top | bottom |
|---|---|---|
| `.hero` | `clamp(80px, 12vw, 160px)` | `clamp(60px, 8vw, 120px)` |
| `section.zone` | `var(--section-pad)` = `clamp(72px, 10vw, 160px)` | (gleicher Wert) |
| `.cta-zone` | `clamp(60px, 8vw, 120px)` | (gleicher Wert) |
| `footer` | `clamp(56px, 7vw, 96px)` | `32px` |

### Wichtige Grids
| Element | grid-template-columns | Mobile-Override |
|---|---|---|
| `.nav-inner` | `auto auto` (`justify-content: space-between`) | `auto auto` (gap 16px) bei <960px |
| `.hero-stats` | `repeat(4, 1fr)` | `repeat(2, 1fr)` <960px → `1fr` <520px |
| `.hero-meta` | `minmax(120px,1fr) auto minmax(120px,1fr)` | `1fr` <520px (hr ausgeblendet) |
| `.hero-sub` | `1fr auto 1fr` | `1fr` <520px (hr ausgeblendet) |
| `.steps-grid` | `220px 1fr` | `1fr` <960px (sidebar wird zur Reihe) |
| `.step` | `120px 1fr auto` | `80px 1fr` <960px (meta wandert auf eigene Reihe) |
| `.principle .ledger` | `repeat(3, 1fr)` | `1fr` <960px (border-right → border-bottom) |
| `.faq-q`, `.faq-a-inner` | `56px 1fr 32px` | `32px 1fr 24px` <960px |
| `.faq-head` | `1fr 1fr` | `1fr` <960px |
| `.cta-grid` | `1fr` (immer einspaltig, Inhalt zentriert) | — |
| `.foot` | `1.4fr repeat(4, 1fr)` | `1fr 1fr` <960px → `1fr` <760px |
| `.foot-bottom` | `1fr auto 1fr` | `1fr` <960px |

---

## 6. Komponenten zum Wiederverwenden

Jede Cream-Look-Seite bindet diese Komponenten direkt ein. Pfade aus Sicht von `src/pages/<deine-seite>.astro`:

| Komponente | Import-Pfad | Pflicht? | Kommentar |
|---|---|---|---|
| `LandingLayout` | `../layouts/LandingLayout.astro` | ja | Setzt `<head>` (SEO, Schema-LD), lädt `landing.css`, rendert `Chatbot` und `CookieBanner` automatisch |
| `Nav` | `../components/Nav.astro` | ja | Sticky-Nav mit Logo + CTA-Button. Scrollt mit. |
| `LandingFooter` | `../components/LandingFooter.astro` | ja | 5-Spalten-Footer, auf Mobile Akkordeon |
| `ChatbotTooltip` | `../components/ChatbotTooltip.astro` | ja | Cream-Notification + 8s-Tooltip. Der eigentliche Chatbot wird von LandingLayout via `Chatbot.astro` geladen. |

**NICHT direkt importieren** — das macht LandingLayout für dich:
- `Chatbot.astro` (im Body via Layout)
- `CookieBanner.astro` (im Body via Layout)

**Nicht für Subpages-Welt zweckentfremden** — Header.astro, Footer.astro, Hero.astro, Cta.astro, Faq.astro etc. ohne `Landing`-Präfix gehören zur v1-Welt (`global.css`/`BaseLayout.astro`) und brechen das Cream-Look-Design, wenn du sie hier einbindest. Siehe `DESIGN.md` Abschnitt 0.

---

## 7. Italic-Bordeaux-Pattern

Zwei Varianten, je nach Kontext.

### Variante A — In `.hero-h1` (mit Klasse `.em`)

CSS-Regel ist Teil von landing.css, daher reicht die Klasse:

```html
<h1 class="hero-h1 reveal">
  KI macht<br>
  dich <span class="em">besser.</span>
</h1>
```

`.hero-h1 .em` setzt:
```css
font-family: var(--serif-italic);
font-style: italic;
font-weight: 400;
color: var(--bordeaux);
letter-spacing: -0.01em;
```

### Variante B — In `.zone-h2`, `.principle h2`, `.cta-grid h2` (Inline-em)

Es gibt keine universelle `.em`-Klasse außerhalb von `.hero-h1`. Verwende ein `<em>`-Element mit Inline-Style:

```html
<h2 class="zone-h2">
  Du machst Beratung.
  <em style="font-family:var(--serif-italic); font-weight:400; color:var(--bordeaux);">
    Nicht Sortierarbeit.
  </em>
</h2>
```

Die Inline-Werte greifen ausschließlich auf existierende CSS-Variablen zurück — keine Magic-Numbers.

### Don'ts

- Nie ganze Sätze italic-bordeaux setzen — der Akzent verliert seine Wirkung. **1-3 Wörter** am Ende der Headline ist die Norm.
- Nie `font-size` im inline-em setzen — übernimmt sich automatisch von der Headline.
- Nie auf Body-Paragraphen anwenden (außer der speziellen Closer-Pattern wie in „Der ehrliche Teil" auf ki-steuerberater.astro: italic-bordeaux Schlusssatz mit eigenem `font-size:clamp(20px, 2.4vw, 26px)`).

---

## 8. Animation & Reveal

### `.reveal` — Fade-Up beim Scrollen

Klasse hängt initial bei `opacity:0; transform:translateY(14px)`. Wenn das Element ins Viewport kommt, fügt das Page-Script `.in` hinzu, was Opacity 1 und transform reset transitioniert (0.7s ease).

```css
.reveal{opacity:0; transform:translateY(14px); transition:opacity .7s ease, transform .7s ease}
.reveal.in{opacity:1; transform:none}
```

### Pflicht-Page-Script

Jede Page muss diese drei Observer am Ende einbinden (in einem `<script>`-Block, NICHT `is:inline` — Astro bundelt das ins Page-JS):

```js
// 1. Reveal-on-scroll für ALLE .reveal-Elemente
const io = new IntersectionObserver((entries) => {
  entries.forEach(e => {
    if (e.isIntersecting) {
      e.target.classList.add('in');
      io.unobserve(e.target);
    }
  });
}, { threshold: 0.12, rootMargin: '0px 0px -40px 0px' });
document.querySelectorAll('.reveal').forEach(el => io.observe(el));

// 2. Steps-Active-Sidebar (NUR wenn Pattern 2 verwendet wird)
const stepsObs = new IntersectionObserver((entries) => {
  entries.forEach(e => {
    if (e.isIntersecting) {
      const target = e.target as HTMLElement;
      const id = target.dataset.step;
      if (!id) return;
      document.querySelectorAll<HTMLElement>('.step-link').forEach(l => {
        l.classList.toggle('active', l.dataset.step === id);
      });
    }
  });
}, { threshold: 0.5 });
document.querySelectorAll('.step[data-step]').forEach(s => stepsObs.observe(s));

// 3. FAQ-Accordion (NUR wenn FAQ-Pattern verwendet wird; LandingFaq.astro hat das bereits selbst)
document.querySelectorAll('.faq-item').forEach(item => {
  const btn = item.querySelector('.faq-q');
  btn?.addEventListener('click', () => {
    const open = item.classList.toggle('open');
    btn.setAttribute('aria-expanded', String(open));
  });
});
document.querySelector('.faq-item')?.classList.add('open');
document.querySelector('.faq-item .faq-q')?.setAttribute('aria-expanded', 'true');
```

**Wichtig:** Wenn du `<LandingFaq />` als Komponente einbindest, hat sie ihren Accordion-Code schon dabei — Block 3 NICHT doppeln. Wenn du FAQ-Markup inline schreibst (wie ki-steuerberater.astro), brauchst du Block 3.

### Zusätzliche Animationen aus landing.css

- **`.hero::before`** Radial-Gradient (Bordeaux-Schimmer am Hero-Boden) — passiv, kein JS.
- **`@keyframes pulse`** für `.live .dot` — Topstrip-Indikator, aktuell ungenutzt.
- **`@keyframes scroll`** für `.marquee-track` — Topstrip-Marquee, aktuell ungenutzt.
- **`.faq-a` Grid-Rows-Transition** (`grid-template-rows: 0fr → 1fr`) — Akkordeon-Smooth-Open, rein CSS.
- **`.step:hover .index`** Olive → Bordeaux — passiv hover, kein JS.
- **`.col-collapsible[open] > summary::after`** Plus → Minus — native `<details>`, kein JS.

---

## 9. Mobile-Verhalten

Drei Breakpoints in `landing.css`:

### `@media (max-width: 960px)` — Tablet & große Phone
- `.nav-inner`: gap 32px → 16px
- `.topstrip-inner .marquee`: hidden
- `.hero-stats`: 4-col → 2-col, erste 2 Stats bekommen `border-bottom`, 2. Stat verliert `border-right`
- `.steps-grid`: 220px+1fr → 1fr (sidebar von sticky-vertikal zu inline-horizontal)
- `.steps-aside`: `position:sticky` → `position:static`; `flex-direction:column` → `row` mit `flex-wrap`
- `.steps-aside ol li.active`-Highlight wird **neutralisiert** (alle Items sehen identisch aus, sonst springt der Text beim Scrollen)
- `.step`: `120px 1fr auto` → `80px 1fr`; `.step .meta` springt auf `grid-column: 1 / -1` (eigene Reihe unter dem Body)
- `.principle .ledger`: 3-col → 1-col, border-rights werden border-bottoms
- `.faq-head`: 2-col → 1-col, `.lead` linksbündig
- `.faq-q`, `.faq-a-inner`: gap reduziert, Numeral-Spalte schmaler
- `.foot`: 5-col → 2-col

### `@media (max-width: 760px)` — Footer-spezifisch
- `.foot`: 2-col → 1-col, gap 0
- `.foot .col.about`: bottom-margin + border-bottom
- `.col-collapsible`: Akkordeon-Verhalten aktiviert (Plus/Minus Toggle, Listen versteckt bis [open])
- ChatbotTooltip-Texte wechseln auf Kurzform (siehe ChatbotTooltip.astro)

### `@media (max-width: 520px)` — Phone
- `.hero-meta`: 1-col, `<hr>` ausgeblendet
- `.hero-sub`: 1-col, `<hr>` ausgeblendet
- `.hero-stats`: 1-col stack
- `.foot`: 1-col

### Empirische Regel
Wenn dein Design auf Desktop sauber aussieht, sind die Mobile-Overrides in `landing.css` so geschickt, dass es auf Mobile auch passt. **NICHT versuchen, auf Mobile umzubauen** — wenn etwas auf Mobile nicht passt, liegt das fast immer am Inhalt (zu lang, zu komplex), nicht am CSS.

---

## 10. Beispiel: Eine neue Seite bauen

Minimal-Skelett für eine neue Cream-Look-Branchenseite. Copy-paste, dann Inhalte einfüllen:

```astro
---
import LandingLayout from '../layouts/LandingLayout.astro';
import Nav from '../components/Nav.astro';
import LandingFooter from '../components/LandingFooter.astro';
import ChatbotTooltip from '../components/ChatbotTooltip.astro';

const CALENDLY = 'https://calendly.com/onlinemaster711/new-meeting';
---

<LandingLayout
  title="Branche-Headline | MarkMade"
  description="SEO-Description, 150-160 Zeichen."
>
  <Nav />

  <!-- HERO -->
  <section class="hero">
    <div class="hero-grid">
      <div class="hero-meta reveal">
        <hr><span class="tag"><span class="pin"></span>KI für Branche · DACH</span><hr>
      </div>
      <h1 class="hero-h1 reveal">
        Headline. <span class="em">Punchline.</span>
      </h1>
      <div class="hero-sub reveal">
        <hr><p>Italic-Subline.</p><hr>
      </div>
      <div class="hero-cta reveal">
        <a class="btn btn-lg" href={CALENDLY} target="_blank" rel="noopener noreferrer">Kostenloses Erstgespräch buchen <span class="arrow">→</span></a>
      </div>
      <!-- Optional: <div class="hero-stats reveal">...4 .stat...</div> -->
    </div>
  </section>

  <!-- Weitere Sektionen — siehe Pattern 2-5 in Abschnitt 3 -->

  <LandingFooter />
  <ChatbotTooltip />
</LandingLayout>

<script>
  // Reveal + Steps + FAQ Observer (siehe Abschnitt 8)
  const io = new IntersectionObserver((entries) => {
    entries.forEach(e => {
      if (e.isIntersecting) { e.target.classList.add('in'); io.unobserve(e.target); }
    });
  }, { threshold: 0.12, rootMargin: '0px 0px -40px 0px' });
  document.querySelectorAll('.reveal').forEach(el => io.observe(el));
</script>
```

LandingLayout setzt automatisch:
- `<title>` + `<meta description>` aus deinen Props
- Canonical-URL = `https://www.markmade.de` + Astro.url.pathname
- Viewport, Charset, Robots, Author
- Open Graph (Title/Description aus Props, Bild + URL hardcoded auf homepage)
- Twitter Card
- Drei JSON-LD Schema-Blocks (ProfessionalService, WebSite, WebPage)
- Lädt `landing.css`
- Bindet `<CookieBanner />` und `<Chatbot />` ein

**Bekannte Limitation:** OG-URL und WebPage-Schema-URL in LandingLayout zeigen hardcoded auf `https://www.markmade.de/`. Auf Subseiten technisch leicht ungenau, aber kein Crawl-Problem (Canonical überschreibt).

---

## 11. Lessons Learned aus ki-steuerberater.astro

### Patterns vs. Inhalts-Realität

| Pattern | Was es verträgt (gemessen) | Was kollabiert |
|---|---|---|
| `.principle .ledger` Zelle | 5-9 Wörter Stichwort | 25-30 Wörter → 1-2-Wort-Zeilen, kollabierte Spalten |
| `.step .body h3` | 10-15 Wörter, 1 Satz | 4 Sätze nacheinander |
| `.step .body p` | 8-13 Wörter, 1 knapper Satz | 25-30 Wörter → quetscht den `auto`-meta-Slot, sichtbare Überlappung |
| `.step .meta` | 1 Wort label + 1-2 Wert-Tokens | 3+ Wörter im `<b>` |
| `.zone-h2` lang | wrappt durch `max-width:14ch` editorial in mehrere Zeilen | wirkt wie Hero-Größe statt sub-Hero (perception) |

### Konkrete Fehler bei der ersten ki-steuerberater.astro-Version

1. **Sektion 05 „Drei Module" Modul-Beschreibungen ~30 Wörter pro `.ledger > div`** — gefixt durch radikale Kürzung auf 7-9 Wörter.
2. **Sektion 03 „Drei Szenen" Szenen-Bodies 25-30 Wörter** — gefixt durch Kürzung auf 10-15 Wörter pro `.step .body p`.
3. **Hero-Stats mit `<span class="unit">` für die 2. Hälfte des Vergleichs** — ergab visuell „großes Vorher / kleines Nachher" statt gleichwertiger Vergleich. Gefixt: ganze Vergleichswerte in `.num` ohne `.unit`.
4. **Rechnung-Tabelle: Label als h3, Vergleichswert als p** — Label dominierte den Wert. Gefixt: getauscht (Vergleich = h3, Label = p).
5. **Module-Body-Text 14px** — sub-body, wirkte „zu klein". Gefixt: font-size aus inline-style entfernt → erbt 16px Body-Default.

### 5 Faustregeln für künftige Seiten

1. **Pattern bestimmt Wortlänge, nicht andersrum.** Wenn die Startseite an einer Stelle 6 Wörter nutzt, schreibe 6-9. Nicht 30. Nicht 60. Wenn dein Inhalt mehr braucht, ist es das falsche Pattern — wechsle das Pattern (oder kürze konsequent).
2. **Steps-Pattern für mittlere Sätze, Ledger-Pattern für Stichworte, FAQ-Pattern für Absätze.** Niemals umgekehrt.
3. **`.step .meta` ist ein **Stempel**, kein Untertitel.** „Reduktion / −98 %" passt. „Differenz beim Vergleich pro Mandant pro Monat / signifikant" passt nicht.
4. **Italic-Bordeaux ist Punkt, nicht Strich.** 1-3 Wörter. Nie ein ganzer Satz, nie als Überschrift.
5. **Wenn etwas auf Mobile bricht, ist der Text zu lang** — nicht das CSS schuld. Die Mobile-Overrides in `landing.css` sind vom Original-HTML-Entwurf so abgestimmt, dass sie mit kurzen, knappen Inhalten exzellent funktionieren. Kürzen, nicht patchen.
6. **Hero-Wortlänge prüfen:** Kein Wort in `.hero-h1` länger als ~13 Glyphen. Sehr lange Compound-Wörter im Deutschen („Mandantenanfragen", „Verwaltungsaufgaben") sprengen das Pattern auf großen Viewports. Wenn solch ein Wort unverzichtbar ist: in die Subline verschieben.
7. **Eyebrows, Labels und Mikrotext nicht unter 13px.** Lesbarkeit vor Editorial-Eleganz. Das Sprung-Verhältnis zwischen Headlines und Kleintext sollte gemäßigt bleiben — sonst „schreit" die Hero und „flüstert" alles andere. `.kicker`, `.stat .lbl`, `.step .meta` haben deshalb 13px Mindestgröße; `.steps-aside` 14px. Begleitend: letter-spacing bei kleinem Uppercase nicht über `0.14em`, sonst wirkt Text zu gespreizt.

---

*Letzte Aktualisierung: April 2026. Wenn `landing.css` oder eine Landing*-Komponente sich ändert, dieses Dokument auch.*
