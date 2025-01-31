## KN06: Skalierung – AWS Webserver mit Auto Scaling und Load Balancer

###  Reverse Proxy Erklärung
Ein Reverse Proxy ist ein Server, der Anfragen von Clients entgegennimmt und an einen oder mehrere Backend-Server weiterleitet. In dieser Aufgabe wird Nginx als Reverse Proxy verwendet, um Anfragen von Port 80 an die eigentliche Applikation weiterzuleiten, die intern auf Port 5000 (.NET) bzw. 5001 (Java) läuft. Dies ermöglicht eine bessere Sicherheit, Lastverteilung und Skalierbarkeit.

## Anwendung testen
![alt text](<Bildschirmfoto 2025-01-29 um 12.39.49.png>)

- API-Endpunkte: Die Endpunkte können direkt über die Swagger-UI getestet werden.

![alt text](<Bildschirmfoto 2025-01-29 um 18.24.02.png>)

- hier wurde es von 8gBb zu 20gb gewechselt.

![alt text](<Bildschirmfoto 2025-01-29 um 18.25.34.png>) 

![alt text](<Bildschirmfoto 2025-01-29 um 18.28.42.png>) 


## Horizontale Skalierung mit Auto Scaling

1. Einrichtung eines Load Balancers

Ein Application Load Balancer wurde erstellt, um den Traffic auf mehrere Instanzen zu verteilen.

DNS-Name des Load Balancers: KN06loadbalancer-123456.elb.amazonaws.com

**Target Group:**

**Health Check Path:** /swagger/index.html

**Verknüpfte Instanzen:** Zwei Instanzen (KN06 und eine zusätzliche Kopie).

2. Horizontale Skalierung mit Auto Scaling

2.1 Launch Template

Ein Launch Template wurde basierend auf dem bestehenden AMI erstellt.
Details:

Instanztyp: t2.medium

![alt text](<Bildschirmfoto 2025-01-29 um 18.31.17.png>)

Sicherheitsgruppen: HTTP (Port 80) und 5000 für internen Traffic.

VPC und Subnet: Gleich wie die bestehende Umgebung.

**2.2 Auto-Scaling-Gruppe**

Eine Auto-Scaling-Gruppe wurde eingerichtet, um sicherzustellen, dass immer mindestens 2 

***Instanzen die aktiv sind:***

**Desired Capacity:** 2

**Minimum Capacity:** 2

**Maximum Capacity:** 5

**Scaling Policies:**

Neue Instanz starten, wenn die CPU-Auslastung über 75% steigt.

Eine Instanz entfernen, wenn die CPU-Auslastung unter 25% fällt.

## 3. Test der Auto-Scaling-Funktionalität

Eine Instanz wurde manuell gestoppt, um den Ausfallschutz zu testen.

Ergebnis: Die Auto-Scaling-Gruppe startete automatisch eine neue Instanz, um die gewünschte Anzahl von 2 Instanzen beizubehalten.

### Fazit
Die .NET-Applikation wurde erfolgreich bereitgestellt und kann horizontal skaliert werden.

Mit Auto Scaling ist die Umgebung vor Ausfällen geschützt.

Der Load Balancer verteilt den Traffic gleichmäßig auf die verfügbaren Instanzen.