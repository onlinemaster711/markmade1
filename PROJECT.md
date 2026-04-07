# MarkMade – Projektstruktur

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
