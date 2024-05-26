# Wireshark
- [x] *In Wireshark zeichnen Sie die rekursive Abfrage auf und erklären diese.*
- [ ] *In einem früheren Auftrag haben Sie exotische Betriebssysteme ans Netzwerk angebunden. Binden Sie Ihren DNS-Resolver ein und zeigen Sie per Wireshark, ob diese Betriebssysteme die Abfragen korrekt durchführen.*

Ich habe meinen ehemaligen DHCP Client verwendet, wo Wireshark schon installiert war.
## Windows
Ich habe einen Scan gestartet und nach `dns` gefiltert. Während dem Scan habe ich Microsoft Edge geöffnet und olat.bbw.ch aufgelöst.

![wireshark_4](images/wireshark_4.png)
[Datei herunterladen](../downloadable/sephley_lookup.pcapng)

1. Start bei dem Resolver:  
Der Client sendet eine DNS-Abfrage an den DNS-Resolver.  

2. DNS Server erhaltet die Anfrage:  
Der Resolver fragt einen der Root-Nameserver an.

3. Weiterleitung an die TLD-Nameserver:  
Der Root-Nameserver antwortet mit einem Verweis auf die TLD-Nameserver, die für die Domäne zuständig sind.

4. Anfrage an die autoritativen Nameserver:
Der TLD-Nameserver antwortet mit den autoritativen Nameservern für primary.sephley.local. Der Resolver schickt dann eine Anfrage an einen dieser autoritativen Nameserver.

5. Erhalt der endgültigen Antwort:  
Der autoritative Nameserver (primary.sephley.local) antwortet mit der IP-Adresse der Domäne. Diese Antwort wird an den Resolver zurückgegeben.

6. Übermittlung an den Client:  
Der Resolver sendet die erhaltene IP-Adresse an den ursprünglichen Client zurück, der die Anfrage gestellt hat.

7. Caching der Antwort:  
Sowohl der Resolver als auch der Client speichern die Antwort im Cache, um bei zukünftigen Anfragen schneller antworten zu können.

## Probleme / Anmerkungen
Ich habe irgendwie den Sinn der Aufgabe nicht begriffen und habe die rekursive Anfrage an olat.bbw.ch gemacht. Aber der Sinn und Zweck dieser Aufgabe ist ja, dass ich die Anfrage an meinen eigenen DNS mache...  
Dazu habe ich zuerst eine bereits gecachte Abfrage auf www.google.ch gemacht, was natürlich nichts nützt, wenn man den ganzen Prozess erklären möchte.

![wireshark_1](images/wireshark_1.png)  
[Datei herunterladen](../downloadable/windows_dns.pcapng)

Falls Sie sich fragen, was gstatic.com ist: Google lädt static content (Javascripts, Bilder, CSS) von einer anderen Domäne. Dies hilft bei der Ladezeit, da es die Bandbreite verringert.  
![wireshark_2](images/wireshark_2.png)
