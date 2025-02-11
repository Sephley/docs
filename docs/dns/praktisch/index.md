# Aufgaben
- [x] = fertig
- [ ] = WIP

Checkliste der Aufträge gemäss Olat:

- [x] *Als Pflichtprogramm wird die Inbetriebnahme eines DNS-Resolvers und Nameservers erwartet (bind unter Linux).*
    * [x] *In Wireshark zeichnen Sie die rekursive Abfrage auf und erklären diese.*
    * [x] *Erstellen Sie einen Secondary DNS und lassen Sie die Zonen automatisiert synchronisieren.*
    * [ ] *In einem früheren Auftrag haben Sie exotische Betriebssysteme ans Netzwerk angebunden. Binden Sie Ihren DNS-Resolver ein und zeigen Sie per Wireshark, ob diese Betriebssysteme die Abfragen korrekt durchführen.*
    * [ ] *Versuchen Sie dynamisch DNS-Einträge anpassen zu lassen. Spielen Sie Kapitel 3 von https://strugglers.net/~andy/blog/2018/03/19/ nach. Beachten Sie, dass sich die Welt ändert: Nutzen Sie tsig-keygen statt dnssec-keygen.*
    * [ ] *Unter maas.bbw-it.ch haben Sie Zugriff auf eine «persönliche» DNS-Subdomain. Nutzen Sie diese Möglichkeit und testen Sie, wie sie diese einsetzen können. Für Fortgeschrittene können Sie auch die dynamische Anpassung ausprobieren.*
    * [x] *Übersteuern Sie den DNS mittels Hosts-File (auch unter Windows). Wie verhält sich der Resolver, wenn Sie ihm per Hosts-File andere Werte unterjubeln? Werden diese da berücksichtigt?*

### Netzwerkschema
Ich übernehme das Netzwerk vom letzten Auftrag zu PXE und DHCP. Einerseits weil es praktisch ist, andererseits weil es eine gute Übung für mich ist.
![Netzwerkschema](drawio/netzwerkschama_m300_dns.drawio)