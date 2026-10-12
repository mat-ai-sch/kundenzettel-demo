# Kundenzettel-Demo

Dieses öffentliche Repository veröffentlicht ausschließlich die geprüften statischen Browserdateien aus `site/` unter https://demo.kundenzettel.de/. `site/release.json` benennt den zugehörigen Commit des privaten Quellrepositories Moinwerk/Kundenzettel, Branch `feat/kundenzettel-ui-kit-demo`.

Die Demo zeigt fiktive Gesprächs- und Auftragsdaten. Lokale Testnachrichten bleiben im Browser; der Build enthält keinen Worker, keine API-Zugangsdaten und führt keine OpenAI- oder WhatsApp-Anfragen aus. Die geschützte Betreiber-App und API bleiben auf Cloudflare.

## Aktualisierung

Im privaten Quellrepository die Vorschau bauen und prüfen. `scripts/github-pages/prepare-demo.py` bereitet die Browserdateien, Rechtsseiten, Lizenzhinweise und die Veröffentlichungskennung vor. Danach den geprüften Inhalt von `site/` in diesem Repository aktualisieren und nach `main` pushen.

Der Workflow `.github/workflows/pages.yml` prüft die Dateihashes, veröffentlicht `site/` über GitHub Pages und prüft beide HTTPS-Adressen auf den passenden Quellstand. Ein manueller Workflowstart veröffentlicht dieselben bereits eingecheckten Dateien. Änderungen an der Hauptwebsite lösen keine Demo-Aktualisierung aus.

`https://www.demo.kundenzettel.de/` ist als Alias der kanonischen Demo-Adresse vorgesehen. Beide DNS-Einträge zeigen auf GitHub Pages. Der Workflow protokolliert die echte TLS-Verbindung beider Adressen und prüft, dass der Alias zur kanonischen Adresse weiterleitet. Eine Cloudflare-Weiterleitung ist im privaten Quellrepository als Alternative vorbereitet, aber nicht aktiviert.
