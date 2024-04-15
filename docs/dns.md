# Auftrag DNS M300 Vogel
[Auftrag](https://olat.bbw.ch/auth/RepositoryEntry/635961710/CourseNode/109192337476214/path%3D~~DNS/0)  
## Vorwissen
Ich habe bereits im Geschäft einen Bind9 DNS-Server aufgesetzt. Dies ist nun schon zwei Jahre her, von dem her bin ich also doch froh kann ich dies erneut tun. Mit DynDNS habe ich auch schon in meiner privaten Infrastruktur erfahrungen gemacht.
## Theorie
Hier ist nicht nur Theorie, sondern auch Beispiele aus meinem Geschäft sowie aus der Freizeit / persönlichen Umgebung. Es kommen folgende Punkte vom Auftrag vor:    
- *Erklären Sie die Zonendatei inkl. allen Parametern im SOA.*  
- *Recherchieren Sie über die Anfänge des Internets und setzen Sie die Primary / Secondary DNS-Infrastruktur in den Zusammenhang des redundanten dezentralen Konzepts.*  
- *Recherchieren Sie verschiedene Record-Typen und erklären Sie diese.*  
- *DynDNS hat einige spannende Probleme zu entdecken: Wie ist das mit den Timeouts? Wie lösen die das mit den vielen Anfragen? Wie ist DynDNS eigentlich entstanden?*
- *Auch in der AWS oder Azure-Umgebung finden Sie DNS. Was lässt sich damit anstellen?*  
- *DNS unter IPv6 – was ändert sich?*  
- *Reverse DNS unter IPv6: https://tech.rana.at/2017/12/08/*

Damit es nochmals geschrieben steht, DNS steht bedeutet ausgeschrieben: "Domain Name System".
### Zonendatei
Die Zonendatei enthält die gesamte Hierarchie der Zone inklusive allen Records. Eine Zonendatei startet immer mit einem SOA record, wo alle wichtigen Infos zur Zone stehen (z.B. Kontakt zum Zonenadmin)
### Anfänge des Internets
Der Ursprung des DNS liegt in den frühen Tagen des Internets, als es noch ARPANET hiess und nur wenige Forscher und Institutionen miteinander vernetzt waren. Zu dieser Zeit wurden Hostnamen und ihre zugehörigen IP-Adressen in einer einzigen Datei namens "HOSTS.TXT" verwaltet, die zentral gepflegt wurde.

In den 1980er Jahren wurde das DNS-Konzept entwickelt, um diese Probleme zu lösen.

### Primary / Secondary Konzept
Wie Mario und Luigi, hat man Primary und Secondary DNS Server.

### Record-Typen
### DynDNS
DynDNS ist sehr nützlich, wenn mon von seinem ISP keine Statische Public IP erhält, aber trotzdem Dienste in einem lokalen Netzwerk veröffentlichen möchte.
### DNS in AWS
### DNS unter IPv6
### Reverse DNS unter IPv6
## Prakitische Arbeiten
Dieser Teil handelt sich um folgende Punkte von dem Auftrag:  
- *In Wireshark zeichnen Sie die rekursive Abfrage auf und erklären diese.*
- *Erstellen Sie einen Secondary DNS und lassen Sie die Zonen automatisiert synchronisieren.*
- *In einem früheren Auftrag haben Sie exotische Betriebssysteme ans Netzwerk angebunden. Binden Sie Ihren DNS-Resolver ein und zeigen Sie per Wireshark, ob diese Betriebssysteme die Abfragen korrekt durchführen.*  
- *Versuchen Sie dynamisch DNS-Einträge anpassen zu lassen. Spielen Sie Kapitel 3 von https://strugglers.net/~andy/blog/2018/03/19/ nach. Beachten Sie, dass sich die Welt ändert: Nutzen Sie tsig-keygen statt dnssec-keygen.*  
- *Unter maas.bbw-it.ch haben Sie Zugriff auf eine «persönliche» DNS-Subdomain. Nutzen Sie diese Möglichkeit und testen Sie, wie sie diese einsetzen können. Für Fortgeschrittene können Sie auch die dynamische Anpassung ausprobieren.*  
- *Übersteuern Sie den DNS mittels Hosts-File (auch unter Windows). Wie verhält sich der Resolver, wenn Sie ihm per Hosts-File andere Werte unterjubeln? Werden diese da berücksichtigt?*
### Netzwerkschema
Ich übernehme das Netzwerk vom letzen Auftrag zu PXE und DHCP. Einerseits weil es praktisch ist, anderseits war mein letztes Netzwerkschema nicht besonders gut(unnötig Pfeile + vswitch nicht aufgezeichnet). Es ist also eine gute Übung für mich.  
![Netzwerkschema](drawio/netzwerkschama_m300_dns.drawio)
### Bind9 Setup
Wie folgt habe Bind9 installiert, konfiguriert und in meine Umgebung integriert.
#### Probleme
Zuerst wollte ich den Bind9 mit Der Anleitung von Digitalocean aufsetzen, diese war jedoch overkill für meine Umgebung.
Meine lokale VMware Umgebung ist sehr langsam. Vielleicht sollte ich sie migrieren. Ich glaube ich verwende ab nun Terraform & Packer, um meine VMs zu erstellen.
### Wireshark Abfrage Analyse
### Wireshark Resolver Analyse
### Secondary DNS
### Persönliche Subdomain
### DNS übersteuren
## Quellen
### Theorie
- DNS Zone file Erklärung von Cloudflare  
[https://www.cloudflare.com/learning/dns/glossary/dns-zone/](https://www.cloudflare.com/learning/dns/glossary/dns-zone/)

### Bind9
- Bind9 DNS setup von Digitalocean  
[https://www.digitalocean.com/community/tutorials/how-to-configure-bind-as-a-private-network-dns-server-on-ubuntu-20-04](https://www.digitalocean.com/community/tutorials/how-to-configure-bind-as-a-private-network-dns-server-on-ubuntu-20-04)
- Bind9 Docs  
[https://bind9.readthedocs.io/en/latest/chapter3.html](https://bind9.readthedocs.io/en/latest/chapter3.html)
- Bind9 setup von Linuxtechi  
[https://www.linuxtechi.com/install-configure-bind-9-dns-server-ubuntu-debian/](https://www.linuxtechi.com/install-configure-bind-9-dns-server-ubuntu-debian/)