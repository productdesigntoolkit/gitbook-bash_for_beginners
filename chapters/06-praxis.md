# Übungen & Projekte

> Wende dein Wissen in praktischen Projekten an und festige deine Bash-Kenntnisse.

---

## Lernziele

Nach diesem Kapitel wirst du:

- Mehrere praktische Skripte selbst geschrieben haben
- Typische Alltagsaufgaben automatisieren können
- Debugging-Techniken kennen
- Best Practices für Bash-Skripte anwenden

---

## Einleitung

Theorie ist wichtig, aber Übung macht den Meister. In diesem Kapitel findest du praktische Projekte, die du selbstständig umsetzen solltest. Versuche zuerst, die Aufgaben ohne Blick auf die Lösung zu lösen.

---

## Projekt 1: Datei-Organizer

**Aufgabe:** Erstelle ein Skript, das Dateien nach Typ in Unterordner sortiert.

### Anforderungen

- Erstellt Ordner für verschiedene Dateitypen (bilder, dokumente, musik, etc.)
- Verschiebt Dateien basierend auf der Endung
- Gibt eine Zusammenfassung aus

### Lösung

```bash
#!/bin/bash

# Datei-Organizer
# Sortiert Dateien nach Typ in Unterordner

echo "=== Datei-Organizer ==="

# Ordner erstellen
mkdir -p bilder dokumente musik videos archiv sonstiges

# Zähler initialisieren
moved=0

# Dateien durchgehen (nur im aktuellen Verzeichnis, keine Ordner)
for datei in *; do
    # Überspringe Verzeichnisse
    if [ -d "$datei" ]; then
        continue
    fi
    
    # Dateiendung extrahieren (lowercase)
    ext="${datei##*.}"
    ext=$(echo "$ext" | tr '[:upper:]' '[:lower:]')
    
    # Zielordner bestimmen
    case "$ext" in
        jpg|jpeg|png|gif|bmp|svg)
            ziel="bilder"
            ;;
        pdf|doc|docx|txt|odt|md)
            ziel="dokumente"
            ;;
        mp3|wav|flac|aac|ogg)
            ziel="musik"
            ;;
        mp4|mkv|avi|mov|wmv)
            ziel="videos"
            ;;
        zip|tar|gz|7z|rar)
            ziel="archiv"
            ;;
        *)
            ziel="sonstiges"
            ;;
    esac
    
    # Datei verschieben
    mv "$datei" "$ziel/" 2>/dev/null
    if [ $? -eq 0 ]; then
        echo "  $datei → $ziel/"
        ((moved++))
    fi
done

echo ""
echo "=== Zusammenfassung ==="
echo "Verschobene Dateien: $moved"

# Leere Ordner entfernen
for ordner in bilder dokumente musik videos archiv sonstiges; do
    if [ -z "$(ls -A $ordner 2>/dev/null)" ]; then
        rmdir "$ordner" 2>/dev/null
    else
        anzahl=$(ls -1 "$ordner" | wc -l)
        echo "$ordner: $anzahl Dateien"
    fi
done
```

---

## Projekt 2: System-Info-Skript

**Aufgabe:** Erstelle ein Skript, das wichtige Systeminformationen übersichtlich anzeigt.

### Anforderungen

- Zeigt Hostname, OS, Kernel-Version
- Zeigt CPU, RAM, Festplattennutzung
- Formatiert die Ausgabe übersichtlich

### Lösung

