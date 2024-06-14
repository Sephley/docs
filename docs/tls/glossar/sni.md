# SNI
- [x] *Lange bestand das Problem, dass pro HTTPS-Subdomain eine eigene IP-Adresse nötig war. Warum und wie löste man das? Wie funktioniert SNI?*

## Problem
In den frühen Versionen des SSL/TLS-Protokolls wird die Anfrage des Clients an den Server ohne Hostinformationen gesendet.
Das bedeutet, dass der Server nicht weiss, für welche Subdomain oder welchen Hostname die Anfrage bestimmt ist, da die Hostinformationen erst in der HTTP-Anfrage enthalten sind, die nach dem SSL/TLS-Handshake kommt.
Ohne diese Information konnte der Server nicht das richtige Zertifikat auswählen, wenn mehrere Subdomains auf derselben IP-Adresse gehostet wurden.

## Lösung
Um dieses Problem zu lösen haben die Entwickler des "EdelKey project" SNI (Server Name Indication) als Erweiterung von TLS 2003 ins Leben gerufen.  
Ich finde die Erklärung von [Cloudflare](https://www.cloudflare.com/en-gb/learning/ssl/what-is-sni/) sehr verständlich: *SNI is somewhat like mailing a package to an apartment building instead of to a house. When mailing something to someone's house, the street address alone is enough to get the package to the right person. But when a package goes to an apartment building, it needs the apartment number in addition to the street address; otherwise, the package might not go to the right person or might not be delivered at all.*

Technisch wird der Hostname in der ersten Nachricht des SSL/TLS-Handshakes gesendet. Dies erlabut es dem Server, das richtige Zertifikat für die angeforderte Subdomain auszuwählen.