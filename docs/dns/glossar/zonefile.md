# Zonendatei
- [x] *Erklären Sie die Zonendatei inkl. allen Parametern im SOA.*

Die Zonendatei enthält die gesamte Hierarchie der Zone inklusive allen Records. Eine Zonendatei startet immer mit einem SOA record, wo alle wichtigen Infos zur Zone stehen (z.B. Kontakt zum Zonenadmin).

Hier sind die Parameter eines SOA-Eintrags und deren Bedeutung:

#### Primary Name Server (MNAME)
Dies ist der vollqualifizierte Domainname (FQDN) des primären Nameservers für die Zone. Er ist der erste Server, der autoritative Antworten für die Zone liefert.

#### Responsible Person (RNAME)
Dies ist die E-Mail-Adresse der Person, die für die Verwaltung der Zone verantwortlich ist. Das "@"-Zeichen wird durch einen Punkt (".") ersetzt. Zum Beispiel, "admin.example.com" bedeutet "admin@example.com".

#### Serial Number
Eine fortlaufende Nummer, die bei jeder Änderung der Zonendatei erhöht wird. Dies hilft sekundären Nameservern zu erkennen, wann die Zonendatei aktualisiert wurde, sodass sie ihre Kopien entsprechend aktualisieren können.

#### Refresh Interval
Die Zeit in Sekunden, nach der sekundäre Nameserver überprüfen sollen, ob die Zonendatei auf dem primären Nameserver aktualisiert wurde. Typischerweise ein Wert zwischen 1 Stunde (3600 Sekunden) und 1 Tag (86400 Sekunden).

#### Retry Interval
Die Zeit in Sekunden, die sekundäre Nameserver warten sollen, bevor sie nach einem fehlgeschlagenen Update-Versuch erneut versuchen, die Zonendatei zu aktualisieren. Dieser Wert ist normalerweise kürzer als das Refresh-Intervall.

#### Expire Time
Die maximale Zeit in Sekunden, die ein sekundärer Nameserver die Zonendatei als gültig betrachten soll, wenn keine Aktualisierung vom primären Server erfolgt. Nach dieser Zeit wird die Zonendatei als ungültig betrachtet, und der Server stellt die Beantwortung von Anfragen für diese Zone ein. Typischerweise ein Wert von mehreren Wochen.

#### Minimum TTL (Time To Live)
Die Standardzeit in Sekunden, die DNS-Einträge aus dieser Zone im Cache eines Clients oder eines zwischengeschalteten Nameservers verbleiben sollen. Wenn kein spezifischer TTL-Wert für einen Eintrag festgelegt ist, wird dieser Wert verwendet.