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

cd - springt in das letzte Verzeichnis zurück.
	•	tree zeigt die Verzeichnisstruktur als Baum (erst mit sudo apt install tree installieren).
	•	du -sh * zeigt die Größe aller Dateien/Ordner im aktuellen Verzeichnis.
	•	find . -name "*.js" sucht alle .js-Dateien im aktuellen Verzeichnis (rekursiv).

Datei-Handling & Suchen:
	•	cat file.txt gibt den Inhalt einer Datei aus.
	•	less file.txt zeigt große Dateien seitenweise an (mit q beenden).
	•	grep "Suchwort" datei.txt findet Zeilen mit dem Suchwort.
	•	grep -rnw . -e "function" durchsucht rekursiv alle Dateien nach “function”.
	•	touch {1..5}.txt erstellt fünf Dateien (1.txt bis 5.txt).
	•	head -n 20 file.txt zeigt die ersten 20 Zeilen an.
	•	tail -f log.txt beobachtet die Datei live (z. B. Log-Dateien).

Pakete & Tools:
	•	apt list --installed zeigt alle installierten Pakete.
	•	dpkg -L <paketname> zeigt an, welche Dateien ein Paket installiert hat.
	•	sudo apt autoremove entfernt überflüssige Pakete.
	•	sudo apt clean leert den Paket-Cache.

System & Prozesse:
	•	top oder htop zeigt laufende Prozesse (htop ist grafisch besser – erst sudo apt install htop).
	•	ps aux | grep node zeigt alle laufenden Node.js-Prozesse.
	•	kill -9 <PID> beendet einen Prozess hart.
	•	df -h zeigt die Speicherbelegung der Laufwerke.
	•	free -h zeigt die RAM-Auslastung.

Entwicklerfreundlich:
	•	alias ll="ls -la" erstellt eine Abkürzung (in ~/.bashrc oder ~/.zshrc).
	•	code . öffnet den aktuellen Ordner in VS Code (nur mit VS Code WSL installiert).
	•	npm init startet ein neues Node.js-Projekt.
	•	node öffnet die Node.js-Konsole.
	•	curl ifconfig.me zeigt die öffentliche IP-Adresse.
	•	chmod +x script.sh macht ein Script ausführbar.

Docker Einzeiler:
	•	docker images zeigt alle Docker-Images.
	•	docker ps -a zeigt alle Container, auch gestoppte.
	•	docker rm $(docker ps -aq) löscht alle Container.
	•	docker rmi $(docker images -q) löscht alle Images.
	•	docker exec -it <container> bash öffnet eine Shell in einem Container.

Fancy Stuff:
	•	cowsay "Hallo Mikail" gibt Text als sprechende Kuh aus (erst sudo apt install cowsay).
	•	figlet "Mikail" erzeugt ASCII-Schrift (erst sudo apt install figlet).
	•	neofetch zeigt Systeminfos in ASCII (erst sudo apt install neofetch).
	•	watch -n 2 date zeigt alle 2 Sekunden das aktuelle Datum.
	•	yes "Mikail ist cool" gibt unendlich oft „Mikail ist cool“ aus (mit Strg+C beenden).

WSL-spezifisch:
	•	explorer.exe . öffnet den aktuellen Pfad im Windows Explorer.
	•	wsl --shutdown beendet alle WSL-Instanzen.
	•	wsl -l -v zeigt installierte WSL-Distributionen.
	•	wsl --set-version Ubuntu 2 stellt Ubuntu auf WSL2 um.
	•	wsl --set-default-version 2 macht WSL2 zum Standard für neue Distros.



Wenn du Docker installierst und dann z. B. nginx laufen lässt, kannst du die NGINX-Startseite über deinen Browser aufrufen (z. B. http://localhost:8080). Unten findest du alle nötigen Schritte – inklusive wie du die HTML-Datei bearbeitest mit vim oder vi.

⸻

Schritt-für-Schritt: NGINX im Docker starten

Zuerst sicherstellen, dass Docker läuft.

Dann NGINX im Container starten mit:

docker run –name mein-nginx -p 8080:80 -d nginx

Erklärung:
	•	--name mein-nginx gibt dem Container einen Namen
	•	-p 8080:80 leitet Port 8080 auf Port 80 im Container weiter
	•	-d startet ihn im Hintergrund
	•	nginx ist das Image, das verwendet wird

Jetzt kannst du im Browser aufrufen:

http://localhost:8080

Du siehst dann die Standardstartseite von NGINX.

⸻

In die Container-Konsole wechseln

docker exec -it mein-nginx bash

Jetzt bist du im Container. Standardmäßig liegt die HTML-Datei hier:

cd /usr/share/nginx/html

Mit ls kannst du die Dateien dort sehen.

Die Datei heißt meist index.html.

⸻

HTML-Datei bearbeiten mit vim oder vi

vi index.html

oder

vim index.html

Wenn vim nicht installiert ist, kannst du es mit folgendem Befehl im Container nachinstallieren:

apt update && apt install vim

Dann wieder vim index.html eingeben.

⸻

vim/vi Steuerung (Kurz-Anleitung)
	•	Mit Pfeiltasten bewegen
	•	Zum Bearbeiten:
Taste i drücken (Insert-Modus)
	•	Jetzt kannst du schreiben oder ändern
	•	Speichern und beenden:
Taste ESC, dann :wq eingeben (write + quit), dann Enter drücken
	•	Nur beenden ohne Speichern:
ESC, dann :q!

⸻

NGINX neu starten (im Container)

Wenn du Änderungen gemacht hast, kannst du NGINX im Container neu laden mit:

nginx -s reload

Oder:

service nginx reload

Falls das nicht funktioniert, Container neu starten:

exit

dann auf dem Host:

docker restart mein-nginx

⸻

Jetzt zeigt dir http://localhost:8080 deine eigene HTML-Seite an.

Wenn du willst, kann ich dir auch zeigen, wie man ein Volume verwendet, damit du die HTML-Datei außerhalb des Containers auf deinem PC speicherst und direkt bearbeiten kannst – ganz ohne in den Container zu gehen. Sag einfach Bescheid!
