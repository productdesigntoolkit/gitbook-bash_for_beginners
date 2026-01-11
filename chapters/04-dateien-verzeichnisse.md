# Dateien & Verzeichnisse

> Vertiefe deine Kenntnisse in der Dateiverwaltung mit Suche, Berechtigungen und fortgeschrittenen Techniken.

---

## Lernziele

Nach diesem Kapitel wirst du:

- Dateien im System finden können (find, locate)
- Textmuster in Dateien suchen (grep)
- Dateiberechtigungen verstehen und ändern (chmod)
- Dateibesitz ändern (chown)
- Mit Links arbeiten (ln)

---

## Einleitung

Im vorherigen Kapitel hast du die Grundlagen der Dateiverwaltung gelernt. Jetzt gehen wir tiefer. Du lernst, wie du Dateien findest, Inhalte durchsuchst und Berechtigungen verwaltest. Diese Fähigkeiten sind essentiell für jeden, der ernsthaft mit Linux oder macOS arbeitet.

---

## Dateien finden

### find – Mächtige Suche

`find` durchsucht das Dateisystem nach verschiedenen Kriterien:

```bash
find /pfad -name "dateiname"
```

**Häufige Anwendungen:**

```bash
# Nach Name suchen
find . -name "*.txt"                    # Alle .txt im aktuellen Verzeichnis
find /home -name "config*"              # Alle Dateien die mit config beginnen

# Nach Typ suchen
find . -type f                          # Nur Dateien
find . -type d                          # Nur Verzeichnisse

# Nach Grösse suchen
find . -size +10M                       # Grösser als 10 MB
find . -size -1k                        # Kleiner als 1 KB

# Nach Zeit suchen
find . -mtime -7                        # Geändert in letzten 7 Tagen
find . -mmin -60                        # Geändert in letzten 60 Minuten

# Kombinationen
find . -name "*.log" -size +1M          # Grosse Log-Dateien
```

### Aktionen mit find

```bash
# Gefundene Dateien löschen
find . -name "*.tmp" -delete

# Befehl auf gefundene Dateien anwenden
find . -name "*.txt" -exec cat {} \;
```

{% hint style="warning" %}
**Achtung:** `-delete` löscht ohne Nachfrage! Teste erst mit `-print` (Standard), bevor du löschst.
{% endhint %}

### locate – Schnelle Suche in Datenbank

```bash
locate dateiname
```

`locate` ist schneller als `find`, da es eine Datenbank nutzt. Diese muss aber aktuell sein:

```bash
sudo updatedb                           # Datenbank aktualisieren
```

---

## In Dateien suchen: grep

`grep` sucht nach Textmustern in Dateien:

```bash
grep "suchbegriff" datei.txt
```

**Häufige Optionen:**

```bash
grep "fehler" log.txt                   # Einfache Suche
grep -i "fehler" log.txt                # Ignoriert Gross/Klein
grep -r "TODO" .                        # Rekursiv in allen Dateien
grep -n "fehler" log.txt                # Zeigt Zeilennummern
grep -c "fehler" log.txt                # Zählt Treffer
grep -v "debug" log.txt                 # Zeilen OHNE "debug"
grep -l "fehler" *.log                  # Nur Dateinamen mit Treffern
```

### Reguläre Ausdrücke mit grep

```bash
grep "^Start" datei.txt                 # Zeilen die mit "Start" beginnen
grep "Ende$" datei.txt                  # Zeilen die mit "Ende" enden
grep "error\|warning" log.txt           # "error" ODER "warning"
grep -E "[0-9]{4}" datei.txt            # Vierstellige Zahlen
```

{% hint style="info" %}
**Tipp:** Nutze `grep -E` (extended regex) für komplexere Muster.
{% endhint %}

---

## Dateiberechtigungen

Linux-Dateisysteme haben ein ausgefeiltes Berechtigungssystem.

### Berechtigungen verstehen

```bash
ls -l datei.txt
-rw-r--r-- 1 ralph staff 1024 Jan 10 14:30 datei.txt
```

Die ersten 10 Zeichen zeigen die Berechtigungen:

```
-rw-r--r--
│├─┤├─┤├─┤
│ │  │  └── Others (alle anderen)
│ │  └───── Group (Gruppenmitglieder)
│ └──────── User (Besitzer)
└────────── Typ (- = Datei, d = Verzeichnis)
```

| Zeichen | Bedeutung |
|---------|-----------|
| `r` | Read – Lesen |
| `w` | Write – Schreiben |
| `x` | Execute – Ausführen |
| `-` | Keine Berechtigung |

### chmod – Berechtigungen ändern

**Symbolische Notation:**

```bash
chmod u+x script.sh                     # User: Ausführen hinzufügen
chmod g-w datei.txt                     # Group: Schreiben entfernen
chmod o=r datei.txt                     # Others: Nur Lesen setzen
chmod a+r datei.txt                     # All: Lesen für alle
```

