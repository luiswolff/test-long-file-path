# Test langer Dateipfade

[english](./README.md)

<!-- TABLE OF CONTENTS -->
<details>
  <summary>Inhaltsverzeichnis</summary>

* [Über das Projekt](#über-das-projekt)
* [Vorgehen](#vorgehen)
  1. [Voraussetzungen](#voraussetzungen)
  2. [Windows konfigurieren](#windows-konfigurieren)
  3. [Git konfigurieren](#git-konfigurieren)
* [Beschränkungen](#beschränkungen)
* [Links](#links)
  
</details>

## Über das Projekt

Dieses Projekt beschreibt, wie Sie lange Dateipfade mit Git und Windows handhaben können.
Dies ist wichtig, da das Windows-Betriebssystem standardmäßig keine Pfadnamen mit mehr als 260 Zeichen zulässt.
Es ist jedoch möglich, das Betriebssystem so zu konfigurieren, dass es eine eingeschränkte Arbeit mit überlangen Dateibäumen erlaubt.

Dieses Projekt selbst ist ein Beispiel dafür, denn der relative Pfad zur enthaltenen Datei `es.txt` hat 265 Zeichen.
Ohne Konfiguration ist es daher nicht möglich, dieses Projekt auf einem Windows-Betriebssystem auszuchecken.

[Zum Anfang](#test-langer-dateipfade)

## Vorgehen

Dieser Abschnitt zeigt, wie ein Git-Projekt mit einer Pfandlänge von mehr als 260 Zeichen ausgecheckt werden kann.

### Voraussetzungen

* Die gezeigten Schritte wurden in einer Windows 10 Enterprise Umgebung getestet.
* Der getestete Git-Client war Git für Windows.
* Administrative Rechte für den lokalen Computer sind erforderlich.

### Windows konfigurieren

1. Drücken Sie die Windows-Taste und geben Sie "gpedit" ein.
Dies öffnet das Fenster __Gruppenrichtlinie bearbeiten__.
2. Gehen Sie zu __Administrative Vorlagen > System > Dateisystem__ und öffnen Sie __Lange Win32-Pfade aktivieren__.
3. Wählen Sie die Option __Aktiviert__ und drücken Sie __OK__.
4. Drücken Sie nun erneut die Windows-Taste und geben Sie "cmd" ein. Dadurch wird die Windows-Eingabeaufforderung geöffnet.
5. Geben Sie die folgenden Befehle ein, um die geänderten Gruppenrichtlinien anzuwenden

```
> gpupdate /target:computer /force
> gpupdate /target:user /force
```

Jetzt können Sie eine Datei mit einem Pfad, der länger als 260 Zeichen ist, mit der __Eingabeaufforderung__ erstellen.

### Git konfigurieren

Nachdem Sie Windows so konfiguriert haben, dass es lange Dateipfade unterstützt, müssen Sie dies auch mit Ihrer lokalen Git-Installation tun.

1. Drücken Sie die Windows-Taste und geben Sie `git bash` ein. Wenn Sie die Git Bash öffnen, wählen Sie die Option __Als Administrator ausführen__.
2. Geben Sie den folgenden Befehl ein

```
$ git config --system core.longpaths true
```

Jetzt können Sie Git-Projekte auschecken, die eine tiefe Dateistruktur haben und zu Pfaden führen, die länger als 260 Zeichen auf Ihrem lokalen System sind.

[Zum Anfang](#test-langer-dateipfade)

## Beschränkungen

Das Problem der Dateipfad länge kann mit den obigen Schritten nicht komplett gelöst werden.
Soweit ich informiert bin hängt dieses Problem mit einer älteren Windows API zusammen, weshalb nicht alle Programme mit Dateien in einer so tiefen Ordnerstruktur umgehen können. 

Beispiele für Programme, die keine langen Dateipfade unterstützen:
* Windows Explorer (Unterstützt nur das Anzeigen)
* Notepad++

Beispiele für Programme, die lange Dateipfade unterstützen:
* Visual Studio Code
* Notepad (Windows Boardmittel)

[Zum Anfang](#test-langer-dateipfade)

## Links

Diesen Artikel über das generelle Problem in Windows finde ich persönlich sehr hilfreich.
 * [https://helpdeskgeek.com/how-to/how-to-fix-filename-is-too-long-issue-in-windows/]

Hier ist noch ein Stackoverflow Artikel über das Problem in Git for Windows
 * [https://stackoverflow.com/questions/22575662/filename-too-long-in-git-for-windows]

 [Zum Anfang](#test-langer-dateipfade)