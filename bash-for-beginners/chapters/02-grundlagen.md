# Kernkonzepte

> Verstehe die fundamentalen Konzepte der Bash, die Grundlage für alles Weitere sind.

---

## Lernziele

Nach diesem Kapitel wirst du:

- Die Anatomie eines Bash-Befehls verstehen
- Mit Optionen und Argumenten arbeiten können
- Die Hilfe-Systeme (man, --help) nutzen können
- Pfade verstehen (absolut vs. relativ)
- Mit der Befehlshistorie arbeiten

---

## Einleitung

Bevor wir in die Praxis einsteigen, müssen wir einige Grundkonzepte verstehen. Diese Konzepte ziehen sich durch die gesamte Bash-Welt und werden dir immer wieder begegnen. Nimm dir Zeit für dieses Kapitel – es ist das Fundament für alles Weitere.

---

## Anatomie eines Befehls

Jeder Bash-Befehl folgt einem Muster:

```
befehl [optionen] [argumente]
```

**Beispiel:**

```bash
ls -la /home
```

| Teil | Bedeutung |
|------|-----------|
| `ls` | Der Befehl (list – zeigt Verzeichnisinhalte) |
| `-la` | Optionen (-l = langes Format, -a = alle Dateien) |
| `/home` | Argument (das Verzeichnis, das angezeigt werden soll) |

### Befehle

Der Befehl selbst ist ein Programm, das ausgeführt wird. Er steht immer am Anfang.

### Optionen (Flags)

Optionen modifizieren das Verhalten eines Befehls. Sie beginnen meist mit `-` oder `--`:

- **Kurze Optionen:** `-l`, `-a`, `-h` (ein Buchstabe)
- **Lange Optionen:** `--all`, `--human-readable` (ausgeschrieben)
- **Kombiniert:** `-la` ist dasselbe wie `-l -a`

### Argumente

Argumente sind die Daten, auf die der Befehl angewendet wird – oft Dateien oder Verzeichnisse.

{% hint style="info" %}
**Tipp:** Nicht jeder Befehl braucht Optionen oder Argumente. `pwd` funktioniert ohne alles.
{% endhint %}

---

## Hilfe finden

Du musst nicht alle Befehle auswendig kennen. Es gibt eingebaute Hilfe-Systeme.

### Die --help Option

Fast jeder Befehl unterstützt `--help`:

```bash
ls --help
```

Dies zeigt eine kurze Übersicht der verfügbaren Optionen.

### Man Pages

Für ausführliche Dokumentation gibt es die **Manual Pages**:

```bash
man ls
```

Navigation in Man Pages:

| Taste | Aktion |
|-------|--------|
| `Space` | Seite nach unten |
| `b` | Seite nach oben |
| `/suchbegriff` | Suchen |
| `n` | Nächstes Suchergebnis |
| `q` | Beenden |

### TLDR Pages

Für schnelle Beispiele gibt es `tldr` (muss installiert werden):

```bash
tldr ls
```

Dies zeigt praktische Beispiele statt trockener Dokumentation.

---

## Pfade verstehen

Ein **Pfad** ist die Adresse einer Datei oder eines Verzeichnisses im Dateisystem.

### Absolute Pfade

Ein absoluter Pfad beginnt beim Wurzelverzeichnis `/`:

```bash
/home/ralph/dokumente/brief.txt
```

Er beschreibt den kompletten Weg von der Wurzel zur Datei.

### Relative Pfade

Ein relativer Pfad geht vom aktuellen Verzeichnis aus:

```bash
dokumente/brief.txt
```

Wenn du dich in `/home/ralph` befindest, zeigt dieser Pfad auf dieselbe Datei.

### Spezielle Verzeichnisse

| Symbol | Bedeutung |
|--------|-----------|
| `/` | Wurzelverzeichnis (Root) |
| `~` | Home-Verzeichnis des aktuellen Nutzers |
| `.` | Aktuelles Verzeichnis |
| `..` | Übergeordnetes Verzeichnis |

**Beispiele:**

```bash
cd ~           # Gehe ins Home-Verzeichnis
cd ..          # Gehe ein Verzeichnis nach oben
cd ../..       # Gehe zwei Verzeichnisse nach oben
cd ./scripts   # Gehe in scripts (relativ)
```

