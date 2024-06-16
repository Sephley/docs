# Verschlüsslungsverfahren
- [x] *Welche Verschlüsselungsverfahren können mit TLS eingesetzt werden?*

Es gibt eine Menge Verschlüsselungsverfahren welche mit TLS eingesetzt werden können, da es viele Prozesse gibt. Dempentsprechend hat man viele Möglichkeiten.  
Wenn man diese sich für jeden Bereich ein Verschlüsslungsverfahren aussucht, hat man eine "Cipher Suite".

![tls-cipher-microsoft](../images/tls-ciphers-microsoft.png)  
[*Bild von Microsoft*](https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Flearn.microsoft.com%2Fen-us%2Fwindows%2Fwin32%2Fsecauthn%2Fimages%2Ftls-cipher-suite.png&f=1&nofb=1&ipt=1ccdfea13751b06d3c83503ef8d18b5dfd7eed7683db07e0517b1f11d5166b84&ipo=images)

Hier sind einige Beispiele für TLS Cipher Suites, die diese Algorithmen kombinieren:

| **Cipher Suite**| **Beschreibung**|
|--|--|
| `TLS_AES_128_GCM_SHA256`| Verwendet AES-128 im GCM-Modus für die Verschlüsselung und SHA-256 für die HMAC.|
| `TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256`| Verwendet ECDHE für den Schlüsselaustausch, RSA für die Authentifizierung, AES-128 im GCM-Modus für die Verschlüsselung und SHA-256 für die HMAC.|
| `TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384`| Verwendet ECDHE für den Schlüsselaustausch, ECDSA für die Authentifizierung, AES-256 im GCM-Modus für die Verschlüsselung und SHA-384 für die HMAC.|
| `TLS_CHACHA20_POLY1305_SHA256`| Verwendet ChaCha20 für die Verschlüsselung und Poly1305 für die Authentifizierung, zusammen mit SHA-256.|

Hier ist eine Liste von allen Cipher Suites, welche Mozilla Firefox unterstützt:  
<https://wiki.mozilla.org/Security/Cipher_Suites>