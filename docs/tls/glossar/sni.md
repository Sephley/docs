# SNI
- [ ] *Lange bestand das Problem, dass pro HTTPS-Subdomain eine eigene IP-Adresse nötig war. Warum und wie löste man das? Wie funktioniert SNI?*

<https://www.cloudflare.com/en-gb/learning/ssl/what-is-sni/>

## Problem
In den frühen Versionen des SSL/TLS-Protokolls wird die Anfrage des Clients an den Server ohne Hostinformationen gesendet.
Das bedeutet, dass der Server nicht weiss, für welche Subdomain oder welchen Hostname die Anfrage bestimmt ist, da die Hostinformationen erst in der HTTP-Anfrage enthalten sind, die nach dem SSL/TLS-Handshake kommt.
Ohne diese Information konnte der Server nicht das richtige Zertifikat auswählen, wenn mehrere Subdomains auf derselben IP-Adresse gehostet wurden.

## Lösung