**Numerische Notation:**

| Wert | Bedeutung |
|------|-----------|
| 4 | Read (r) |
| 2 | Write (w) |
| 1 | Execute (x) |

```bash
chmod 755 script.sh                     # rwxr-xr-x (User: alles, Rest: lesen+ausführen)
chmod 644 datei.txt                     # rw-r--r-- (User: lesen+schreiben, Rest: nur lesen)
chmod 700 privat/                       # rwx------ (nur User hat Zugriff)
```

{% hint style="success" %}
**Merkhilfe:** 
- 7 = 4+2+1 = rwx
- 6 = 4+2 = rw-
- 5 = 4+1 = r-x
- 4 = r--
{% endhint %}

### chown – Besitzer ändern

```bash
sudo chown ralph datei.txt              # Ändert Besitzer
sudo chown ralph:staff datei.txt        # Ändert Besitzer und Gruppe
sudo chown -R ralph:staff ordner/       # Rekursiv
```

---

## Symbolische und Hard Links

Links sind Verweise auf Dateien.

### Symbolische Links (Soft Links)

Wie ein "Shortcut" – zeigt auf eine andere Datei:

```bash
ln -s /pfad/zum/original link-name
```

```bash
ln -s ~/dokumente/wichtig.txt ~/desktop/shortcut.txt
```

- Kann auf Verzeichnisse zeigen
- Kann über Dateisysteme hinweg funktionieren
- Wird ungültig, wenn das Ziel gelöscht wird

### Hard Links

Zeigt auf dieselben Daten wie das Original:

```bash
ln original.txt hardlink.txt
```

- Nur für Dateien (nicht Verzeichnisse)
- Nur im selben Dateisystem
- Bleibt gültig, auch wenn Original "gelöscht" wird

{% hint style="info" %}
**In der Praxis:** Symbolische Links sind häufiger. Hard Links sind eher für spezielle Anwendungen.
{% endhint %}

---

## Nützliche Befehle

### du – Speicherverbrauch anzeigen

```bash
du -h datei.txt                         # Grösse einer Datei
du -sh ordner/                          # Gesamtgrösse eines Ordners
du -h --max-depth=1 .                   # Grössen im aktuellen Verzeichnis
```

### df – Freier Speicherplatz

```bash
df -h                                   # Alle Dateisysteme
df -h /home                             # Bestimmtes Dateisystem
```

### file – Dateityp ermitteln

```bash
file unbekannt.bin                      # Zeigt den tatsächlichen Typ
```

### stat – Detaillierte Dateiinfos

```bash
stat datei.txt                          # Alle Metadaten
```

---

## Praktische Übung

{% hint style="success" %}
**Übung: Dateien finden und verwalten**

1. Finde alle `.md` Dateien in deinem Home-Verzeichnis:
   ```bash
   find ~ -name "*.md" 2>/dev/null
   ```
   (Das `2>/dev/null` unterdrückt Fehlermeldungen für nicht zugängliche Verzeichnisse)

2. Suche nach "TODO" in allen Textdateien:
   ```bash
   grep -ri "todo" ~/dokumente 2>/dev/null
   ```

3. Erstelle ein Skript und mache es ausführbar:
   ```bash
   echo '#!/bin/bash' > ~/test-script.sh
   echo 'echo "Hallo von meinem Skript!"' >> ~/test-script.sh
   chmod +x ~/test-script.sh
   ~/test-script.sh
   ```

4. Erstelle einen symbolischen Link:
   ```bash
   ln -s ~/test-script.sh ~/mein-link.sh
   ls -la ~/mein-link.sh
   ```

5. Aufräumen:
   ```bash
   rm ~/test-script.sh ~/mein-link.sh
   ```

**Erwartetes Ergebnis:** Du hast Dateien gefunden, nach Inhalten gesucht, Berechtigungen gesetzt und mit Links gearbeitet.
{% endhint %}

---

## Zusammenfassung

In diesem Kapitel hast du gelernt:

- `find` durchsucht das Dateisystem nach Namen, Typ, Grösse oder Zeit
- `grep` sucht Textmuster in Dateien
- Berechtigungen bestehen aus r(ead), w(rite), x(ecute) für User, Group, Others
- `chmod` ändert Berechtigungen (755, 644 sind häufige Werte)
- `ln -s` erstellt symbolische Links

---

## Weiterführende Ressourcen

- [Linux Permissions Explained](https://linuxize.com/post/understanding-linux-file-permissions/) – Tiefere Erklärung
- [Grep Tutorial](https://www.gnu.org/software/grep/manual/grep.html) – Offizielle Dokumentation

---

**Nächstes Kapitel:** [Scripting Basics](./05-scripting-basics.md)
