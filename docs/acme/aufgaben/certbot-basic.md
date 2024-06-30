# Basisinstallation von Certbot

Da snap nun die offiziell-unterstützte Installationsmethode ist, verwenden wir snap.

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

![certbot_cert](../images/certbot_cert.png)