# Secondary DNS
## [Dazugehörige Theorie: Primary / Secondary Konzept](dns/section/theorie/primsec.md)
Für den Secondary DNS erstellen wir nochmals eine Ubuntu-Server VM. Diesmal habe ich eine Ubuntu 24.04 (Noble Numbat) VM erstellt, denn so kann ich die neue Version testen sowie auch die Rückwärtskompatibilität prüfen.
#### 1. APT Pakete installieren
```
sudo apt update
sudo apt install bind9 bind9utils bind9-doc dnsutils
```
#### 2. Konfiguration vornehmen
Zurst müssen wir noch auf unserem primären DNS die folgenden parameter in `/etc/bind/named.conf.local` in beiden `zone` blocks einfügen:
```
allow-transfer { 192.168.1.9 };
also-notify { 192.168.1.9 };
```
`/etc/bind/named.conf.local` wie folgt bearbeiten:  
```
zone "sephley.local" {
type slave;
file "/etc/bind/forward.sephley.local";
masters { 192.168.1.7; };
};
```
Anschliessend laden wir den Dienst neu:  
```
sudo systemctl reload named
```