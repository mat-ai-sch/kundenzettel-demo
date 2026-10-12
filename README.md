# Kundenzettel-Demo

Dieses öffentliche Repository veröffentlicht ausschließlich die geprüften statischen Browserdateien aus `site/` unter https://demo.kundenzettel.de/. `site/release.json` benennt den zugehörigen Commit des privaten Quellrepositories Moinwerk/Kundenzettel, Branch `feat/kundenzettel-ui-kit-demo`.

Die Demo zeigt fiktive Gesprächs- und Auftragsdaten. Lokale Testnachrichten bleiben im Browser; der Build enthält keinen Worker, keine API-Zugangsdaten und führt keine OpenAI- oder WhatsApp-Anfragen aus. Die geschützte Betreiber-App und API bleiben auf Cloudflare.

## Aktualisierung

Im privaten Quellrepository die Vorschau bauen und prüfen. `scripts/github-pages/prepare-demo.py` bereitet die Browserdateien, Rechtsseiten, Lizenzhinweise und die Veröffentlichungskennung vor. Danach den geprüften Inhalt von `site/` in diesem Repository aktualisieren und nach `main` pushen.

Der Workflow `.github/workflows/pages.yml` prüft die Dateihashes, veröffentlicht `site/` über GitHub Pages und prüft beide HTTPS-Adressen auf den passenden Quellstand. Ein manueller Workflowstart veröffentlicht dieselben bereits eingecheckten Dateien. Änderungen an der Hauptwebsite lösen keine Demo-Aktualisierung aus.

`https://www.demo.kundenzettel.de/` ist als Alias der kanonischen Demo-Adresse vorgesehen. Beide DNS-Einträge zeigen auf GitHub Pages. Der Workflow protokolliert die echte TLS-Verbindung beider Adressen und prüft, dass der Alias zur kanonischen Adresse weiterleitet. Eine Cloudflare-Weiterleitung ist im privaten Quellrepository als Alternative vorbereitet, aber nicht aktiviert.

Bei einem fehlenden Zertifikat für den www-Alias kann ein Administrator die Domain in Settings → Pages entfernen und sofort wieder als `demo.kundenzettel.de` speichern; anschließend HTTPS erneut aktivieren. Die automatisierte Alternative mit `renew_certificate:true` benötigt zuvor das Repository-Secret `PAGES_ADMIN_TOKEN` mit Pages: write und Administration: write für genau dieses Repository. Ohne diesen zusätzlichen Token nimmt der Workflow keine Domainänderung vor. Normale Veröffentlichungen benötigen diesen Token nicht. Nach erfolgreicher Dateiprüfung entfernt er ausschließlich die erwartete Custom Domain und stellt sie sofort wieder her, um die Ausstellung gemäß GitHub-Dokumentation neu anzufordern. Die Domain kann dabei kurzzeitig nicht erreichbar sein. Normale Pushes erneuern das Zertifikat nicht. Erst die abschließende unabhängige TLS-Prüfung bestätigt die Live-Veröffentlichung beider Adressen; danach wird HTTPS erneut erzwungen.

## Wechsel von der bisherigen Offline-Demo

Die frühere Demo konnte ihre alte Oberfläche aus einem bereits installierten Workbox-Cache anzeigen, obwohl auf dem Server neue Dateien lagen. `site/sw.js` löst diesen alten Offline-Worker ab. Für den sofortigen Wechsel gibt es https://demo.kundenzettel.de/_v/update.html; dieser Pfad umgeht den früheren Dokument-Cache, meldet nur die Root-Registrierung dieser Demo ab und öffnet den aktuellen Stand. Lokale Browserdaten werden nicht gelöscht. Der private Quellstand enthält einen Browser-Regressionstest für bereits besuchte und frische Profile auf Desktop und Mobil.

## Archiv: alte GitLab-Oberfläche

https://demo.kundenzettel.de/alt/ öffnet parallel die bisherige Oberfläche. Sie wurde aus dem übernommenen Website-Commit `326b0ebb52e59833ff23becd63cd248eb9fd8745` gebaut, auf den auch der vorherige Demo-Workflow zugriff. `site/alt/archive.json` dokumentiert diesen Ursprung. Der Build nutzt `VITE_PUBLIC_SURFACE=whatsapp`, `VITE_RUNTIME_MODE=preview` und den Asset-Basispfad `/alt/`. Nur Asset-Pfade, eigene Speicherkennungen und die Entfernung der Offline-Registrierung wurden für die parallele Vorschau angepasst; das alte Design bleibt erhalten. Die aktuelle Oberfläche an der Startadresse bleibt unverändert.

Bei künftigen Veröffentlichungen `site/alt/` als unabhängiges Archiv erhalten und seine Dateien erneut in die Hashliste von `site/release.json` aufnehmen. Keine alten Root-Dateien oder Root-Service-Worker zurückspielen.

## Informationen: Q&A-Board

Der aktuelle Stand enthält unter `#/informationen` zwölf redaktionell geprüfte Fragen, Beispielfragen und ein Fragefeld, das vorhandene Antworten im Browser findet. Geplante Module stehen getrennt darunter. Fragen werden weder gespeichert noch an externe Anbieter gesendet. Die Businessansicht bündelt Fragen in vier Themencluster und begrenzt die Inhaltsbreite auf 1120 px. Desktop nutzt zwei unabhängige Scrollflächen und ein kompaktes Fragepanel. Mobil beginnen die häufigen Fragen; Fragefeld und Modulausblick folgen in derselben Lesefläche. Die Desktop-Zeile „Dein Arbeitsplatz“ entfällt, die mobile Kopfzeile bleibt erhalten.