---

## Die Befehlshistorie

Die Bash merkt sich deine eingegebenen Befehle. Das spart viel Tipparbeit.

### Navigation mit Pfeiltasten

- `↑` – Vorheriger Befehl
- `↓` – Nächster Befehl

### Historie anzeigen

```bash
history
```

Zeigt die letzten Befehle mit Nummern.

### Befehle wiederholen

```bash
!42         # Führt Befehl Nr. 42 aus der Historie aus
!!          # Wiederholt den letzten Befehl
!ls         # Führt den letzten Befehl aus, der mit "ls" begann
```

### In der Historie suchen

Drücke `Ctrl + R` und tippe einen Suchbegriff. Die Bash zeigt passende Befehle aus der Historie.

{% hint style="success" %}
**Profi-Tipp:** `Ctrl + R` ist einer der mächtigsten Shortcuts. Nutze ihn oft!
{% endhint %}

---

## Tab-Vervollständigung

Die Tab-Taste ist dein bester Freund. Sie vervollständigt:

- Befehle
- Dateinamen
- Verzeichnisnamen
- Optionen (bei vielen Programmen)

**Beispiel:**

```bash
cd /ho[TAB]        # wird zu: cd /home/
cd /home/ra[TAB]   # wird zu: cd /home/ralph/
```

Wenn es mehrere Möglichkeiten gibt, drücke Tab zweimal, um alle anzuzeigen.

---

## Sonderzeichen und Escaping

Einige Zeichen haben in der Bash spezielle Bedeutung:

| Zeichen | Bedeutung |
|---------|-----------|
| `*` | Wildcard – steht für beliebig viele Zeichen |
| `?` | Wildcard – steht für genau ein Zeichen |
| `$` | Variablen-Präfix |
| `"` | Doppelte Anführungszeichen (Variablen werden ersetzt) |
| `'` | Einfache Anführungszeichen (alles literal) |
| `\` | Escape-Zeichen |

**Beispiele:**

```bash
echo "Hallo $USER"       # Gibt: Hallo ralph
echo 'Hallo $USER'       # Gibt: Hallo $USER
echo Hallo\ Welt         # Gibt: Hallo Welt (Leerzeichen escaped)
```

{% hint style="warning" %}
**Achtung:** Dateinamen mit Leerzeichen oder Sonderzeichen müssen in Anführungszeichen oder mit Backslash escaped werden.
{% endhint %}

---

## Praktische Übung

{% hint style="success" %}
**Übung: Konzepte anwenden**

1. Zeige alle Dateien (auch versteckte) in deinem Home-Verzeichnis:
   ```bash
   ls -la ~
   ```

2. Öffne die Man Page für den `cp` Befehl:
   ```bash
   man cp
   ```
   Finde heraus, was die Option `-r` macht. Beende mit `q`.

3. Nutze die Tab-Vervollständigung:
   ```bash
   cd /u[TAB][TAB]
   ```
   Was wird angezeigt?

4. Finde einen alten Befehl mit `Ctrl + R`:
   - Drücke `Ctrl + R`
   - Tippe "ls"
   - Drücke Enter, um den gefundenen Befehl auszuführen

**Erwartetes Ergebnis:** Du verstehst, wie Optionen funktionieren, kannst Hilfe finden und effizient navigieren.
{% endhint %}

---

## Zusammenfassung

In diesem Kapitel hast du gelernt:

- Befehle bestehen aus Befehl, Optionen und Argumenten
- `--help` und `man` liefern Dokumentation
- Absolute Pfade beginnen mit `/`, relative gehen vom aktuellen Verzeichnis aus
- Die Befehlshistorie (`↑`, `history`, `Ctrl+R`) spart Zeit
- Tab-Vervollständigung ist essentiell für effizientes Arbeiten

---

## Weiterführende Ressourcen

- [Bash Reference Manual](https://www.gnu.org/software/bash/manual/bash.html) – Offizielle Referenz
- [ShellCheck](https://www.shellcheck.net/) – Online-Tool zur Syntax-Prüfung

---

**Nächstes Kapitel:** [Erste Schritte](./03-erste-schritte.md)