```bash
#!/bin/bash

# System-Info-Skript

echo "╔════════════════════════════════════════╗"
echo "║          SYSTEM INFORMATION            ║"
echo "╚════════════════════════════════════════╝"
echo ""

# Betriebssystem-Info
echo "▶ SYSTEM"
echo "  Hostname:    $(hostname)"
echo "  Benutzer:    $USER"
echo "  Kernel:      $(uname -r)"
echo "  Architektur: $(uname -m)"
echo ""

# CPU-Info
echo "▶ CPU"
if [ -f /proc/cpuinfo ]; then
    cpu_model=$(grep "model name" /proc/cpuinfo | head -1 | cut -d':' -f2 | xargs)
    cpu_cores=$(grep -c "processor" /proc/cpuinfo)
    echo "  Modell:      $cpu_model"
    echo "  Kerne:       $cpu_cores"
elif command -v sysctl &> /dev/null; then
    # macOS
    cpu_model=$(sysctl -n machdep.cpu.brand_string)
    cpu_cores=$(sysctl -n hw.ncpu)
    echo "  Modell:      $cpu_model"
    echo "  Kerne:       $cpu_cores"
fi
echo ""

# Speicher-Info
echo "▶ SPEICHER"
if command -v free &> /dev/null; then
    # Linux
    mem_total=$(free -h | awk '/^Mem:/ {print $2}')
    mem_used=$(free -h | awk '/^Mem:/ {print $3}')
    mem_free=$(free -h | awk '/^Mem:/ {print $4}')
    echo "  Gesamt:      $mem_total"
    echo "  Verwendet:   $mem_used"
    echo "  Frei:        $mem_free"
else
    # macOS
    mem_total=$(sysctl -n hw.memsize | awk '{print $1/1024/1024/1024 " GB"}')
    echo "  Gesamt:      $mem_total"
fi
echo ""

# Festplatten-Info
echo "▶ FESTPLATTE"
df -h / | awk 'NR==2 {printf "  Gesamt:      %s\n  Verwendet:   %s (%s)\n  Frei:        %s\n", $2, $3, $5, $4}'
echo ""

# Netzwerk-Info
echo "▶ NETZWERK"
if command -v ip &> /dev/null; then
    ip_addr=$(ip route get 1 2>/dev/null | awk '{print $7; exit}')
else
    ip_addr=$(ipconfig getifaddr en0 2>/dev/null || echo "N/A")
fi
echo "  IP-Adresse:  $ip_addr"
echo ""

# Uptime
echo "▶ LAUFZEIT"
echo "  Uptime:      $(uptime | awk -F'up ' '{print $2}' | awk -F',' '{print $1}')"
echo ""

echo "════════════════════════════════════════"
echo "  Generiert am: $(date '+%Y-%m-%d %H:%M:%S')"
echo "════════════════════════════════════════"
```

---

## Projekt 3: Log-Analyzer

**Aufgabe:** Analysiere eine Log-Datei und erstelle eine Zusammenfassung.

### Anforderungen

- Zählt verschiedene Log-Level (ERROR, WARNING, INFO)
- Findet die häufigsten Fehlermeldungen
- Erstellt einen Bericht

### Lösung

```bash
#!/bin/bash

# Log-Analyzer
# Analysiert Log-Dateien und erstellt Statistiken

if [ -z "$1" ]; then
    echo "Verwendung: $0 <logdatei>"
    exit 1
fi

logfile="$1"

if [ ! -f "$logfile" ]; then
    echo "Fehler: Datei '$logfile' nicht gefunden!"
    exit 1
fi

echo "=== Log-Analyse: $logfile ==="
echo ""

# Grundlegende Statistiken
total_lines=$(wc -l < "$logfile")
echo "▶ Übersicht"
echo "  Gesamtzeilen: $total_lines"
echo "  Dateigrösse:  $(du -h "$logfile" | cut -f1)"
echo ""

# Log-Level zählen
echo "▶ Log-Level Verteilung"
for level in ERROR WARNING INFO DEBUG; do
    count=$(grep -ci "$level" "$logfile" 2>/dev/null || echo "0")
    printf "  %-10s %d\n" "$level:" "$count"
done
echo ""

# Top 5 Fehler
errors=$(grep -i "error" "$logfile" | sort | uniq -c | sort -rn | head -5)
if [ -n "$errors" ]; then
    echo "▶ Top 5 häufigste Fehler"
    echo "$errors" | while read count msg; do
        printf "  [%d] %s\n" "$count" "${msg:0:60}"
    done
    echo ""
fi

# Zeitraum (falls Zeitstempel vorhanden)
first_date=$(head -1 "$logfile" | grep -oE '[0-9]{4}-[0-9]{2}-[0-9]{2}' | head -1)
last_date=$(tail -1 "$logfile" | grep -oE '[0-9]{4}-[0-9]{2}-[0-9]{2}' | head -1)
if [ -n "$first_date" ] && [ -n "$last_date" ]; then
    echo "▶ Zeitraum"
    echo "  Von: $first_date"
    echo "  Bis: $last_date"
    echo ""
fi

echo "=== Analyse abgeschlossen ==="
```

