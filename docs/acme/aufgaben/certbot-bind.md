# Certbot mit Bind9 in Betrieb nehmen
Im Geschäft stellen wir unsere Wildcard Zertifikate manuell aus, denn es sei zu riskant ist dies zu automatisieren.

Das ist natürlich blödsinn, denn ein funktionierender Automatismus macht keine Fehler und ist gar weniger riskant als wenn man es manuell macht.
## Bind DNS für Letsencrypt aufsetzen
Wir setzen Bind9 als DNS ein, also müssen wir diesen umkonfigurieren. Hierfür verwende ich die [Anleitung aus Olat](https://www.hagen-bauer.de/2019/06/authoritive-bind-server.html).

## Installation