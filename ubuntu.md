1.	Öffne die Ubuntu-Shell.
	2.	Gib diesen Befehl ein, um einen neuen Benutzer anzulegen:
adduser mikail
Folge den Anweisungen, um ein Passwort zu setzen.
	3.	Füge den Benutzer zur sudo-Gruppe hinzu:
usermod -aG sudo mikail
	4.	Standardbenutzer ändern:
Gib diesen Befehl in PowerShell ein (nicht in Ubuntu!):
wsl -d Ubuntu -u mikail
Wenn du das dauerhaft machen willst:
ubuntu config --default-user mikail

⸻

Grundlegende WSL/Ubuntu-Befehle für Dateien & Ordner

Verzeichnisse anzeigen:
	•	ls zeigt Dateien und Ordner im aktuellen Verzeichnis
	•	ls -la zeigt zusätzlich versteckte Dateien (dotfiles)

Navigieren:
	•	cd /home/mikail wechselt in dein Home-Verzeichnis
	•	cd .. geht ein Verzeichnis zurück
	•	pwd zeigt den aktuellen Pfad an

Ordner & Dateien erstellen:
	•	mkdir neuer_ordner erstellt einen neuen Ordner
	•	touch datei.txt erstellt eine leere Datei
	•	nano datei.txt öffnet eine Datei im Terminal-Editor (Strg+O speichern, Strg+X beenden)

⸻

Docker in WSL nutzen

Docker installieren (falls nicht vorhanden):
	•	sudo apt update
	•	sudo apt install docker.io

Docker aktivieren:
	•	sudo systemctl start docker startet den Docker-Dienst
	•	sudo systemctl enable docker startet Docker beim Systemstart automatisch

Achtung: systemctl funktioniert in WSL manchmal nicht direkt!

Docker-Befehle:
	•	sudo docker ps zeigt laufende Container
	•	sudo docker images zeigt verfügbare Images
	•	sudo docker pull ubuntu lädt ein Ubuntu-Image herunter
	•	sudo docker run -it ubuntu startet einen Container interaktiv

Docker in WSL ohne systemd starten:
	•	sudo service docker start
	•	oder: dockerd &

⸻

sudo apt Befehle erklärt
	•	sudo apt update – Paketlisten aktualisieren
	•	sudo apt upgrade – installierte Pakete aktualisieren
	•	sudo apt install <paket> – neues Paket installieren
	•	sudo apt remove <paket> – Paket entfernen
	•	sudo apt search <paket> – nach Paket suchen

Beispiel:
sudo apt install curl git nano
