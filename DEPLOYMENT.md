# ZeugnisWerk Schweiz

Technische Vorschau für einen Schweizer Arbeitszeugnis-Entwurfsgenerator.

## Status
**NICHT PRODUKTIONSREIF.** Zahlungen und Formulardatenübermittlung sind absichtlich deaktiviert. Keine API-Schlüssel in Git einchecken.

## Architektur für den späteren Livebetrieb
- Stripe Checkout serverseitig, Checkout-Sitzung und Bestellung persistent zuordnen
- Stripe Webhook: Rohdaten mit Stripe-Signatur und Zeitfenster verifizieren, Ereignisse deduplizieren
- Postgres: Auftragszustand, idempotente Verarbeitung und minimale Zahlungsbelege
- OpenAI: Schweizer Arbeitszeugnis als geprüfter HTML-Entwurf
- Isolierter HTML-zu-PDF-Renderer ohne Netzwerkzugriff für fremde Inhalte
- Resend: Versand mit wiederholbaren, idempotenten Zustellversuchen
- Fehler: begrenzte Wiederholungen, Refund nur einmal, Information an Kunden
- Daten: kurze Aufbewahrung, Bereinigung von Job-Logs und temporären Dateien; Backup-Fristen gesondert dokumentieren

## Vor Echtgeldbetrieb erforderlich
1. Sicherheitsreview und Integrationstests inkl. manipuliertem Webhook und doppelten Events
2. Ausfallsichere Speicherung, Retry-/Refund-State-Machine und Tests für Crash-Szenarien
3. DSG-Datenschutzinformation, Impressum, Auftragsbearbeitungsverträge und Aufbewahrungskonzept
4. API-Keys als Render Secrets hinterlegen; keine leeren Secrets als scheinbar fertige Konfiguration
5. Zahlung erst nach erfolgreichem End-to-End-Test freischalten
