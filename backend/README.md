# Backend – noch nicht produktionsreif

Dieses Backend ist ein erster Entwicklungsstand, nicht für Echtgeld-Zahlungen freigegeben. Die Vorschau-Landingpage bleibt absichtlich deaktiviert.

## Bereits implementiert
- Stripe Checkout Session serverseitig
- Stripe Webhook mit Signaturprüfung auf dem Roh-Body
- PostgreSQL-Bestellungen und grundlegende Deduplizierung
- OpenAI HTML-Erzeugung, Gotenberg PDF, Resend E-Mail
- begrenzte Wiederholungen und Refund-Versuch
- Löschen von Nutzdaten nach erfolgreichem Versand aus der Bestelltabelle

## Kritische offene Punkte
- Refund-Queue läuft derzeit nur, wenn ein neuer Job bearbeitet wird; muss separat verarbeitet werden.
- Zustellung nach Prozessabsturz kann doppelt erfolgen; Outbox und Zustell-Idempotenz nötig.
- Nach Neustart können processing-Jobs hängen bleiben; Lease-Recovery erforderlich.
- Formulardatenvalidierung und Abuse-/Rate-Limits härten.
- Vollständige DSG-Löschung inklusive Log-, Backup- und Provider-Aufbewahrung ist nicht garantiert.
- Checkout-Webseite ist noch nicht mit Backend verbunden.
- Fehler- und Zahlungsszenarien mit echten Sandbox-Diensten testen.
- Gotenberg und Datenbank bereitstellen; Geheimnisse nur über Render-Umgebung.

**Nicht live schalten, bevor diese Punkte behoben sind.**
