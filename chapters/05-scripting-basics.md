# Scripting Basics

> Lerne, Bash-Skripte zu schreiben und repetitive Aufgaben zu automatisieren.

---

## Lernziele

Nach diesem Kapitel wirst du:

- Ein einfaches Bash-Skript schreiben und ausführen können
- Variablen verwenden können
- Benutzereingaben verarbeiten
- Bedingte Anweisungen (if/else) nutzen
- Schleifen (for, while) einsetzen
- Ein- und Ausgabeumleitung verstehen

---

## Einleitung

Bisher hast du einzelne Befehle eingegeben. Aber was, wenn du dieselben 10 Befehle jeden Tag ausführen musst? Hier kommen Skripte ins Spiel. Ein Bash-Skript ist eine Textdatei mit einer Sequenz von Befehlen. Einmal geschrieben, kannst du es immer wieder ausführen.

---

## Dein erstes Skript

Erstelle eine Datei namens `hallo.sh`:

```bash
#!/bin/bash

# Mein erstes Bash-Skript
echo "Hallo, Welt!"
echo "Heute ist $(date)"
echo "Du bist eingeloggt als: $USER"
```

### Der Shebang

Die erste Zeile `#!/bin/bash` ist der **Shebang**. Er teilt dem System mit, welcher Interpreter das Skript ausführen soll.

### Skript ausführbar machen und starten

```bash
chmod +x hallo.sh        # Ausführbar machen
./hallo.sh               # Ausführen
```

Alternativ ohne chmod:

```bash
bash hallo.sh            # Mit Bash direkt ausführen
```

{% hint style="info" %}
**Merke:** Das `./` vor dem Skriptnamen ist nötig, weil das aktuelle Verzeichnis normalerweise nicht im Suchpfad ist.
{% endhint %}

---

## Variablen

Variablen speichern Werte für spätere Verwendung.

### Variablen setzen und lesen

```bash
#!/bin/bash

# Variable setzen (KEIN Leerzeichen um das =!)
name="Ralph"
zahl=42

# Variable lesen (mit $)
echo "Hallo, $name"
echo "Die Antwort ist $zahl"

# Variablen in Text einbetten (mit geschweiften Klammern)
echo "Datei: ${name}_backup.txt"
```

{% hint style="warning" %}
**Wichtig:** Keine Leerzeichen um das `=` bei Zuweisungen! `name = "Ralph"` funktioniert NICHT.
{% endhint %}

### Spezielle Variablen

| Variable | Bedeutung |
|----------|-----------|
| `$0` | Name des Skripts |
| `$1, $2, ...` | Argumente (erstes, zweites, ...) |
| `$#` | Anzahl der Argumente |
| `$@` | Alle Argumente als Liste |
| `$?` | Exit-Status des letzten Befehls |
| `$$` | Prozess-ID des Skripts |

**Beispiel mit Argumenten:**

```bash
#!/bin/bash
echo "Skript: $0"
echo "Erstes Argument: $1"
echo "Zweites Argument: $2"
echo "Anzahl Argumente: $#"
```

Aufruf:
```bash
./skript.sh hallo welt
```

### Befehlsausgabe in Variable speichern

```bash
#!/bin/bash

# Mit $(...) - empfohlen
aktuelle_zeit=$(date +%H:%M)
anzahl_dateien=$(ls | wc -l)

echo "Es ist $aktuelle_zeit Uhr"
echo "Hier sind $anzahl_dateien Dateien"
```

---

## Benutzereingaben

### read – Eingabe vom Benutzer

```bash
#!/bin/bash

echo "Wie heisst du?"
read name
echo "Hallo, $name!"

# Mit Prompt in einer Zeile
read -p "Dein Alter: " alter
echo "Du bist $alter Jahre alt"

# Stille Eingabe (für Passwörter)
read -s -p "Passwort: " passwort
echo ""  # Neue Zeile nach stiller Eingabe
```

---

## Bedingte Anweisungen

### if / else

```bash
#!/bin/bash

read -p "Gib eine Zahl ein: " zahl

if [ $zahl -gt 10 ]; then
    echo "Die Zahl ist grösser als 10"
elif [ $zahl -eq 10 ]; then
    echo "Die Zahl ist genau 10"
else
    echo "Die Zahl ist kleiner als 10"
fi
```

### Vergleichsoperatoren für Zahlen

| Operator | Bedeutung |
|----------|-----------|
| `-eq` | Equal (gleich) |
| `-ne` | Not equal (ungleich) |
| `-gt` | Greater than (grösser) |
| `-lt` | Less than (kleiner) |
| `-ge` | Greater or equal |
| `-le` | Less or equal |

### Vergleichsoperatoren für Strings

