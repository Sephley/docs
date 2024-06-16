# Wireshark Sniffing

- [ ] *TLS Wireshark Analyse*

*TLS ist auch dazu da, den Verkehr vor neugierigen Blicken zu verheimlichen. Doch zu Debugging-Zwecke wäre es oft hilfreich, den Traffic trotzdem mittels Wireshark mithören zu können. Und tatsächlich lässt sich dies bewerkstelligen, wenn man Einfluss auf eine der Seiten hat. Natürlich wollen Sie das durchführen und erforschen. Sie finden alles Wichtige dazu hier: https://wiki.wireshark.org/TLS Tipp: Sie müssen dem TLS Stream folgen. Und da lohnt es sich oft, den Hex Dump anzuzeigen. Insbesondere bei der Nutzung binärer Daten. Auch ein Blick ins Hex Dump Feld und dessen Reiter ist lohnend!*

><https://www.sephley.com>

[tls capture download](../tls.pcapng)

Wenn wir in dieser Datei nach `ssl` filtern, können wird der Handshake klar ersichtlich.

![wireshark-1](../images/wireshark-1.png)

<https://wiki.wireshark.org/TLS>