---

## Debugging-Techniken

### Debug-Modus aktivieren

```bash
#!/bin/bash
set -x  # Gibt jeden Befehl vor Ausführung aus

# oder beim Aufruf:
bash -x skript.sh
```

### Strengen Modus aktivieren

```bash
#!/bin/bash
set -e  # Beendet bei Fehlern
set -u  # Fehler bei undeklarierten Variablen
set -o pipefail  # Fehler in Pipes erkennen

# Kurzform:
set -euo pipefail
```

### Eigene Debug-Funktion

```bash
#!/bin/bash

DEBUG=true

debug() {
    if [ "$DEBUG" = true ]; then
        echo "[DEBUG] $1" >&2
    fi
}

debug "Starte Verarbeitung..."
# ... dein Code ...
debug "Verarbeitung abgeschlossen"
```

---

## Best Practices

### 1. Immer Shebang verwenden

```bash
#!/bin/bash
# oder für maximale Kompatibilität:
#!/usr/bin/env bash
```

### 2. Variablen in Anführungszeichen

```bash
# Schlecht
cp $datei $ziel

# Gut
cp "$datei" "$ziel"
```

### 3. Sinnvolle Exit-Codes

```bash
if [ ! -f "$config" ]; then
    echo "Fehler: Config nicht gefunden" >&2
    exit 1
fi
```

### 4. Funktionen nutzen

```bash
#!/bin/bash

log_info() {
    echo "[INFO] $1"
}

log_error() {
    echo "[ERROR] $1" >&2
}

main() {
    log_info "Starte..."
    # Hauptlogik hier
    log_info "Fertig"
}

main "$@"
```

### 5. Hilfe-Option einbauen

```bash
#!/bin/bash

show_help() {
    cat << EOF
Verwendung: $(basename "$0") [OPTIONEN] <datei>

Optionen:
  -h, --help     Diese Hilfe anzeigen
  -v, --verbose  Ausführliche Ausgabe

Beispiel:
  $(basename "$0") -v eingabe.txt
EOF
}

if [ "$1" = "-h" ] || [ "$1" = "--help" ]; then
    show_help
    exit 0
fi
```

---

## Praktische Übung

{% hint style="success" %}
**Übung: Eigenes Tool bauen**

Erstelle ein Skript `countdown.sh`, das:
1. Eine Anzahl Sekunden als Argument nimmt
2. Einen Countdown anzeigt
3. Am Ende eine Benachrichtigung ausgibt

**Bonus:** Füge eine Option für eine eigene Nachricht hinzu.

**Hinweis:** Nutze `sleep 1` für die Pause und `\r` für das Überschreiben der Zeile.

```bash
#!/bin/bash

# Dein Code hier...
```
{% endhint %}

---

## Zusammenfassung

In diesem Kapitel hast du:

- Drei praktische Projekte umgesetzt (Organizer, System-Info, Log-Analyzer)
- Debugging-Techniken kennengelernt (`set -x`, `set -e`)
- Best Practices für produktionsreife Skripte gelernt

---

## Weiterführende Ressourcen

- [Google Shell Style Guide](https://google.github.io/styleguide/shellguide.html) – Best Practices von Google
- [Bash Pitfalls](https://mywiki.wooledge.org/BashPitfalls) – Häufige Fehler vermeiden

---

**Nächstes Kapitel:** [Nächste Schritte](./07-naechste-schritte.md)