| Operator | Bedeutung |
|----------|-----------|
| `=` | Gleich |
| `!=` | Ungleich |
| `-z` | Leer (zero length) |
| `-n` | Nicht leer |

```bash
if [ "$name" = "Ralph" ]; then
    echo "Hallo Chef!"
fi

if [ -z "$variable" ]; then
    echo "Variable ist leer"
fi
```

### Dateiprüfungen

| Operator | Bedeutung |
|----------|-----------|
| `-e` | Existiert |
| `-f` | Ist eine reguläre Datei |
| `-d` | Ist ein Verzeichnis |
| `-r` | Ist lesbar |
| `-w` | Ist schreibbar |
| `-x` | Ist ausführbar |

```bash
#!/bin/bash

if [ -f "config.txt" ]; then
    echo "Config gefunden"
else
    echo "Config nicht gefunden, erstelle..."
    touch config.txt
fi
```

---

## Schleifen

### for-Schleife

```bash
#!/bin/bash

# Über Liste iterieren
for name in Alice Bob Charlie; do
    echo "Hallo, $name"
done

# Über Dateien iterieren
for datei in *.txt; do
    echo "Verarbeite: $datei"
done

# Über Zahlenbereich
for i in {1..5}; do
    echo "Durchlauf $i"
done

# C-Style for-Schleife
for ((i=0; i<5; i++)); do
    echo "Index: $i"
done
```

### while-Schleife

```bash
#!/bin/bash

zaehler=1
while [ $zaehler -le 5 ]; do
    echo "Durchlauf $zaehler"
    ((zaehler++))
done

# Datei zeilenweise lesen
while read zeile; do
    echo "Zeile: $zeile"
done < eingabe.txt
```

---

## Ein- und Ausgabeumleitung

### Standardkanäle

| Kanal | Nummer | Bedeutung |
|-------|--------|-----------|
| stdin | 0 | Standardeingabe |
| stdout | 1 | Standardausgabe |
| stderr | 2 | Fehlerausgabe |

### Umleitung

```bash
# Ausgabe in Datei (überschreiben)
echo "Hallo" > datei.txt

# Ausgabe an Datei anhängen
echo "Welt" >> datei.txt

# Eingabe aus Datei
wc -l < datei.txt

# Fehler umleiten
ls nicht_da 2> fehler.txt

# Alles umleiten
befehl > ausgabe.txt 2>&1

# Ausgabe verwerfen
befehl > /dev/null 2>&1
```

### Pipes

Mit Pipes (`|`) verbindest du Befehle – die Ausgabe eines Befehls wird zur Eingabe des nächsten:

```bash
# Zeilen zählen, die "error" enthalten
cat log.txt | grep "error" | wc -l

# Sortieren und Duplikate entfernen
cat namen.txt | sort | uniq

# Prozesse finden
ps aux | grep "firefox"
```

---

## Praktische Übung

{% hint style="success" %}
**Übung: Backup-Skript erstellen**

Erstelle ein Skript `backup.sh`, das:
1. Ein Backup-Verzeichnis mit Datum erstellt
2. Alle `.txt` Dateien dorthin kopiert
3. Eine Zusammenfassung ausgibt

```bash
#!/bin/bash

# Backup-Verzeichnis mit Datum
backup_dir="backup_$(date +%Y%m%d_%H%M%S)"

# Verzeichnis erstellen
mkdir -p "$backup_dir"

# Dateien zählen
anzahl=$(ls *.txt 2>/dev/null | wc -l)

if [ $anzahl -eq 0 ]; then
    echo "Keine .txt Dateien gefunden!"
    rmdir "$backup_dir"
    exit 1
fi

# Dateien kopieren
cp *.txt "$backup_dir/"

echo "Backup erstellt: $backup_dir"
echo "Gesicherte Dateien: $anzahl"
ls -la "$backup_dir"
```

**Teste es:**
```bash
touch test1.txt test2.txt test3.txt
chmod +x backup.sh
./backup.sh
```

{% endhint %}

---

## Zusammenfassung

In diesem Kapitel hast du gelernt:

- Skripte beginnen mit `#!/bin/bash` und werden mit `chmod +x` ausführbar
- Variablen werden mit `=` gesetzt (ohne Leerzeichen) und mit `$` gelesen
- `read` nimmt Benutzereingaben entgegen
- `if/elif/else/fi` ermöglichen bedingte Ausführung
- `for` und `while` ermöglichen Schleifen
- `>`, `>>`, `<` und `|` steuern Ein- und Ausgabe

---

## Weiterführende Ressourcen

- [Bash Scripting Tutorial](https://ryanstutorials.net/bash-scripting-tutorial/) – Umfassendes Tutorial
- [ShellCheck](https://www.shellcheck.net/) – Findet Fehler in deinen Skripten

---

**Nächstes Kapitel:** [Übungen & Projekte](./06-praxis.md)
