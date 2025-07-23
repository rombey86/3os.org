---
title: ADB Spickzettel
description: Spickzettel für ADB. ADB, Android Debug Bridge, ist ein Befehlszeilen-Dienstprogramm für Android. ADB kann Ihr Gerät über USB von einem Computer aus steuern, Dateien hin- und herkopieren, Apps installieren und deinstallieren, Shell-Befehle ausführen.
template: comments.html
tags: [android, adb, cheat-sheet]
---

# Android ADB Spickzettel

ADB, Android Debug Bridge, ist ein Befehlszeilen-Dienstprogramm, das im Android SDK von Google enthalten ist. ADB kann Ihr Gerät über USB von einem Computer aus steuern, Dateien hin- und herkopieren, Apps installieren und deinstallieren, Shell-Befehle ausführen und vieles mehr. ADB ist ein leistungsstarkes Werkzeug, das zur Steuerung Ihres Android-Geräts von einem Computer aus verwendet werden kann. Im Folgenden sind einige der gängigsten Befehle aufgeführt, die Sie mit ADB verwenden können, und deren Verwendung. Weitere Informationen zu ADB und seiner Verwendung finden Sie auf der [offiziellen Website][adb-docs-url]{target=\_blank}.

## Häufige ADB-Befehle

### Eine Datei in den Download-Ordner des Android-Geräts verschieben

```bash
adb push example.apk /mnt/sdcard/Download/
```

### Listet alle installierten Pakete auf und gibt die vollständigen Pfade an

```bash
adb shell pm list packages -f
```

### Zieht eine Datei vom Android-Gerät

```bash
adb pull /mnt/sdcard/Download/example.apk
```

---

### APK vom Host auf Android-Gerät installieren

```bash
adb shell install example.apk
```

### APK aus dem Android-Gerätespeicher installieren

```bash
adb shell install /mnt/sdcard/Download/example.apk
```

---

### Netzwerk-Proxy einstellen

```bash
adb shell settings put global http_proxy <address>:<port>
```

Netzwerk-Proxy deaktivieren

```bash
adb shell settings put global http_proxy :0
```

## ADB Grundlagen-Befehle

| Befehl | Beschreibung |
| ----------------------------------- | ------------------------------------------- |
| **adb devices** | **Listet verbundene Geräte auf** |
| **adb connect 192.168.2.1** | **Verbindet sich mit dem ADB-Gerät über das Netzwerk** |
| adb root | Startet adbd mit Root-Berechtigungen neu |
| adb start-server | Startet den adb-Server |
| adb kill-server | Beendet den adb-Server |
| **adb reboot** | **Startet das Gerät neu** |
| **adb devices -l** | **Liste der Geräte nach Produkt/Modell** |
| **adb -s `<deviceName> <command>`** | **Leitet Befehl an bestimmtes Gerät um** |
| adb –d `<command>` | Leitet Befehl nur an das angeschlossene USB-Gerät weiter |
| adb –e `<command>` | Leitet Befehl nur an den angeschlossenen Emulator weiter |

## Protokolle

| Befehl | Beschreibung |
| -------------------------------------------- | ------------------- |
| **adb logcat `[options] [filter] [filter]`** | **Geräteprotokoll anzeigen** |
| adb bugreport | Fehlerberichte ausgeben |

## Berechtigungen

| Befehl | Beschreibung |
| -------------------------------- | ---------------------------------- |
| adb shell permissions groups | Definitionen der Berechtigungsgruppen auflisten |
| adb shell list permissions -g -r | Details der Berechtigungen auflisten |

## Paketinstallation

| Befehl | Beschreibung |
| ------------------------------ | ------------------------------- |
| **adb shell install** `<apk>` | **App installieren** |
| **adb shell install `<path>`** | **App vom Telefonpfad installieren** |
| adb shell install -r `<path>` | App vom Telefonpfad installieren |
| adb shell uninstall `<name>` | App entfernen |

## Pfade

