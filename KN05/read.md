# A. Grundbegriffe und private IP wählen (30%)

## 1. Erklärung der Begriffe:

### VPC (Virtual Private Cloud):

Eine VPC ist ein isolierter, privater Netzwerkbereich in der Cloud, in dem Sie Ihre Ressourcen wie Instanzen, Datenbanken und mehr betreiben können. Es ist vergleichbar mit einem privaten Netzwerk in einem Rechenzentrum, in dem Sie die volle Kontrolle über IP-Adressbereiche, Subnetze und Sicherheitsregeln haben.

###	Subnetz (Subnet):
Ein Subnetz ist ein Teilbereich eines VPCs, der eine kleinere IP-Adressrange abdeckt. Subnetze dienen dazu, Netzwerke zu segmentieren, z. B. für öffentliche und private Ressourcen. Sie bestimmen, ob die Ressourcen in einem Subnetz über das Internet zugänglich sind oder nur intern kommunizieren können.

![alt text](<Bildschirmfoto 2025-01-24 um 13.32.08.png>)

###	Öffentliche IP (Public IP):
Eine öffentliche IP-Adresse ist eine weltweit eindeutige Adresse, die für den Zugriff auf Ressourcen über das Internet verwendet wird.

###	Private IP:
Eine private IP-Adresse ist nur innerhalb eines VPCs sichtbar und wird für die interne Kommunikation zwischen Ressourcen verwendet.

###	Statische IP:
Eine statische IP ist eine IP-Adresse, die sich nicht ändert, selbst wenn die zugehörige Instanz gestoppt und neu gestartet wird. AWS nennt diese Elastic IP.

![alt text](<Bildschirmfoto 2025-01-24 um 16.06.57.png>) 


|Ressource | IP-Adresse  |
|--------- | ----------  |
| web      | 172.31.32.10|
| db       | 172.31.32.20|


### Sicherheitsgruppen
Regeln:

HTTP (Port 80): Zugriff von überall (0.0.0.0/0).
HTTPS (Port 443): Zugriff von überall (0.0.0.0/0).

![alt text](<Bildschirmfoto 2025-01-24 um 15.29.53.png>) 

Sicherheitsgruppe für den Datenbankserver
Eingehende Regeln:

MySQL (Port 3306): Zugriff nur von der privaten IP des Webservers.

![alt text](<Bildschirmfoto 2025-01-24 um 15.34.22.png>)

und hier sind alle Sicherheitsgruppen

![alt text](<Bildschirmfoto 2025-01-24 um 15.48.18.png>) 

### Verbindungen testen

```
mysql -h 172.31.176.30 -u admin -p
```

### Ergebnisse
![alt text](<Bildschirmfoto 2025-01-24 um 16.31.06.png>) 

![alt text](<Bildschirmfoto 2025-01-24 um 16.32.42.png>)

![alt text](<Bildschirmfoto 2025-01-24 um 16.30.37.png>) 