# Basisinstallation von Certbot

[Certbot](https://certbot.eff.org/) ist ein Open-Source Tool, welches automatisch Let's Encrypt Zertifikate generieren kann.

## Voraussetzungen

Um Certbot für mich auszutesten, habe ich es auf meinem Linode installiert. Auf meinem Linode ist ein nginx Webserver auf Ubuntu 24.04 installiert.

Selbstverständlich benötigt man bei dem DNS-Provider auch ein Record, der auf den Linode zeigt.

## Installation

Da snap nun die offiziell-unterstützte Installationsmethode ist, verwenden wir snap.

<https://certbot.eff.org/instructions?ws=nginx&os=ubuntufocal>

Zuerst sorgen wir dafür, dass Certbot nicht bereits installiert ist.
```
sudo apt-get remove certbot
```

Danach können wir Certbot mittels Snap installieren.
```
sudo snap install --classic certbot
```

Mittels diesem nächsten Befehl können wir Certbot nicht nur ein Zertifikat ausstellen, sondern es wird auch die `nginx` config für HTTPS angepasst.
```
sudo certbot --nginx
```

![certbot_1](../images/certbot_1.png)

![certbot_2](../images/certbot_2.png)

Somit haben wir ein Zertifikat ausgestellt.

![certbot_cert](../images/certbot_cert.png)

## Probleme / Anmerkungen

Keine, die Installation erfolgte reibungslos. Es hat mich wirklich überrascht, wie leicht es funktioniert hat.