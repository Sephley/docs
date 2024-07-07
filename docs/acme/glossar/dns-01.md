# DNS-01

DNS-01 ist eine Art von Challenge-Mechanismus, der von dem ACME Protokoll verwendet wird, um zu verifizieren, dass ein Antragsteller die Kontrolle über eine Domain-name hat.

Es ist die einzige ACME-Challenge, die zur Verifizierung von Wildcard-Zertifikaten verwendet werden kann, da es bei Wildcard-Zertifikaten nicht praktikabel ist, jede Subdomain einzeln zu verifizieren, bietet DNS-01 eine skalierbare Lösung.