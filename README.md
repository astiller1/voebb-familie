# VÖBB-Familie

Eine gemeinsame Übersicht für mehrere Bibliothekskonten im VÖBB (Verbund der Öffentlichen Bibliotheken
Berlins), z. B. die Ausweise der Kinder: Was ist ausgeliehen, wann muss es zurück, was kann verlängert werden?

**Status:** Konzeptphase, noch kein Code. Siehe [`docs/konzept.md`](docs/konzept.md).

## Grundsätze
- Privates Werkzeug für die eigene Familie, kein öffentlicher Dienst.
- Zugangsdaten nur in `.env` oder im Schlüsselbund, nie im Repo.
- Selten abfragen (1–2× am Tag), um voebb.de nicht zu belasten.
