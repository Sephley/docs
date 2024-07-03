# Let's Encrypt Zertifikate

<https://letsencrypt.org/>

## Über Let's Encrypt

Let’s Encrypt ist eine freie, automatisierte und offene Zertifizierungsstelle (CA) und läuft für die Öffentlichkeit. Der Dienst wird zur Verfügung gestellt von Internet Security Research Group (ISRG).

Die Schlüsselprinzipien hinter Let’s Encrypt sind:

- Frei: Jeder, der einen Domainnamen besitzt, kann Let’s Encrypt benutzen, um sichere Zertifikate kostenfrei zu erhalten.
- Automatisch: Die Software die auf dem Webserver läuft, kann auf einfache Website mit Let’s Encrypt Zertifikate beziehen, zur Benutzung abgesichert werden und automatisch Zertifikate erneuern.
- Sicher: Let’s Encrypt stellt eine Plattform für erweiterte TLS-Sicherheit zur Verfügung, sowohl auf der CA-Seite als auch beim Betreiber, um ihn bei der Absicherung seines Servers zu unterstützen.
- Transparent: Alle ausgestellten und widerrufenen Zertifikate werden öffentlich für jedermann zur Inspektion zur Verfügung gestellt.
- Offen: Das automatische Ausstellungs- und Erneuerungsprotokoll wird als offener Standard veröffentlicht, damit es andere adaptieren können.
- Kooperativ: Ähnlich wie die zugrundeliegenden Internetprotokolle selbst ist Let’s Encrypt eine gemeinsame Anstrengung, die der Community zugute kommt und außerhalb der Kontrolle einer einzelnen Organisation liegt.

## Funktionilität von Let's Encrypt

<https://letsencrypt.org/getting-started/>

Um ein Zertifikat bei Let's Encrypt zu generieren muss man auf folgende URL zugreifen können: `https://acme-v02.api.letsencrypt.org/directory`

Diese URL ist das ACME Directory. Es dient als Entrypoint für ACME-Clients, um die verfügbaren Endpoints für die Interaktion mit der CA zu ermitteln. Das Directory ist ein JSON-Objekt, das eine Reihe von URLs für verschiedene vom ACME-Server bereitgestellte Dienste enthält.

Es gibt [sehr viele Wege](<https://letsencrypt.org/docs/client-options/>), um ein Let's Encrypt Zertifikat auszustellen.