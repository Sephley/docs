# Certbot mit Bind9 in Betrieb nehmen

- [ ] *Certbot mit Wildcard Zertifikat in Betrieb nehmen (geschäftsumfeld)*

Im Geschäft stellen wir unsere Wildcard Zertifikate manuell aus, denn es sei zu riskant ist dies zu automatisieren.

Das ist natürlich blödsinn, denn ein funktionierender Automatismus macht keine Fehler und ist gar weniger riskant als wenn ein Mensch es manuell macht.

Das einzige Risiko, welches besteht, ist wenn Certbot einen breaking change einführt und es niemand merkt.

Am idealsten wäre es warscheinlich wenn wir unsere Wildcard Zertifikate ganz ersetzen würden, [siehe Glossar](../glossar/wildcard.md).

## Bind DNS für Letsencrypt aufsetzen

Wir setzen Bind9 als DNS ein, also müssen wir diesen umkonfigurieren. Hierfür verwende ich die [Anleitung aus Olat](https://www.hagen-bauer.de/2019/06/authoritive-bind-server.html).

## Installation

Wir verwenden im Geschäft kein snap, also wir müssen eine andere Installationsmethode suchen.

Pip ist gemäss der [offiziellen Doku](https://eff-certbot.readthedocs.io/en/latest/install.html#alternative-2-pip) eine Alternative zu snap. Diese Methode ist für uns geeignet, da Python und Pip standardmässig auf unseren Servern installiert sind.

Also können wir folgende Anleitung verwenden: <https://certbot.eff.org/instructions?ws=nginx&os=pip&tab=wildcard>

### 1. Pakete installieren / entfernen

>müssen wir nicht, da diese bei uns Standardmässig installiert sind, aber so würde es funktionieren:
```
sudo apt update
sudo apt install python3 python3-venv libaugeas0
```

Dann sorgen wir dafür, dass Certbot nicht bereits installiert ist.
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

## Automatische Ernuerung

Die automatische Ernuerung kann man via Cronjob erzielen.

```
echo "0 0,12 * * * root /opt/certbot/bin/python -c 'import random; import time; time.sleep(random.random() * 3600)' && sudo certbot renew -q" | sudo tee -a /etc/crontab > /dev/null
```

## Certbot einsetzen

```
sudo certbot \
--server https://acme-v02.api.letsencrypt.org/directory \
--manual --preferred-challenges dns \
-d *.cloudynerd.us -d *.scm.cloudynerd.us
```

## Certbot updaten

Certbot updaten mir gemäss vorgabe monatlich, um die Security auf dem neusten Stand zu halten. Um das oben-genannte Risiko zu vermeiden, lesen wir die Release Notes vor jedem Update.
```
sudo /opt/certbot/bin/pip install --upgrade certbot certbot-nginx certbot-dns-rfc2136
```

## Probleme / Anmerkungen

Diese Methode wurde noch nicht angenommen (bis 08.07.2024 noch nicht), da ich es noch in der Sitzung besprechen muss. Wie oben erwähnt wäre das Ersetzen der Wildcard Zertifkate evtl. auch eine Lösung.