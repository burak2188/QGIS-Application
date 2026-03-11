# Aufgabe: `Connection`-Klasse als Basis für das Plugin
Das Ziel ist es, eine im Plugin verwendbare `Connection`-Klasse zu definieren und sie in einem Script (`main.py`) aufzurufen und zu testen.
Erstelle bei allen Schritten auch immer die nötige Dokumentation. Wenn du Schritt für Schritt vorgehst kann es sein, dass du hinterher ein paar von den früheren Dingen ändern muss - das macht nichts, und ist normal! Denk dran in Sinnabschnitten deinen Code zu committen und immer zu kommentieren, was du in dem Commit gemacht hast.

## Schritt 1: Erstelle einen neuen branch. 
*Ziel:* Arbeite auf einem eigenen _branch_ und lerne, wie man mit _pull-requests_ reviews bekommen kann. 

Arbeit auf einem eigenen branch, der auf diesem hier ("new-task") basiert, damit du jeden der hier aufgelisteten Schritt mit einem _pull request_ in den "new-task"-branch integrieren kannst. 

*Was zu tun ist:* 
1. Erstelle einen neuen _branch_, der auf diesem hier ("new-task") basiert und arbeite nur auf deinem _branch_! Du kannst ihn z.B. "new-task-solution" nennen.
2. Füge einen Kommentar in `main.py` hinzu. 
3. Committe die Änderung in deinen neuen _branch_. 
4. Öffne auf GitHub einen _pull request_ zum _branch_ "new-task" und fordere einen Review von mir an. 
5. Wir mergen den "PR" (_pull request_).

Das werden wir bei allen weiteren Schritten auch so machen. Arbeite also weiterhin auf deinem neuen _branch_.

## Schritt 2: Eine einfache `Connection`-Klasse erstellen
*Ziel*: Erstelle ein Skelett für die Connection Klasse.

*Was zu tun ist:* 
1. Definiere die Klasse `Connection` in der Datei `connection.py`.
2. Füge eine `__init__` Methode hinzu, die username, password und address (mit dem Standardwert "localhost") als Parameter erhält.
3. Gib eine Nachricht in der `__init__` Methode aus, um zu bestätigen, dass die Klasse korrekt instanziiert wurde.
4. Importiere die Klasse `Connection` in der Datei `main.py`
5. Erstelle eine Instanz der Klasse `Connection` in der Datei `main.py`
6. Führe `main.py` aus! Klappt alles?
7. Wenn ja, öffne einen neuen _pull request_ zum _branch_ "new-task" und fordere einen Review von mir, Simon oder Nicolas an.

Zur Übung kannst du (fast) jeden der einzelnen Punkte hier in diesem Schritt in jeweils einem Commit veröffentlichen!

Denk dran: das ist nur das Fundament der Klasse. Hier passier noch gar nichts wirklich. Wenn du dir bei einem dieser Schritt nicht sicher bist, lies im Internet nach oder frag ChatGPT, ob es dir das Definieren von Klassen und die Nutzung einer "Instanz" einer Klasse in Python erklären kann. 

## Schritt 3: Der Klasse `Connection` die `try_connection`-Methode hinzufügen
*Ziel*: Implementiere eine grundlegende Methode, um zu überprüfen, ob die Verbindung zu CouchDB funktioniert.

*Was zu tun ist:* 
1. Definiere die Methode `try_connection` der Klasse `Conncetion`.
2. Verwende `requests.get`, um eine GET-Anfrage an den Haupt-Endpunkt ("http://{username}:{password}@{address}:3001") zu senden.
3. Verarbeite die JSON-Antwort: Wenn sie einen Fehlerstatus enthält, gib den Fehler aus; wenn sie "express-pouchdb" enthält, gib aus, dass die Verbindung erfolgreich ist. 
4. Finde heraus, ob du hier noch weitere Fehler abfangen musst.
5. Rufe die `try_connection`-Methode deiner Instanz der Klasse `Connection` in der Datei `main.py` auf.
6. Führe `main.py` aus! Klappt alles? 
7. Wenn ja, öffne einen neuen _pull request_ zum _branch_ "new-task" und fordere einen Review von mir, Simon oder Nicolas an.


## Schritt 4: Eine `validate_connection`-Methode hinzufügen
*Ziel*: Füge eine Methode hinzu, die `try_connection` verwendet, um die Verbindung zu validieren und das Skript zu stoppen, wenn es nicht funktioniert.

