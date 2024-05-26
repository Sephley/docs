# Record-Typen
- [x] *Recherchieren Sie verschiedene Record-Typen und erklären Sie diese.*

|**Record** |**Beschreibung** |**Beispiel** |
|---|---|---|
|A |Das "A" steht für Adresse. Dies ist der fundamentalste Bestandteil des DNS, denn er verbindet Domainnamen mit IP-Adressen. |`www IN A 192.168.1.4` |
|AAAA |Gleich wie A, aber mit IPv6. |`www IN AAAA 2607:f8b0:400a:800::200e` |
|CNAME |Canonical Name record. CNAME Records können einem Domänen-Namen einen weiteren Namen zuweisen. Er wird oft dafür verwendet, Subdomänen wie www oder mail, der Domäne, die den Inhalt hostet zuzuordnen. |`www.sephley.local CNAME www.sephley.com` |
|Alias |Wie ein CNAME record, können Alias Records einem Domänen-Namen einen weiteren Namen zuweisen. Allerdings können Aliases bestehen, auch wenn bereits ein Record mit demselben Namen existiert. |`@ IN ALIAS sephley.local.` |
|MX |Mail Exchange Record. Sie leiten Mails an die dazugehörigen Server weiter und werden auch zur Priorisierung verwendet |`sephley.local. IN MX 10 mail.sephley.local.` |
|NS |NS steht für «Name Server». Er entscheidet, welcher DNS-Server massgeblich ist. |`@ IN NS primary.sephley.local.` |
|PTR |PTR steht für «Pointer» und macht das Gegenteil des A Records. Er kann IP-Adressen in Domain Namen verwandeln, was bedeutet das er in der Reverse-Zone verwendet wird. |`2 IN PTR primary.sephley.local` |