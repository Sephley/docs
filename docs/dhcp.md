# DHCP Vogel
[Auftrag](https://olat.bbw.ch/auth/1%3A1%3A32044700929%3A3%3A0%3Aserv%3Ax%3A_csrf%3Ad6d20b18-d00f-4da6-8969-ce5d2b958249/DHCP%20PXE/DHCP-Auftrag.pdf)  
[Präsi](https://olat.bbw.ch/auth/1%3A1%3A32044700929%3A3%3A0%3Aserv%3Ax%3A_csrf%3Ad6d20b18-d00f-4da6-8969-ce5d2b958249/DHCP%20PXE/DHCP-praesi.pdf)
## Umgebung
- VMware Workstation Pro
    - Ubuntu Server (Ohne GUI)
    - Windows Client

### Requirements

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
default-lease-time 600;
max-lease-time 7200;
    
subnet 192.168.1.0 netmask 255.255.255.0 {
 range 192.168.1.150 192.168.1.200;
 option routers 192.168.1.254;
 option domain-name-servers 192.168.1.1, 192.168.1.2;
 option domain-name "mydomain.example";
}
```

#### 3. Dienst neustarten

```
sudo systemctl restart isc-dhcp-server.service
```
## Sources
- Offizielle Installaition `isc-dhcp-server` von Canonical  
https://ubuntu.com/server/docs/how-to-install-and-configure-isc-dhcp-server