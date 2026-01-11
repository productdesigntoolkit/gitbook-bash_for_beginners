# Was ist Bash?

> Lerne die Geschichte und Bedeutung der Bash-Shell kennen und verstehe, warum sie auch heute noch unverzichtbar ist.

---

## Lernziele

Nach diesem Kapitel wirst du:

- Verstehen, was eine Shell ist und wozu sie dient
- Die Geschichte der Bash kennen
- Wissen, warum die Kommandozeile auch heute relevant ist
- Die Unterschiede zwischen GUI und CLI verstehen
- Ein Terminal auf deinem System öffnen können

---

## Einleitung

Bevor es grafische Benutzeroberflächen gab, war die Kommandozeile die einzige Möglichkeit, mit einem Computer zu kommunizieren. Heute, Jahrzehnte später, ist sie immer noch das mächtigste Werkzeug für viele Aufgaben. Professionelle Entwickler, Systemadministratoren und DevOps-Ingenieure verbringen einen Grossteil ihrer Zeit im Terminal.

Aber was genau ist die Bash? Und warum solltest du dich im Jahr 2025 noch damit beschäftigen?

---

## Was ist eine Shell?

Eine **Shell** ist ein Programm, das zwischen dir und dem Betriebssystem vermittelt. Du gibst Befehle ein, die Shell interpretiert sie und leitet sie an das System weiter. Das Ergebnis wird dir angezeigt.

Stell dir die Shell wie einen Übersetzer vor: Du sprichst in einer Sprache (Bash-Befehle), und die Shell übersetzt das in eine Sprache, die der Computer versteht.

Es gibt verschiedene Shells:

| Shell | Beschreibung |
|-------|--------------|
| **Bash** | Bourne Again Shell – Standard auf Linux und älteren macOS |
| **Zsh** | Z Shell – Standard auf neueren macOS, Bash-kompatibel |
| **Fish** | Friendly Interactive Shell – modern, aber weniger verbreitet |
| **PowerShell** | Microsofts Shell für Windows |

Dieses Buch konzentriert sich auf **Bash**, da sie der De-facto-Standard ist und auf praktisch jedem Unix-System verfügbar.

---

## Die Geschichte der Bash

Die Bash wurde 1989 von Brian Fox für das GNU-Projekt geschrieben. Der Name steht für **Bourne Again Shell** – ein Wortspiel, das auf die ältere Bourne Shell (sh) von Stephen Bourne anspielt.

**Wichtige Meilensteine:**

- **1971:** Die erste Unix-Shell (Thompson Shell)
- **1979:** Bourne Shell (sh) wird Standard
- **1989:** Bash wird veröffentlicht
- **2004:** Bash 3.0 mit vielen Verbesserungen
- **2019:** Bash 5.0 – die aktuelle Major-Version

Bash ist Open Source und wird aktiv weiterentwickelt. Sie ist auf praktisch jedem Linux-System vorinstalliert und war bis 2019 auch Standard auf macOS.

---

## CLI vs. GUI: Warum Kommandozeile?

Die grafische Benutzeroberfläche (GUI) ist intuitiv – du siehst Buttons, klickst darauf, und etwas passiert. Warum also die Mühe mit der Kommandozeile (CLI)?

### Vorteile der Kommandozeile

**Geschwindigkeit:** Ein erfahrener Nutzer tippt `rm *.tmp` schneller als er 50 Dateien einzeln anklicken könnte.

**Automatisierung:** Du kannst Befehle in Skripten speichern und wiederholt ausführen. Versuche das mal mit Mausklicks.

**Reproduzierbarkeit:** Ein Befehl ist dokumentiert. "Klick da, dann da, dann da" ist es nicht.

**Remote-Zugriff:** Server haben oft keine grafische Oberfläche. Die Kommandozeile funktioniert über SSH von überall.

**Ressourcen:** Die CLI braucht weniger Speicher und Rechenleistung als eine GUI.

{% hint style="info" %}
**Merke:** Die GUI ist wie ein Aufzug mit vordefinierten Stockwerken. Die CLI ist wie eine Treppe – du kommst überall hin, auch in den Keller.
{% endhint %}

---

## Dein erstes Terminal öffnen

Je nach Betriebssystem öffnest du ein Terminal unterschiedlich:

### macOS

1. Öffne Spotlight mit `Cmd + Space`
2. Tippe "Terminal"
3. Drücke Enter

Oder: Finder → Programme → Dienstprogramme → Terminal

### Linux (Ubuntu/Debian)

1. Drücke `Ctrl + Alt + T`

Oder: Aktivitäten → "Terminal" suchen

### Windows (mit WSL)

1. Installiere WSL: `wsl --install` in PowerShell (als Admin)
2. Starte Ubuntu aus dem Startmenü
3. Erstelle einen Benutzernamen und Passwort

{% hint style="warning" %}
**Windows-Nutzer:** Die normale Windows-Eingabeaufforderung (cmd) und PowerShell sind keine Bash. Du brauchst WSL (Windows Subsystem for Linux) für echte Bash-Unterstützung.
{% endhint %}

---

## Der Prompt

Wenn du ein Terminal öffnest, siehst du etwas wie:

```bash
ralph@macbook:~$
```

Das ist der **Prompt**. Er zeigt dir:

- `ralph` – Dein Benutzername
- `macbook` – Der Computername
- `~` – Das aktuelle Verzeichnis (~ = Home-Verzeichnis)
- `$` – Du bist ein normaler Benutzer (# = Root/Admin)

Der Prompt wartet auf deine Eingabe. Tippe etwas ein und drücke Enter.

---

## Dein erster Befehl

Tippe folgenden Befehl und drücke Enter:

```bash
echo "Hallo, Bash!"
```

Du solltest sehen:

```
Hallo, Bash!
```

Herzlichen Glückwunsch – du hast soeben deinen ersten Bash-Befehl ausgeführt!

`echo` ist ein Befehl, der Text ausgibt. Wir werden ihn noch oft verwenden.

---

## Praktische Übung

{% hint style="success" %}
**Übung: Erste Schritte im Terminal**

1. Öffne ein Terminal auf deinem System
2. Finde heraus, welche Shell du verwendest:
   ```bash
   echo $SHELL
   ```
3. Zeige das aktuelle Datum an:
   ```bash
   date
   ```
4. Zeige deinen Benutzernamen an:
   ```bash
   whoami
   ```

**Erwartetes Ergebnis:** Du siehst den Pfad zu deiner Shell, das aktuelle Datum und deinen Benutzernamen.
{% endhint %}

---

## Zusammenfassung

In diesem Kapitel hast du gelernt:

- Eine Shell ist ein Programm, das Befehle interpretiert und an das System weitergibt
- Bash steht für "Bourne Again Shell" und ist seit 1989 der Standard auf Unix-Systemen
- Die Kommandozeile ist schneller, automatisierbar und funktioniert auch remote
- Du kannst mit `echo` Text ausgeben und mit `date`, `whoami` erste Systeminformationen abrufen

---

## Weiterführende Ressourcen

- [GNU Bash Manual](https://www.gnu.org/software/bash/manual/) – Die offizielle Dokumentation
- [Bash Guide for Beginners](https://tldp.org/LDP/Bash-Beginners-Guide/html/) – Ausführliches Tutorial
- [ExplainShell](https://explainshell.com/) – Erklärt Bash-Befehle visuell

---

**Nächstes Kapitel:** [Kernkonzepte](./02-grundlagen.md)
