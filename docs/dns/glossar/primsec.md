# Primary / Secondary Konzept
- [x] *Recherchieren Sie über die Anfänge des Internets und setzen Sie die Primary / Secondary DNS-Infrastruktur in den Zusammenhang des redundanten dezentralen Konzepts.*

Wie Mario und Luigi, hat man Primary (master) und Secondary (slave) DNS-Server. Die Hauptaufgabe des sekundären DNS ist die Redundanz, falls der primäre ausfällt. Somit vermeidet man einen Single point of failure und man kann den Load aufteilen. Für den slave werden read-only kopien der Zonendateien eingesetzt und alle information erhaltet er direkt von dem primären DNS-Server.