*Was zu tun ist:* 
1. Definiere die Methode `validate_connection` in der Klasse `Conncetion` und rufe `try_connection` darin auf.
2. Wenn die Verbindung ungültig ist, gib eine Nachricht aus und beende das Skript (`quit()`).
3. Diese Methode soll sicherstellen, dass das Skript bei einer fehlerhaften Verbindung gestoppt wird, um weitere (Folge)Fehler zu vermeiden.
4. Rufe die `validate_connection`-Methode deiner Instanz der Klasse `Connection` in der Datei `main.py` auf.
5. Führe `main.py` aus! Klappt alles? 
7. Wenn ja, öffne einen neuen _pull request_ zum _branch_ "new-task" und fordere einen Review von mir, Simon oder Nicolas an.


## Schritt 5: Die `get_project_list`-Methode implementieren
*Ziel*: Implementiere die Funktionalität, um die Liste der verfügbaren Projekte abzurufen.

*Was zu tun ist*: 
1. Füge der Klasse `Conncetion` eine Methode `get_project_list` hinzu, die `requests.get` verwendet, um die Liste der Datenbanken abzurufen (`/_all_dbs`). Denk daran, dass das nur mit einer validierten Verbindung funktionieren sollte. 
2. Entferne den Eintrag `_replicator` aus der Liste, z.B. mit ...`.remove()`. 
3. Speichere die Liste in einem Attribut der Klasse (`self.projects`) und gib sie zurück.
4. Füge in der Datei `main.py` eine Aufruf der `get_project_list`-Methode zu deiner Instanz der Klasse `Connection` hinzu.
5. Führe `main.py` aus! Klappt alles? 
7. Wenn ja, öffne einen neuen _pull request_ zum _branch_ "new-task" und fordere einen Review von mir, Simon oder Nicolas an.

## Schritt 6: Die `select_project`-Methode implementieren
*Ziel*: Ermögliche es dem Benutzer, ein Projekt aus der Liste auszuwählen.

*Was zu tun ist:*
1. Füge der Klasse `Connection` die `select_project`-Methode hinzu, die einen Projektnamen als Eingabe erhält.
2. Stelle sicher, dass das Projekt in der Liste (`self.projects`) existiert. Wenn ja, setze `self.selected_project` auf dieses Projekt. Wenn nein, melde das dem Benutzer.
3. Füge in der Datei `main.py` eine Aufruf der `select_project`-Methode zu deiner Instanz der Klasse `Connection` hinzu und ermögliche die Eingabe durch einen User-input.
4. Führe `main.py` aus! Klappt alles?
7. Wenn ja, öffne einen neuen _pull request_ zum _branch_ "new-task" und fordere einen Review von mir, Simon oder Nicolas an.

Denk dran: Die Auswahl eines Projekts (einer 'Datenbank' in der CouchDB) ist entscheidend, um sicherzustellen, dass nur das richtige Projekt für weitere Operationen verwendet wird. Du musst daher immer überprüfen können, ob ein gültiges Projekt ausgewählt wurde.

## Schritt 7: Die `get_categories`-Methode implementieren
*Ziel*: Hole die Kategorien für das ausgewählte Projekt ab.

*Was zu tun ist:*
1. Füge der Klasse `Connection` die Methode `get_categories` hinzu, die den Field-spezifischen Endpunkt `/config/{project_name}` aufruft, um die Konfiguration des Projekts abzurufen. Denk dran, dass das nur bei einer validen Verbindung und mit einem gültigen Projekt funktionieren kann.
2. Gib in der Methode den Array der verschiedenen Kategorien zurück, die in der Projektkonfiguration definiert sind.
3. Füge in der Datei `main.py` eine Aufruf der `get_categories`-Methode zu deiner Instanz der Klasse `Connection` hinzu und teste die Funkionalität.
4. Führe `main.py` aus! Klappt alles?
7. Wenn ja, öffne einen neuen _pull request_ zum _branch_ "new-task" und fordere einen Review von mir, Simon oder Nicolas an.

*Tipp:* Du findest Infos zu dem "Konfigurations"-Endpoint in der Hilfe von Field Desktop. Die gesamte Adresse des Endpunktes wäre: "http://{username}:{password}@{address}:3000/config/{project_name}" bzw. "http://user:A12345@localhost:3000/config/test" - wenn du es dir mal im Browser vorher anschauen willst. Der Endpunkt liefert nur eine einzige JSON-Datei aus, die die gesamte Konfigurationsinfo umfasst. In der Datei kannst du auch die Struktur des _responses_ erkennen.


## Schritt 8: Den gesamten Ablauf in `main.py` testen
*Ziel*: Setze alles in dem Skript `main.py` zusammen.

*Was zu tun ist:*
1. Erstelle eine Instanz der Klasse Connection und rufe nacheinander get_project_list, select_project und get_categories auf.
2. Gib die Ergebnisse nach jedem Schritt aus (Liste der Projekte, ausgewähltes Projekt und Kategorien).
3. Teste ausgiebig, wo es zu Fehlern kommen kann, und überlege dir, wie du diese in der Klasse `Connection` abfangen kannst. 


