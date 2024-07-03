# Certbot mit Bind9 in Betrieb nehmen

Im Geschäft stellen wir unsere Wildcard Zertifikate manuell aus, denn es sei zu riskant ist dies zu automatisieren.

Das ist natürlich blödsinn, denn ein funktionierender Automatismus macht keine Fehler und ist gar weniger riskant als wenn ein Mensch es manuell macht.

Das einzige Risiko, welches besteht ist wenn Certbot einen breaking change einführt und es niemand merkt.

## Bind DNS für Letsencrypt aufsetzen

Wir setzen Bind9 als DNS ein, also müssen wir diesen umkonfigurieren. Hierfür verwende ich die [Anleitung aus Olat](https://www.hagen-bauer.de/2019/06/authoritive-bind-server.html).

## Installation

Wir verwenden im Geschäft kein snap, also wir müssen eine andere Installationsmethode suchen.

Pip ist gemäss der [offiziellen Doku](https://eff-certbot.readthedocs.io/en/latest/install.html#alternative-2-pip) eine Alternative zu snap. Diese Methode ist für uns geeignet, da Python und Pip standardmässig auf unseren Servern installiert sind.

Also können wir folgende Anleitung verwenden: <https://certbot.eff.org/instructions?ws=nginx&os=pip&tab=wildcard>

### 1. Pakete installieren / entfernen

>müssen wir nicht, da diese bei uns Standardmässig installiert sind, aber so würde es funktionieren.
```
sudo apt update
sudo apt install python3 python3-venv libaugeas0
```

Zuerst sorgen wir dafür, dass Certbot nicht bereits installiert ist.
```
sudo apt-get remove certbot
```

### 2. Python virtual envrionment erstellen

```
sudo python3 -m venv /opt/certbot/
sudo /opt/certbot/bin/pip install --upgrade pip
```

### 3. Certbot installieren

```
sudo /opt/certbot/bin/pip install certbot certbot-nginx
```

Dann noch den Symlink erstellen um den `certbot` Befehl ausführen zu können.

```
sudo ln -s /opt/certbot/bin/certbot /usr/bin/certbot
```

### 4. Certbot Plugin installieren

Da wir Bind9 einsetzen, benötigen wir das [dns-rfc2136 Plugin](https://certbot-dns-rfc2136.readthedocs.io/en/stable/).