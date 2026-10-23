# Konzept

## Entscheidung (23.10.2026)
VideLibri funktioniert mit beiden VÖBB-Ausweisen. Damit ist das Problem gelöst, eine eigene App wird
vorerst **nicht** entwickelt. Das Konzept unten bleibt als Plan B, falls VideLibri mit VÖBB einmal nicht
mehr funktioniert oder eine Funktion fehlt.

## Problem
Zwei Kinder, zwei VÖBB-Ausweise. Die offizielle Oberfläche (voebb.de) hat häufig Login-Probleme und zeigt
immer nur ein Konto. Ein Überblick über Rückgabefristen erfordert ständiges Hin- und Herwechseln.

## Vorab prüfen
- **VideLibri** (Open Source, F-Droid) unterstützt laut Changelog aDIS/VÖBB und mehrere Konten.
  Erst testen; vielleicht löst es das Problem schon.
- Alternativ die ältere App „Bibliothek“ (opacclient); aktueller Stand mit VÖBB unklar.

## Technische Lage
- voebb.de läuft auf **aDIS/aDISWeb** (astec). Für Kontodaten gibt es keine bekannte öffentliche API.
- Zugriff nur per Scraping: Sitzungs-Cookie holen → Login-Formular (Ausweisnummer + Passwort) →
  Seite „Ausleihen“ abrufen → Tabelle auslesen (Titel, Rückgabedatum, Verlängerungen, Bibliothek).
- Risiken: Seitenumbau bricht den Parser; dynamische, sitzungsgebundene URLs; instabiler Login
  (→ automatische Wiederholung mit Pause).
- Seit 17.07.2025 strengere Passwortregeln; dasselbe Passwort gilt auch für die Onlineangebote →
  sicher speichern.
- Eine reine Browser-Web-App kann voebb.de wegen CORS nicht direkt abfragen; dafür braucht es
  einen Server oder eine native App.

## Varianten
| Variante | Beschreibung | Pro | Contra |
|---|---|---|---|
| A | Kleiner Server (Python) + Web-App/PWA | Hintergrundabruf, Wiederholungen, Erinnerungen, alle Geräte | Passwörter auf dem Server, Rechner muss laufen |
| B | Native Android-App | Kein Server, Daten bleiben auf dem Gerät | Nur Android, mehr Aufwand |
| C | Skript → Google-Kalender | Minimal, Erinnerungen über den Kalender | Kein Verlängern per Klick |

**Vorschlag:** mit C starten, bei Bedarf zu A ausbauen.

## Funktionsideen
- Gemeinsame Liste aller Ausleihen, nach Rückgabedatum sortiert, farbig je Kind
- „Alles verlängern“ für beide Karten
- Erinnerung z. B. 3 Tage vor Ablauf (Kalender, Push oder Telegram)
- Abholbereite Vorbestellungen, offene Gebühren
- „Wo zurückgeben?“ – erst klären, ob VÖBB-Medien in jeder VÖBB-Bibliothek zurückgegeben werden können

## Offene Fragen
1. ~~Funktioniert VideLibri mit beiden Karten?~~ Ja.
2. Gibt es einen Rechner, der dauerhaft läuft (Raspberry Pi, NAS)?
3. Nutzen alle in der Familie Android?
4. Reichen Kalender-Erinnerungen, oder soll auch per Klick verlängert werden?

## Nächster Schritt
Ausleihseite eines Kontos als HTML speichern (persönliche Daten schwärzen) und unter
`samples/` ablegen. Daraus wird der Parser gebaut und getestet, ohne live auf voebb.de zuzugreifen.
