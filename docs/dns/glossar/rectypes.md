# Record-Typen
- [x] *Recherchieren Sie verschiedene Record-Typen und erklären Sie diese.*

|**Record** |**Beschreibung** |**Beispiel** |
|---|---|---|
|A |Das « A » steht für Adresse. Dies ist der fundamentalste Bestandteil des DNS, denn er verbindet Domainnamen mit IP-Adressen. |`www     IN      A       192.168.1.4` |
|AAAA |Gleich wie A, aber mit IPv6. |`www   IN  AAAA    2607:f8b0:400a:800::200e` |
|CNAME |Canonical Name record. A CNAME record establishes one domain as an alias to another (thereby routing all traffic addressed to the alias to the target; the canonical address). |`www.sephley.local    CNAME      www.sephley.com` |
|Alias |Like a CNAME record, Alias records can be used to map one address to another. But Aliases can coexist with other records using the same name. |`@    IN    ALIAS    sephley.local.`  |
|MX |Mail Exchange Record. These records will redirect a domain’s email to the servers hosting the domain’s user accounts. Mail exchange records are used for determining the priority of email servers for a domain. |`sephley.local. IN MX 10 mail.sephley.local.` |
|PTR |PTR steht für «Pointer» und macht das Gegenteil des A Records. Er kann IP-Adressen in Domain Namen verwandeln, was bedeutet das er in der Reverse-Zone verwendet wird. |`2   IN      PTR     primary.sephley.local` |