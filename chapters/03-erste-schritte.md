# Erste Schritte

> Lerne die wichtigsten Befehle für die tägliche Navigation und Arbeit im Dateisystem.

---

## Lernziele

Nach diesem Kapitel wirst du:

- Dich im Dateisystem bewegen können (cd, pwd)
- Verzeichnisinhalte anzeigen können (ls)
- Dateien und Verzeichnisse erstellen (touch, mkdir)
- Dateien und Verzeichnisse löschen (rm, rmdir)
- Dateien kopieren und verschieben (cp, mv)

---

## Einleitung

Jetzt wird es praktisch. In diesem Kapitel lernst du die Befehle, die du jeden Tag brauchst. Diese Handvoll Kommandos bildet das Fundament deiner Bash-Kenntnisse. Übe sie, bis sie in Fleisch und Blut übergehen.

---

## Navigation: Wo bin ich?

### pwd – Print Working Directory

Zeigt das aktuelle Verzeichnis:

```bash
pwd
```

Ausgabe:
```
/home/ralph
```

### cd – Change Directory

Wechselt das Verzeichnis:

```bash
cd /var/log      # Wechselt zu /var/log
cd ~             # Wechselt ins Home-Verzeichnis
cd ..            # Wechselt ins übergeordnete Verzeichnis
cd -             # Wechselt zum vorherigen Verzeichnis
cd               # Ohne Argument: wechselt ins Home-Verzeichnis
```

{% hint style="success" %}
**Tipp:** `cd -` ist super praktisch, um zwischen zwei Verzeichnissen hin und her zu wechseln.
{% endhint %}

---

## Verzeichnisinhalt anzeigen: ls

`ls` (list) zeigt den Inhalt eines Verzeichnisses:

```bash
ls               # Aktuelles Verzeichnis
ls /var          # Bestimmtes Verzeichnis
ls -l            # Detaillierte Ansicht (long)
ls -a            # Alle Dateien inkl. versteckte
ls -la           # Kombination: alle Details
ls -lh           # Menschenlesbare Grössen (human-readable)
```

### Ausgabe verstehen

```
-rw-r--r-- 1 ralph staff  4.2K Jan 10 14:30 dokument.txt
drwxr-xr-x 2 ralph staff   64B Jan 10 14:25 bilder
```

| Teil | Bedeutung |
|------|-----------|
| `-rw-r--r--` | Berechtigungen |
| `1` | Anzahl Links |
| `ralph` | Besitzer |
| `staff` | Gruppe |
| `4.2K` | Dateigrösse |
| `Jan 10 14:30` | Änderungsdatum |
| `dokument.txt` | Dateiname |

Das erste Zeichen zeigt den Typ:
- `-` = normale Datei
- `d` = Verzeichnis (directory)
- `l` = symbolischer Link

---

## Dateien und Verzeichnisse erstellen

### touch – Datei erstellen oder Zeitstempel aktualisieren

```bash
touch neue-datei.txt           # Erstellt leere Datei
touch datei1.txt datei2.txt    # Mehrere Dateien
```

Wenn die Datei existiert, wird nur der Zeitstempel aktualisiert.

### mkdir – Verzeichnis erstellen

```bash
mkdir neuer-ordner             # Erstellt Verzeichnis
mkdir -p pfad/unter/ordner     # Erstellt alle Zwischenverzeichnisse
```

{% hint style="warning" %}
**Wichtig:** `-p` ist essentiell, wenn Elternverzeichnisse noch nicht existieren.
{% endhint %}

---

## Dateien und Verzeichnisse löschen

### rm – Dateien löschen

```bash
rm datei.txt                   # Löscht eine Datei
rm datei1.txt datei2.txt       # Löscht mehrere Dateien
rm -i datei.txt                # Fragt vor dem Löschen
rm -r ordner                   # Löscht Verzeichnis rekursiv
rm -rf ordner                  # Löscht ohne Nachfrage (GEFÄHRLICH!)
```

{% hint style="danger" %}
**WARNUNG:** `rm` löscht unwiderruflich! Es gibt keinen Papierkorb. Besonders `rm -rf` kann bei falscher Anwendung dein System zerstören. Prüfe immer zweimal, bevor du Enter drückst.
{% endhint %}

### rmdir – Leere Verzeichnisse löschen

```bash
rmdir leerer-ordner            # Löscht nur wenn leer
```

`rmdir` ist sicherer als `rm -r`, funktioniert aber nur bei leeren Verzeichnissen.

