### KN07: PAAS
Public IP für RDS von AWS
Um eine Public IP für eine RDS von AWS zu erhalten, muss die RDS in einem öffentlichen Subnetz erstellt werden. Das Subnetz muss eine Route zu einem Internet Gateway haben. Die RDS muss in einer Security Group sein, die eingehenden Traffic auf den Port 3306 zulässt.

![alt text](<Bildschirmfoto 2025-01-30 um 15.23.54.png>) 

![alt text](<Bildschirmfoto 2025-01-30 um 11.06.34.png>)

PAAS (Platform as a Service) und SAAS (Software as a Service) bieten gegenüber einer selbst gehosteten Datenbank zahlreiche Vorteile:
•	Regelmäßige Sicherheitsaktualisierungen: Sicherheitslücken werden durch automatische Updates geschlossen.

•	Dynamische Skalierung: Die Datenbank wächst flexibel mit den 
Anforderungen des Unternehmens.

•	Effiziente Kostenstruktur: Durch das nutzungsbasierte Abrechnungsmodell fallen nur Kosten für tatsächlich genutzte Ressourcen an, ohne Investitionen in eigene Hardware oder Wartung.

•	Hohe Verfügbarkeit: Cloud-Anbieter gewährleisten durch Redundanz und Ausfallsicherheit eine stabile Performance.

•	Umfassende Sicherheitsmaßnahmen: Funktionen wie Verschlüsselung und Zugriffskontrollen sind standardmäßig integriert.

•	Schnelle Inbetriebnahme: Datenbanken lassen sich in wenigen Minuten einrichten und konfigurieren, wodurch sie sofort einsatzbereit sind.

#### Auto Scaling aktiviert:

![alt text](<Bildschirmfoto 2025-01-30 um 19.36.34.png>)

#### Erstellte Ressourcen/Objekte und CloudFormation

AWS CloudFormation ist ein Service zur Verwaltung von Infrastruktur als Code. Er ermöglicht die Definition und Bereitstellung von AWS-Ressourcen mithilfe von Vorlagen. Diese Vorlagen enthalten die gewünschte Infrastruktur und Konfigurationen, sodass sie automatisch erstellt, aktualisiert und verwaltet werden können. Dadurch wird die Bereitstellung konsistenter, wiederholbar und effizienter.

![alt text](<Bildschirmfoto 2025-01-30 um 20.06.17.png>) 

### 3. Warum PAAS statt eigener DB?

•	Automatische Wartung: AWS verwaltet Backups, Updates und Hochverfügbarkeit.

•	Einfache Skalierung: Mehr Speicher und Rechenleistung mit wenigen Klicks.

•	Keine manuelle Installation: Kein eigenes Server-Setup erforderlich.

•	Sicherheit: AWS verwaltet Verschlüsselung, Firewall-Regeln und Netzwerksicherheit.

![alt text](<Bildschirmfoto 2025-01-30 um 20.07.23.png>) 