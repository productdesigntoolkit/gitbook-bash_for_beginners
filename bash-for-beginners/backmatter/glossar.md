# Glossar

> Wichtige Begriffe aus der Bash-Welt kurz erklärt.

---

## A

**Absolute Path (Absoluter Pfad)**  
Ein vollständiger Pfad, der beim Wurzelverzeichnis `/` beginnt.  
Beispiel: `/home/ralph/dokumente/brief.txt`

**Alias**  
Eine Abkürzung für einen längeren Befehl.  
Beispiel: `alias ll='ls -la'`

**Argument**  
Ein Wert, der einem Befehl übergeben wird.  
Beispiel: In `cp datei.txt backup/` sind `datei.txt` und `backup/` Argumente.

---

## B

**Bash**  
Bourne Again Shell – die Standard-Shell auf den meisten Linux-Systemen. Benannt nach der älteren Bourne Shell (sh).

**Built-in**  
Ein Befehl, der direkt in die Shell eingebaut ist (nicht ein separates Programm).  
Beispiele: `cd`, `echo`, `read`

---

## C

**CLI (Command Line Interface)**  
Die textbasierte Schnittstelle zur Interaktion mit dem Computer.

**Command Substitution**  
Ersetzt einen Befehl durch seine Ausgabe.  
Syntax: `$(befehl)` oder `` `befehl` ``

**Cron**  
Ein Dienst zur zeitgesteuerten Ausführung von Befehlen.

---

## D

**Daemon**  
Ein Hintergrundprozess, der ohne Benutzerinteraktion läuft.

**Directory (Verzeichnis)**  
Ein Ordner im Dateisystem, der Dateien und weitere Verzeichnisse enthält.

---

## E

**Environment Variable (Umgebungsvariable)**  
Eine Variable, die für alle Prozesse in einer Shell-Sitzung verfügbar ist.  
Beispiel: `$PATH`, `$HOME`, `$USER`

**Exit Code (Exit Status)**  
Ein numerischer Wert, den ein Befehl zurückgibt. `0` bedeutet Erfolg, andere Werte zeigen Fehler an.

---

## F

**Flag**  
Siehe Option.

**Fork**  
Das Erstellen eines Kindprozesses als Kopie des Elternprozesses.

---

## G

**Glob (Globbing)**  
Musterexpansion mit Wildcards wie `*` und `?`.  
Beispiel: `*.txt` wird zu allen `.txt`-Dateien expandiert.

**GUI (Graphical User Interface)**  
Die grafische Benutzeroberfläche mit Fenstern, Buttons, Maus.

---

## H

**Hard Link**  
Ein zusätzlicher Name für dieselben Daten auf der Festplatte.

**Here Document (Heredoc)**  
Eine Methode, mehrzeiligen Text an einen Befehl zu übergeben.  
Syntax: `<< EOF ... EOF`

**Home Directory**  
Das persönliche Verzeichnis eines Benutzers. Zugreifbar mit `~` oder `$HOME`.

---

## I

**Interactive Shell**  
Eine Shell, die auf Benutzereingaben wartet (im Gegensatz zu einer, die ein Skript ausführt).

---

## J

**Job**  
Ein Prozess oder eine Gruppe von Prozessen, die von der Shell verwaltet werden.

---

## K

**Kernel**  
Der Kern des Betriebssystems, der Hardware und Software verbindet.

---

## L

**Login Shell**  
Die erste Shell, die beim Einloggen gestartet wird.

---

## M

**Man Page (Manual Page)**  
Die eingebaute Dokumentation für Befehle. Aufruf mit `man befehl`.

---

## O

**Option (Flag)**  
Ein Modifikator für einen Befehl, meist mit `-` oder `--` eingeleitet.  
Beispiel: `-l` in `ls -l`

---

## P

**Path (Pfad)**  
Die Adresse einer Datei oder eines Verzeichnisses im Dateisystem.

**PATH**  
Eine Umgebungsvariable, die die Verzeichnisse enthält, in denen nach ausführbaren Programmen gesucht wird.

**Pipe (Pipe)**  
Verbindet die Ausgabe eines Befehls mit der Eingabe eines anderen.  
Symbol: `|`

**PID (Process ID)**  
Eine eindeutige Nummer für jeden laufenden Prozess.

**Prompt**  
Die Eingabeaufforderung, die auf Befehle wartet.  
Beispiel: `user@host:~$`

---

## R

**Redirect (Umleitung)**  
Lenkt Ein- oder Ausgabe um.  
Symbole: `>`, `>>`, `<`, `2>`

**Regex (Regular Expression)**  
Ein Muster zur Beschreibung von Textstrukturen.

**Relative Path (Relativer Pfad)**  
Ein Pfad, der vom aktuellen Verzeichnis ausgeht.  
Beispiel: `../dokumente/brief.txt`

**Root**  
1. Das Wurzelverzeichnis `/`
2. Der Superuser mit allen Rechten

---

## S

**Shebang**  
Die erste Zeile eines Skripts, die den Interpreter angibt.  
Beispiel: `#!/bin/bash`

**Shell**  
Ein Programm, das Befehle interpretiert und an das Betriebssystem weitergibt.

**stdin (Standard Input)**  
Der Standard-Eingabekanal (normalerweise die Tastatur).

**stdout (Standard Output)**  
Der Standard-Ausgabekanal (normalerweise das Terminal).

**stderr (Standard Error)**  
Der Kanal für Fehlermeldungen.

**Subshell**  
Eine Shell, die innerhalb einer anderen Shell läuft.

**Symbolic Link (Symlink)**  
Ein Verweis auf eine andere Datei oder ein Verzeichnis.

---

## T

**Tab Completion**  
Automatisches Vervollständigen von Befehlen und Pfaden mit der Tab-Taste.

**Terminal**  
Das Programm, das die Shell-Oberfläche bereitstellt.

---

## U

**Unix**  
Eine Familie von Betriebssystemen, zu der Linux und macOS gehören.

---

## V

**Variable**  
Ein benannter Speicherplatz für Werte.  
Setzen: `name=wert`  
Lesen: `$name`

---

## W

**Wildcard**  
Platzhalter für Dateinamen.  
`*` = beliebig viele Zeichen  
`?` = genau ein Zeichen

**Working Directory**  
Das aktuelle Verzeichnis, in dem du dich befindest.

---

## Z

**Zombie Process**  
Ein beendeter Prozess, dessen Exit-Status noch nicht vom Elternprozess abgeholt wurde.
