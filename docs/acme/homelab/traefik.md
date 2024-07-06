# ACME in Traefik

<https://doc.traefik.io/traefik/https/acme/>

Ich setze zurzeit einen Traefik reverse Proxy in meiner privaten Umgebung auf. Vor kurzen habe ich herausgefunden, dass dieser auch ACME unterstützt.

Also habe ich mir vorgenommen, ACME bestmöglich zu integrieren. Mein Traefik Proxy läuft dockerized auf einer Ubuntu-VM. Ich verwende eine Cloudflare Domäne.

Die Integration mit Cloudflare funktioniert mit dem `/etc/traefik/traefik.yml` file

```
  production:
    acme:
      email: mail@clusterstack.net
      storage: /etc/traefik/certs/acme.json
      caServer: "https://acme-v02.api.letsencrypt.org/directory"
      dnsChallenge:
        provider: cloudflare
        resolvers:
          - "1.1.1.1:53"
          - "8.8.8.8:53"
```

Somit werden meine Zertifikate automatisch erneuert.