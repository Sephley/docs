# Architektur des Protokolls
- [ ] *Verschaffen Sie sich einen Überblick über die Architektur des Protokolls.*

<https://www.cloudflare.com/learning/ssl/transport-layer-security-tls/>

TLS (Transport Layer Security) besteht aus mehreren Schichten und Protokollen.

## Record Protocol
Sorgt für die Vertraulichkeit und Integrität der übertragenen Daten. Es zerteilt die Daten in Blöcke, komprimiert sie optional, berechnet Authentifizierungscodes und verschlüsselt sie, bevor sie über das Netzwerk gesendet werden.
## Handshake Protocol & Change Cipher Spec Protocol
Ermöglicht die Authentifizierung der Kommunikationspartner und die Aushandlung kryptographischer Parameter. Das Change Cipher Spec Protocol signalisiert den Übergang von unverschlüsselter zu verschlüsselter Kommunikation.  
<https://www.cloudflare.com/learning/ssl/what-happens-in-a-tls-handshake/>

![handshake](../images/tls-ssl-handshake.png)  
[*Bild von Cloudflare*](https://cf-assets.www.cloudflare.com/slt3lc6tev37/5aYOr5erfyNBq20X5djTco/3c859532c91f25d961b2884bf521c1eb/tls-ssl-handshake.png)

## Alert Protocol
Übermittelt Fehlermeldungen und Warnungen. Mittels einem "Close Notify" Alert sieht man, dass eine Partei die Verbindung sauber schliessen möchte.