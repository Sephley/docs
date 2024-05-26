# DynDNS
- [x] *DynDNS hat einige spannende Probleme zu entdecken: Wie ist das mit den Timeouts? Wie lösen die das mit den vielen Anfragen? Wie ist DynDNS eigentlich entstanden?*

DynDNS (Dynamic Domain Name System) ist ein Dienst, der es ermöglicht, eine ständig wechselnde IP-Adresse, wie sie bei vielen Internet Service Providern (ISPs) für Privatkunden üblich ist, mit einem festen Domainnamen zu verknüpfen.
#### Handling von Timeouts

- Update-Intervalle: Die Client-Software sendet regelmäßig Updates, um sicherzustellen, dass die DNS-Einträge aktuell sind. Dies kann in festgelegten Intervallen (z.B. alle 5 Minuten) oder bei Erkennung einer IP-Änderung geschehen.
- TTL (Time To Live): DNS-Einträge haben eine TTL, die bestimmt, wie lange ein DNS-Eintrag gecached werden darf. DynDNS setzt oft eine relativ kurze TTL (z.B. 300 Sekunden), um sicherzustellen, dass Änderungen schnell wirksam werden.

#### Handling von Anfragen

- Lastverteilung (Load Balancing): DynDNS-Dienste nutzen Lastverteilung, um eingehende Anfragen auf mehrere Server zu verteilen, was die Last auf einzelne Server reduziert.
- Caching: DNS-Server und ISPs cachen DNS-Einträge für die Dauer der TTL, was die Anzahl der Anfragen an den DynDNS-Dienst reduziert.
- Rate Limiting: Einige Dienste implementieren Rate Limiting, um die Anzahl der Updates von einzelnen Clients zu begrenzen und Missbrauch zu verhindern.

## Beispiel
DynDNS (DDNS) ist sehr nützlich, wenn mon von seinem ISP keine Statische Public IP erhält, aber trotzdem Dienste in einem lokalen Netzwerk veröffentlichen möchte.
In unserer geteilten Umgebung (Wyler, Oberle, Chio, Hurley) verwenden wir den DynDNS von Swisscom.  
![swiss_ddns](images/swiss_ddns.png)

So können wir mittels Cloudflare Zero Trust unsere Dienste verwalten und wenn nötig veröffentlichen.