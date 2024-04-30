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
Ich habe die IP-Reservierung von dem Windows Client entfernt, damit der DNS nun diese Adresse übernehmen kann.
### Bind9 Setup
Bind9 ist eine Open-Source Implementation von DNS.  
Wie folgt habe Bind9 installiert, konfiguriert und in meine Umgebung integriert.
- LAN: 192.168.1.0/26
- DNS server: 192.168.1.7
- Client: 192.168.1.4
- Domain: sephley.local

#### 1. APT Pakete installieren
```
sudo apt update
sudo apt install bind9 bind9utils bind9-doc dnsutils
```
#### 2. Konfigration vornehmen
Die config-files für Bind9 befinden findet man unter `/etc/bind`.  
Zuerst bearbeiten wir die Datei `named.conf.options`. Hier legen wir fest
Vieles ist hier schon ausgefüllt, ich habe bloss den DNS zu dem von Cloudflare umkonfiguriert.
```
acl internal-network {
192.168.1.0/26;
};
options {
        directory "/var/cache/bind";
        allow-query { localhost; internal-network; };
        allow-transfer { localhost; };
        forwarders { 1.1.1.1; };
        recursion yes;
        dnssec-validation auto;
};
```
Als nächstes bearbeiten wir die Datei `named.conf.local`
```
zone "sephley.local" IN {
        type master;
        file "/etc/bind/forward.sephley.local";
        allow-update { none; };
};
zone "1.168.192.in-addr.arpa" IN {
        type master;
        file "/etc/bind/reverse.sephley.local";
        allow-update { none; };
};
```
Nun schreiben wir endlich unsere zone file.  
Um uns diese Arbeit zu erleichtern, kopieren wir den Inhalt von `db.local` in unsere neues zone file `forward.sephley.local`
```
cp db.local forward.sephley.local
```
Anschliessend fürgen wir folgendes in `forward.sephley.loccal` ein:
```
$TTL 604800
@ IN SOA primary.sephley.local. root.primary.sephley.local. (
         2022072651 ; Serial
         3600 ; Refresh
         1800 ; Retry
         604800 ; Expire
         604600 ) ; Negative Cache TTL
;Name Server Information
@ IN NS primary.sephley.local.

;IP address of Your Domain Name Server(DNS)
primary IN A 192.168.1.7

;A Record for Host names
www IN A 192.168.1.4

;CNAME Record
ftp IN CNAME www.sephley.local.
```

#### Probleme
Zuerst wollte ich den Bind9 mit der Anleitung von Digitalocean aufsetzen, diese war jedoch overkill für meine Umgebung.
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