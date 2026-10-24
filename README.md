# Kundenzettel-Demo

Öffentliche Gestaltungsvorschau mit zwei fiktiven Gesprächen. Veröffentlicht wird ausschließlich `site/` aus diesem GitHub-Repository. Keine echten Kundendaten und keine WhatsApp- oder Modellanfragen.

| Adresse | Aufgabe |
| --- | --- |
| https://demo.kundenzettel.de/ | Aktuelle Demo auf GitHub Pages |
| https://www.demo.kundenzettel.de/ | Cloudflare-Weiterleitung mit eigenem Zertifikat zur aktuellen Demo |
| https://kundenzettel.de/ | Separate Produktwebsite aus `mat-ai-sch/kundenzettel-website` |

## Veröffentlichung

Der private Quellcode liegt in `Moinwerk/Kundenzettel`, Branch `feat/kundenzettel-ui-kit-demo`. `site/release.json` enthält den geprüften Quellcommit und die Hashes der veröffentlichten Dateien. Verpackungsänderungen werden getrennt als `packagingRevision` benannt.

Der Pages-Workflow prüft die Dateien, veröffentlicht `site/` und prüft danach beide HTTPS-Adressen samt kanonischer Weiterleitung. Ein Push nach `main` oder ein manueller Workflowstart genügt. Die Zertifikatsverwaltung für `www.demo` liegt bei Cloudflare; der Workflow verändert keine Domains und benötigt keinen zusätzlichen Administrationstoken.

## Alte Browseransichten aktualisieren

https://demo.kundenzettel.de/_v/update.html löst ausschließlich die alte Root-Service-Worker-Registrierung ab und öffnet die aktuelle Demo. Lokale Browserdaten bleiben erhalten. `/sw.js` beendet den früheren Offline-Betrieb beim nächsten Browser-Update. Der Cloudflare-Weiterleitungsworker liefert diese beiden Migrationspfade gleich-originig aus.

## Historische Version

Die frühere GitLab-Oberfläche bleibt unter `archive/gitlab-demo-20261012/` im Repository erhalten. Sie gehört **nicht** zum öffentlichen Pages-Paket. Der frühere Webpfad `/alt/` öffnet die aktuelle Demo. Kein zukünftiger Release darf das Archiv erneut nach `site/` kopieren.

## Zuständigkeiten

GitHub ist die Quelle der öffentlichen Inhalte. Cloudflare verwaltet DNS, die www-Demo-Weiterleitung und den getrennten geschützten Backendbetrieb. IONOS bleibt Domainregistrar. GitLab-Pages und GitLab-CI/CD sind abgeschaltet.
