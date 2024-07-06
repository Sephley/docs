# Was ist ACME?

ACME ist ein Protokoll, das die automatische Verwaltung von SSL/TLS-Zertifikaten ermöglicht. Es wird von Let's Encrypt verwendet, um Zertifikate auszustellen und zu erneuern. Im Jahr 2012 erkannte die Internet Security Research Group (ISRG), dass viele Webseitenbetreiber Schwierigkeiten hatten, SSL/TLS-Zertifikate manuell zu erneuern. Dies führte oft zu abgelaufenen Zertifikaten, was nicht nur Sicherheitsrisiken, sondern auch Vertrauensverlust bei den Nutzern zur Folge hatte. Um dieses Problem zu lösen, entwickelte die ISRG das Let's Encrypt-Projekt, eine kostenlose, automatisierte und offene Zertifizierungsstelle. Das Herzstück dieses Projekts war das ACME-Protokoll (Automated Certificate Management Environment), das es Servern ermöglichte, Zertifikate automatisch zu beantragen und zu erneuern.

ACME revolutionierte die Art und Weise, wie Zertifikate verwaltet werden. Es automatisierte die bisher manuellen und fehleranfälligen Prozesse und stellte sicher, dass Webseiten stets mit aktuellen Zertifikaten geschützt sind.

Wie man ACME einsetzen sollte, ist schwer zu sagen, denn es gibt sehr viele Anwendungsmethonden (siehe <https://letsencrypt.org/docs/client-options/>).

Grundsätzlich hilft es, wenn man eine Lösung nimmt, welche gut mit der verwendetetn Umgebung zu integrieren ist. Beispielsweise würde ich etwas Shell-basiertes verwenden, da ich mit damit bestens auskenne.

Allerdings würde jemand, der sich mit Docker auskennt eher eine Lösung wie [letsproxy](https://hub.docker.com/r/neilpang/letsproxy) verwenden.