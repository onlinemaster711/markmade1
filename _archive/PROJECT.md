# MarkMade – Projektstruktur

> ## ⚠️ ARCHIVIERT (April 2026)
>
> Diese Datei beschreibt den ursprünglichen Workflow der Webseite vor dem Cream-Look-Redesign. Die Anweisungen hier — insbesondere "BaseLayout importieren" für neue Seiten — gelten nicht mehr für Cream-Look-Landingpages.
>
> **Aktuelle Quellen:**
> - Projekt-Übersicht und neue Seiten anlegen → `PROJECT_OVERVIEW.md`
> - Cream-Look-Patterns und Tokens → `STYLE-REFERENCE.md`
> - Original-Look-Tokens → `DESIGN.md` (mit Hinweis-Block)
>
> Datei archiviert, weil sie aktiv irreführend war. Inhalt zur historischen Referenz erhalten.
>
> ---

## Neue Seite hinzufügen
1. Neue Datei in src/pages/ anlegen
2. BaseLayout importieren und verwenden
3. title und description als Props übergeben
4. Seite in Footer-Navigation ergänzen
5. npm run build – fertig

## Neue Branche hinzufügen
Beispiel: /chatbot-zahnarzt
1. src/pages/chatbot-zahnarzt.astro anlegen
2. Gleiches Layout wie chatbot-handwerker.astro
3. Nur Texte und Keywords anpassen

## Deployment
git add .
git commit -m "Beschreibung der Änderung"
git push
→ Vercel deployed automatisch

## Lokale Entwicklung
npm run dev → http://localhost:4321
