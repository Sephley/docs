# DHCP Vogel
[Auftrag](https://olat.bbw.ch/auth/1%3A1%3A32068123854%3A3%3A0%3Aserv%3Ax%3A_csrf%3A03007576-d952-4001-add7-05c93a6fbd08/DHCP%20PXE/DHCP-Auftrag.pdf)  
[Präsi](https://olat.bbw.ch/auth/1%3A1%3A32068123854%3A3%3A0%3Aserv%3Ax%3A_csrf%3A03007576-d952-4001-add7-05c93a6fbd08/DHCP%20PXE/DHCP-praesi.pdf)
## Umgebung
- VMware Workstation Pro
    - 2x Ubuntu Server (Ohne GUI) - einer für den ISC und einer als relay agent
    - Windows Client

### Netzwerkplan
![plan](drawio/plan.drawio)

## Installation
#### 1. APT Packet installieren

```
sudo apt update
sudo apt install isc-dhcp-server
```

#### 2. Konfiguration

Um unseren frisch installierten DHCP server zu konfigurieren, müssen wir das File `/etc/dhcp/dhcpd.conf` bearbeiten.  
Folgende Konfiguration habe ich verwendet:

```
subnet 192.168.1.0 netmask 255.255.255.192 {
    range 192.168.1.5 192.168.1.60;
    option routers 192.168.1.1;
    option domain-name-servers 1.1.1.1, 9.9.9.9;
}
```

Danach identifizieren wir unser Netzwerkinterface mittels `ip a` und tragen es bei `/etc/default/isc-dhcp-server` ein.
```
INTERFACESv4="ens33"
```
Nun können wir unseren DHCP server eine statische IP geben: `/etc/netplan/00-installer-config.yaml`  
Ich habe die bereits vorhandene Version wie folgt überschrieben.

```
network:
  version: 2
  ethernets:
    ens33:
      dhcp4: no
      addresses:
        - 192.168.1.2/26
      routes:
        - to: default
          via: 192.168.1.1
      nameservers:
        addresses: [1.1.1.1, 9.9.9.9]
```
Danach folgenden Befehl auführen: `sudo netplan apply`

#### 3. Dienst neustarten

```
sudo systemctl restart isc-dhcp-server.service
```

## DHCP Relay
Um diesen Dienst zu verwenden benötigt man ein DHCP Relay Agent.  
Der Agent wird benötigt um clients von einem separaten Netzwerk mit dem DHCP Server zu verbinden.

## Zusätzliche Probleme

## Quellen
- Offizielle Installation `isc-dhcp-server` von Canonical  
[https://ubuntu.com/server/docs/how-to-install-and-configure-isc-dhcp-server](https://ubuntu.com/server/docs/how-to-install-and-configure-isc-dhcp-server)
- Setup Blog `isc-dhcp-relay ` von Reintech  
[https://reintech.io/blog/configure-dhcp-relay-agent-ubuntu-2004](https://reintech.io/blog/configure-dhcp-relay-agent-ubuntu-2004)
