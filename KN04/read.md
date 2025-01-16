<!-- ## 1A.

## Erklärung:
## cloud-config
Notwendig, um die Datei als Cloud-init-Datei zu identifizieren.

###	users

Definiert Benutzer und deren Eigenschaften.

name: Benutzername, hier ubuntu.

sudo: Gibt sudo-Rechte ohne Passwortabfrage.

groups: Fügt den Benutzer in die Gruppe users ein.

shell: Setzt die Standard-Shell des Benutzers.

ssh_authorized_keys: Hinterlegt den öffentlichen SSH-Schlüssel für den Benutzer.

###	ssh_pwauth

Erlaubt (false) oder verbietet (true) Passwortauthentifizierung für SSH.

###	disable_root

Deaktiviert den Root-Benutzer.

###	package_update

Führt ein apt-get update aus.

###	packages

Installiert Pakete, z. B. Apache und MySQL.

###	runcmd

Führt nach der Konfiguration Kommandos aus, z. B. eine Bestätigung ausgeben. -->