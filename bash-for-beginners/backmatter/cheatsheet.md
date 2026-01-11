# Bash Cheatsheet

> Quick Reference für die wichtigsten Bash-Befehle und Konzepte

---

## Navigation

| Befehl | Beschreibung |
|--------|--------------|
| `pwd` | Aktuelles Verzeichnis anzeigen |
| `cd /pfad` | Verzeichnis wechseln |
| `cd ~` | Ins Home-Verzeichnis |
| `cd ..` | Ein Verzeichnis nach oben |
| `cd -` | Zum vorherigen Verzeichnis |

---

## Dateien & Verzeichnisse

| Befehl | Beschreibung |
|--------|--------------|
| `ls` | Verzeichnisinhalt anzeigen |
| `ls -la` | Alle Dateien mit Details |
| `ls -lh` | Menschenlesbare Grössen |
| `touch datei` | Datei erstellen |
| `mkdir ordner` | Verzeichnis erstellen |
| `mkdir -p a/b/c` | Verschachtelte Verzeichnisse |
| `cp quelle ziel` | Kopieren |
| `cp -r ordner ziel` | Verzeichnis kopieren |
| `mv quelle ziel` | Verschieben/Umbenennen |
| `rm datei` | Datei löschen |
| `rm -r ordner` | Verzeichnis löschen |
| `rm -rf ordner` | Ohne Nachfrage löschen ⚠️ |

---

## Dateiinhalte anzeigen

| Befehl | Beschreibung |
|--------|--------------|
| `cat datei` | Gesamte Datei ausgeben |
| `less datei` | Seitenweise anzeigen |
| `head datei` | Erste 10 Zeilen |
| `head -n 20 datei` | Erste 20 Zeilen |
| `tail datei` | Letzte 10 Zeilen |
| `tail -f datei` | Neuen Zeilen folgen |

---

## Suchen

| Befehl | Beschreibung |
|--------|--------------|
| `find . -name "*.txt"` | Dateien nach Name finden |
| `find . -type d` | Nur Verzeichnisse |
| `find . -size +10M` | Grösser als 10 MB |
| `grep "text" datei` | Text in Datei suchen |
| `grep -r "text" .` | Rekursiv suchen |
| `grep -i "text" datei` | Gross/Klein ignorieren |
| `grep -n "text" datei` | Mit Zeilennummern |

---

## Berechtigungen

| Befehl | Beschreibung |
|--------|--------------|
| `chmod +x datei` | Ausführbar machen |
| `chmod 755 datei` | rwxr-xr-x |
| `chmod 644 datei` | rw-r--r-- |
| `chown user datei` | Besitzer ändern |
| `chown user:gruppe datei` | Besitzer und Gruppe |

**Berechtigungswerte:**
- 4 = read (r)
- 2 = write (w)
- 1 = execute (x)
- 7 = rwx, 6 = rw-, 5 = r-x, 4 = r--

---

## Umleitung & Pipes

| Symbol | Beschreibung |
|--------|--------------|
| `>` | Ausgabe in Datei (überschreiben) |
| `>>` | Ausgabe an Datei anhängen |
| `<` | Eingabe aus Datei |
| `2>` | Fehler umleiten |
| `2>&1` | Fehler zu stdout |
| `\|` | Pipe: Ausgabe → Eingabe |
| `/dev/null` | Ausgabe verwerfen |

**Beispiele:**
```bash
echo "text" > datei.txt
cat log.txt | grep error | wc -l
befehl > out.txt 2>&1
```

---

## Variablen

```bash
# Setzen (KEIN Leerzeichen!)
name="Wert"

# Lesen
echo $name
echo "${name}_suffix"

# Befehlsausgabe
datum=$(date +%Y-%m-%d)
```

**Spezielle Variablen:**
| Variable | Bedeutung |
|----------|-----------|
| `$0` | Skriptname |
| `$1, $2` | Argumente |
| `$#` | Anzahl Argumente |
| `$@` | Alle Argumente |
| `$?` | Exit-Code |
| `$$` | Prozess-ID |

---

## Kontrollstrukturen

**if/else:**
```bash
if [ bedingung ]; then
    # ...
elif [ andere ]; then
    # ...
else
    # ...
fi
```

**for-Schleife:**
```bash
for i in 1 2 3; do
    echo $i
done

for datei in *.txt; do
    echo $datei
done
```

**while-Schleife:**
```bash
while [ bedingung ]; do
    # ...
done
```

---

## Vergleichsoperatoren

**Zahlen:**
| Operator | Bedeutung |
|----------|-----------|
| `-eq` | gleich |
| `-ne` | ungleich |
| `-gt` | grösser |
| `-lt` | kleiner |
| `-ge` | grösser/gleich |
| `-le` | kleiner/gleich |

**Strings:**
| Operator | Bedeutung |
|----------|-----------|
| `=` | gleich |
| `!=` | ungleich |
| `-z` | leer |
| `-n` | nicht leer |

**Dateien:**
| Operator | Bedeutung |
|----------|-----------|
| `-e` | existiert |
| `-f` | ist Datei |
| `-d` | ist Verzeichnis |
| `-r` | lesbar |
| `-w` | schreibbar |
| `-x` | ausführbar |

---

## Tastenkürzel

| Kürzel | Aktion |
|--------|--------|
| `Tab` | Autovervollständigung |
| `↑` / `↓` | Historie navigieren |
| `Ctrl+R` | Historie durchsuchen |
| `Ctrl+C` | Befehl abbrechen |
| `Ctrl+D` | Shell beenden / EOF |
| `Ctrl+L` | Bildschirm leeren |
| `Ctrl+A` | Zeilenanfang |
| `Ctrl+E` | Zeilenende |
| `Ctrl+U` | Zeile löschen |
| `Ctrl+W` | Wort löschen |

---

## Nützliche Einzeiler

```bash
# Alle .log Dateien löschen
find . -name "*.log" -delete

# Grösste Dateien finden
du -ah . | sort -rh | head -10

# Dateien nach Endung zählen
find . -type f | sed 's/.*\.//' | sort | uniq -c | sort -rn

# Leere Verzeichnisse löschen
find . -type d -empty -delete

# Text in allen Dateien ersetzen
find . -name "*.txt" -exec sed -i 's/alt/neu/g' {} \;
```

---

## Skript-Template

```bash
#!/bin/bash
set -euo pipefail

# Beschreibung des Skripts

show_help() {
    echo "Verwendung: $(basename "$0") [optionen]"
}

main() {
    if [ "$#" -eq 0 ]; then
        show_help
        exit 1
    fi
    
    # Hauptlogik hier
}

main "$@"
```

---

*Bash for Beginners – Version 1.0*  
*Autor: Ralph Hutter*