---

## Dateien kopieren und verschieben

### cp – Kopieren

```bash
cp quelle.txt ziel.txt              # Kopiert Datei
cp quelle.txt /zielverzeichnis/     # Kopiert ins Verzeichnis
cp -r ordner /zielverzeichnis/      # Kopiert Verzeichnis rekursiv
cp -i datei.txt ziel.txt            # Fragt vor Überschreiben
```

### mv – Verschieben / Umbenennen

```bash
mv alte.txt neue.txt                # Umbenennen
mv datei.txt /anderer/ort/          # Verschieben
mv datei.txt /anderer/ort/neu.txt   # Verschieben und umbenennen
```

{% hint style="info" %}
**Merke:** `mv` ist sowohl zum Verschieben als auch zum Umbenennen da. Wenn Quelle und Ziel im selben Verzeichnis sind, wird umbenannt.
{% endhint %}

---

## Dateiinhalte anzeigen

### cat – Gesamte Datei ausgeben

```bash
cat datei.txt                  # Zeigt Inhalt
cat datei1.txt datei2.txt      # Zeigt beide Dateien
```

### less – Datei seitenweise anzeigen

```bash
less grosse-datei.txt
```

Navigation wie in Man Pages (Space, b, q).

### head / tail – Anfang oder Ende anzeigen

```bash
head datei.txt                 # Erste 10 Zeilen
head -n 20 datei.txt           # Erste 20 Zeilen
tail datei.txt                 # Letzte 10 Zeilen
tail -f logfile.txt            # Folgt neuen Zeilen (für Logs!)
```

{% hint style="success" %}
**Profi-Tipp:** `tail -f` ist unverzichtbar, um Log-Dateien in Echtzeit zu beobachten.
{% endhint %}

---

## Wildcards in Aktion

Wildcards machen Befehle mächtiger:

```bash
ls *.txt                       # Alle .txt Dateien
rm bild?.jpg                   # bild1.jpg, bild2.jpg, etc.
cp *.md /backup/               # Alle Markdown-Dateien kopieren
```

| Wildcard | Bedeutung |
|----------|-----------|
| `*` | Beliebig viele Zeichen |
| `?` | Genau ein Zeichen |
| `[abc]` | Eines der Zeichen a, b oder c |
| `[0-9]` | Eine Ziffer |

---

## Praktische Übung

{% hint style="success" %}
**Übung: Dateiverwaltung**

1. Erstelle eine Übungsstruktur:
   ```bash
   mkdir -p ~/bash-uebung/dokumente
   mkdir -p ~/bash-uebung/bilder
   cd ~/bash-uebung
   ```

2. Erstelle einige Dateien:
   ```bash
   touch dokumente/brief.txt
   touch dokumente/notiz.txt
   touch bilder/foto1.jpg
   touch bilder/foto2.jpg
   ```

3. Zeige die Struktur an:
   ```bash
   ls -la
   ls -la dokumente
   ```

4. Kopiere eine Datei:
   ```bash
   cp dokumente/brief.txt dokumente/brief-kopie.txt
   ```

5. Verschiebe eine Datei:
   ```bash
   mv dokumente/notiz.txt .
   ```

6. Lösche die Übungsumgebung:
   ```bash
   cd ~
   rm -r bash-uebung
   ```

**Erwartetes Ergebnis:** Du hast Verzeichnisse erstellt, Dateien angelegt, kopiert, verschoben und wieder gelöscht.
{% endhint %}

---

## Zusammenfassung

In diesem Kapitel hast du gelernt:

- `pwd` zeigt das aktuelle Verzeichnis, `cd` wechselt es
- `ls` zeigt Inhalte, mit `-la` auch versteckte Dateien und Details
- `touch` erstellt Dateien, `mkdir` erstellt Verzeichnisse
- `rm` löscht Dateien, `rm -r` löscht Verzeichnisse (Vorsicht!)
- `cp` kopiert, `mv` verschiebt oder benennt um
- `cat`, `less`, `head`, `tail` zeigen Dateiinhalte

---

## Weiterführende Ressourcen

- [Linux File System Hierarchy](https://refspecs.linuxfoundation.org/FHS_3.0/fhs/index.html) – Wo liegt was im System?
- [Linuxize File Commands](https://linuxize.com/tags/file-commands/) – Tutorials zu Dateibefehlen

---

**Nächstes Kapitel:** [Dateien & Verzeichnisse](./04-dateien-verzeichnisse.md)
