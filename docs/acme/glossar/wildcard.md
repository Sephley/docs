# Wildcard Zertifikate

Ein Wildcard-Zertifikat wird für eine Domain und alle ihre Subdomains ausgestellt. Anstatt ein separates Zertifikat für jede Subdomain zu benötigen, kann ein Wildcard-Zertifikat für z.B. *.example.com sowohl www.example.com, mail.example.com, als auch jede andere Subdomain von example.com abdecken.

Die grösste Sorge bei Wildcard-Zertifikaten besteht darin, dass bei einem Ausfall eines Servers oder einer Subdomäne, die von der Wildcard abgedeckt wird, alle Subdomänen gefährdet sein können.  Mit anderen Worten: Die anfängliche Einfachheit der Wildcard kann zu erheblichen Problemen führen, wenn etwas schief geht.