| Befehl | Beschreibung |
| ----------------------------------------- | ----------------------------------------- |
| /data/data/`<package name>`/databases | App-Datenbanken |
| /data/data/`<package name>`/shared_prefs/ | Gemeinsame Präferenzen |
| /mnt/sdcard/Download/ | Download-Ordner |
| /data/app | Vom Benutzer installierte APKs |
| /system/app | Vorinstallierte APK-Dateien |
| /mmt/asec | Verschlüsselte Apps (App2SD) |
| /mmt/emmc | Interne SD-Karte |
| /mmt/adcard | Externe/Interne SD-Karte |
| /mmt/adcard/external_sd | Externe SD-Karte |
| -------                                   | -----------                               |
| adb shell ls | Verzeichnisinhalte auflisten |
| adb shell ls -s | Größe jeder Datei ausgeben |
| adb shell ls -R | Unterverzeichnisse rekursiv auflisten |
| **adb shell pm path `<package name>`** | **Vollständigen Pfad eines Pakets abrufen** |
| **adb shell pm list packages -f** | **Listet alle Pakete und vollständigen Pfade auf** |

## Dateioperationen

| Befehl | Beschreibung |
| ------------------------------- | -------------------------------- |
| **adb push `<local> <remote>`** | **Copy file/dir to device**      |
| **adb pull `<remote> <local>`** | **Copy file/dir from device**    |
| run-as `<package>` cat `<file>` | Auf private Paketdateien zugreifen |

## Telefoninformationen

| Command                                           | Description                            |
| ------------------------------------------------- | -------------------------------------- |
| adb get-statе | Gerätestatus ausgeben |
| adb get-serialno | Seriennummer abrufen |
| adb shell dumpsys iphonesybinfo | IMEI abrufen |
| adb shell netstat | TCP-Konnektivität auflisten |
| adb shell pwd | Aktuelles Arbeitsverzeichnis ausgeben |
| adb shell dumpsys battery | Batteriestatus |
| adb shell pm list features | Telefonfunktionen auflisten |
| adb shell service list | Alle Dienste auflisten |
| adb shell dumpsys activity `<package>/<activity>` | Aktivitätsinformationen |
| adb shell ps | Prozessstatus ausgeben |
| adb shell wm size | Zeigt die aktuelle Bildschirmauflösung an |

## Paketinformationen

| Befehl | Beschreibung |
| ---------------------------------- | --------------------------------- |
| adb shell list packages | Paketnamen auflisten |
| adb shell list packages -r | Listet Paketnamen + Pfad zu APKs auf |
| adb shell list packages -3 | Listet Drittanbieter-Paketnamen auf |
| adb shell list packages -s | Listet nur Systempakete auf |
| adb shell list packages -u | Listet Paketnamen + deinstallierte auf |
| adb shell dumpsys package packages | Listet Informationen zu allen Apps auf |
| adb shell dump `<name>` | Listet Informationen zu einem Paket auf |
| adb shell path `<package>` | Pfad zur APK-Datei |

## Gerätebezogene Befehle

| Befehl | Beschreibung |
| ------------------------------------------------------------ | ---------------------------------------- |
| adb reboot recovery | Gerät in den Wiederherstellungsmodus neu starten |
| adb reboot fastboot | Gerät in den Fastboot-Modus neu starten |
| adb shell screencap -p "/path/to/screenshot.png"             | Capture screenshot                       |
| adb shell screenrecord "/path/to/record.mp4"                 | Record device screen                     |
| adb backup -apk -all -f backup.ab | Einstellungen und Apps sichern |
| adb backup -apk -shared -all -f backup.ab | Einstellungen, Apps und freigegebenen Speicher sichern |
| adb backup -apk -nosystem -all -f backup.ab | Nur Nicht-System-Apps sichern |
| adb restore backup.ab | Eine frühere Sicherung wiederherstellen |
| -------                                                      | -----------                              |
| adb shell am start -a android.intent.action.VIEW -d URL | URL öffnen |
| adb shell am start -t image/\* -a android.intent.action.VIEW | Opens gallery                            |

<!-- appendices -->

[adb-docs-url]: https://developer.android.com/studio/command-line/adb.html 'Android Debug Bridge'

<!-- end appendices -->
