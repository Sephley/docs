# Was ist ACME?

ACME ist ein Protokoll, das die automatische Verwaltung von SSL/TLS-Zertifikaten ermöglicht. Es wird von Let's Encrypt verwendet, um Zertifikate auszustellen und zu erneuern.

Wie man ACME einsetzen sollte, ist schwer zu sagen, denn es gibt sehr viele Anwendungsmethonden (siehe <https://letsencrypt.org/docs/client-options/>).

Grundsätzlich hilft es, wenn man eine Lösung nimmt, welche gut mit der verwendetetn Umgebung zu integrieren ist. Beispielsweise würde ich etwas Shell-basiertes verwenden, da ich mit damit bestens auskenne.

Allerdings würde jemand, der sich mit Docker auskennt eher eine Lösung wie [letsproxy](https://hub.docker.com/r/neilpang/letsproxy) verwenden.