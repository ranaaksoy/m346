# KN04: Cloud-init und AWS

#### Zusammenfassung

In diesem Dokument werden die Schritte erläutert, die unternommen wurden, um SSH-Keys mithilfe von Cloud-Init zu integrieren und eine AWS-Instanz erfolgreich zu konfigurieren.

#### Überblick

Eine Cloud-Init-Datei wurde verwendet, um die Instanz zu konfigurieren. Die Datei beinhaltete folgende Konfigurationsaspekte:

• Benutzererstellung

• Integration von SSH-Keys

• Automatische Installation von Paketen

**Detaillierte Schritte**

#### Erstellung der Cloud-Init-Datei

Die Cloud-Init-Datei wurde mit den erforderlichen Konfigurationen erstellt. Diese beinhaltete spezifische Anweisungen zur Einrichtung des Systems nach dem Start der Instanz, einschließlich der folgenden Punkte:


#### Cloud-Init in AWS-Instanz hochladen

Um die Cloud-Init-Datei in einer neuen AWS-Instanz zu verwenden, sind folgende Schritte notwendig:

1.	AWS Management Console öffnen: Melde dich bei der AWS Management Console an.

2.	Neue EC2-Instanz erstellen: Erstelle eine neue EC2-Instanz und navigiere zu den erweiterten Details.

3.	Cloud-Init-Datei hochladen: Im Abschnitt “Advanced Details” > “User data” kannst du die Cloud-Init-Datei hochladen, die die Instanz bei der Initialisierung konfiguriert.

4.	Sicherheitsgruppe hinzufügen: Achte darauf, eine Sicherheitsgruppe hinzuzufügen, die SSH-Zugriff auf die Instanz erlaubt (Port 22).
    
#### Verbindung zur Instanz herstellen

Es gibt zwei Methoden, um sich mit der Instanz zu verbinden:

•	Mit dem GUI-SSH-Key: Verwende den SSH-Befehl, um dich mit der Instanz zu verbinden.

```
ssh -i "name.pem" ubuntu@<instance-ip>
```

Erfolg: Die Verbindung wurde erfolgreich hergestellt.

•	Mit dem Cloud-Init-SSH-Key: Verwende den Cloud-Init-SSH-Key, um ebenfalls auf die Instanz zuzugreifen.

```
ssh -i "name.pem" ubuntu@<instance-ip>
```

#### Fehlerbehebung und Logs

Falls die Verbindung zur Instanz fehlschlägt, ist es hilfreich, die Logs zu überprüfen:

• **Cloud-Init Logs:** Du kannst die Cloud-Init-Logs einsehen, um etwaige Probleme während der Initialisierung zu erkennen. Diese befinden sich normalerweise unter /var/log/cloud-init.log und /var/log/cloud-init-output.log auf der Instanz.

• **Sicherheitsgruppen und Firewall:** Stelle sicher, dass die Sicherheitsgruppen und Netzwerkkonfigurationen richtig eingerichtet sind, um den SSH-Zugriff zu ermöglichen.

• **SSH-Fehlerbehebung:** Überprüfe die Fehlermeldungen beim SSH-Login und stelle sicher, dass der richtige Schlüssel verwendet wird und die IP-Adresse korrekt ist.

```
cat /var/log/cloud-init-output.log
```

#### Überprüfung

**Schritte zur Überprüfung:**

Zugriff testen mit beiden privaten Schlüsseln.

**Verifiziere die Pakete:**

curl --version
wget --version

**Ergebnis:**

Die Konfiguration wurde erfolgreich durchgeführt.

Datenbank und Webserver Konfiguration

**Überblick**

Dieses Projekt beinhaltet die Konfiguration und den Test einer MySQL-Datenbank sowie eines Webservers in AWS. Beide Server wurden in einem gemeinsamen VPC-Netzwerk bereitgestellt, um sichere und direkte Verbindungen zu gewährleisten.

Schritte zur Überprüfung der MySQL-Verbindung

#### Verbindung zur Datenbank vom Webserver aus testen

Mit folgendem Befehl kann die Verbindung zur Datenbank geprüft werden:

```
mysql -u admin -p -h 172.31.87.243
```

Wenn die Verbindung erfolgreich ist, wird der MySQL-Monitor geöffnet:

Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 32
Server version: 5.5.5-10.11.8-MariaDB-0ubuntu0.24.04.1 Ubuntu 24.04
2. Verbindung mit nc testen
nc -zv 172.31.87.243 3306

**Ausgabe:**

Connection to 172.31.87.243 3306 port [tcp/mysql] succeeded!
PHP-Skript zur Datenbankverbindung
Ein PHP-Skript wurde erstellt, um die Verbindung von der Webserver-Seite zu testen.

**Beispielcode:**

<?php
$servername = "172.00.00.000";
$username = "admin";
$password = "admin";
$dbname = "MainDatabase";

$conn = new mysqli($servername, $username, $password, $dbname);

if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}
echo "Connected successfully to the database.";
?>

![alt text](<Bildschirmfoto 2025-01-17 um 15.07.08.png>)

#### Netzwerkregeln (AWS Sicherheitsgruppen)

**Eingehender Datenverkehr**

Port 3306: Zugriff für MySQL von überall (0.0.0.0/0).
Port 22: SSH-Zugriff von überall (0.0.0.0/0).

![alt text](<Bildschirmfoto 2025-01-17 um 15.23.34.png>)

**Ausgehender Datenverkehr**

Alle Ports: Vollständiger Zugriff für ausgehenden Datenverkehr.


**Status der Dienste**

MySQL-Dienst auf der Datenbankinstanz
```
sudo systemctl status mysql
```

**Ergebnis:**

mariadb.service - MariaDB 10.11.8 database server
Loaded: loaded /usr/lib/systemd/system/mariadb.service; enabled; preset: >
Active: active (running) since Fri 2024-12-06 10:05:20 UTC; 1min 13s ago
UFW-Status
Die Firewall (ufw) ist auf der Datenbankinstanz deaktiviert:

```
sudo ufw Status
```

**Ausgabe:**

![alt text](<Bildschirmfoto 2025-01-17 um 15.07.16.png>)
![alt text](<Bildschirmfoto 2025-01-17 um 15.07.28.png>)
![alt text](<Bildschirmfoto 2025-01-17 um 15.07.44.png>)