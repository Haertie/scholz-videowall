# Changelog – Scholz Videowall

Alle wesentlichen Änderungen werden in dieser Datei dokumentiert.  
Format basiert auf [Keep a Changelog](https://keepachangelog.com/de/1.0.0/).  
Versionierung nach [Semantic Versioning](https://semver.org/lang/de/).

---

## [1.0.0] – 2026-03-06

Erste offizielle Version. Vollständig funktionsfähige Videowall-Anwendung
als Single-Page-App ohne Backend.

### Hinzugefügt
- MJPEG-Livestreaming direkt im Browser (Mobotix, Axis, Hikvision, Custom)
- Multi-Kamera-Dashboard mit 4, 6, 9 und 12 Kamera-Slots
- Flexible Layouts (1×1, 2×1, 2×2, 1+3, 3×2, 2×3, 3×3, 4×3, 3×4)
- Ziehbare Trennlinien zwischen Kameras (Spalten & Zeilen)
- Größenänderung einzelner Kamerakarten per Ecke
- Button „Ansicht zurücksetzen"
- Automatischer Reconnect bei Verbindungsverlust (5 Sekunden)
- Vollbildmodus pro Kamera
- Echtzeit-Statusanzeige (Online / Offline) mit Farbindikator
- LIVE-Badge mit animiertem Punkt
- Uhr im Header
- Dunkles Design mit Scholz-Recycling-Logo (eingebettet als Base64)
- Benutzerverwaltung mit Login-Screen
- Rollen: Admin und User
- Passwort-Hashing mit SHA-256
- Admin-Panel: Benutzer anlegen, löschen, Passwörter zurücksetzen
- Passwort ändern für eigenen Account
- SessionStorage für Benutzerdaten (weg beim Tab-Schließen)
- Kamera-Konfigurationsexport als YAML
- Kamera-Zugangsdaten AES-256-GCM verschlüsselt (PBKDF2, 310.000 Iterationen)
- Benutzerdatenbank-Export / Import als YAML
- Einstellungen: Maximale Kameraanzahl konfigurierbar
- Vendor-Presets mit automatisch befülltem MJPEG-Pfad

### Technisch
- Vollständig in einer HTML-Datei (kein Backend, kein Framework)
- Web Crypto API für Hashing und Verschlüsselung
- ResizeObserver für dynamische Raster-Resizer
- YAML-Parser und -Writer selbst implementiert (keine externe Bibliothek)

---

## [Unreleased]

Geplante Änderungen für zukünftige Versionen:

### Geplant
- Zentraler Backend-Server für Netzwerkbetrieb (Phase 2)
- REST-API zur Benutzerverwaltung
- RTSP-zu-MJPEG-Proxy
- Aufzeichnungsfunktion
- Bewegungserkennung / Alarmierung
- Dark/Light Mode Umschalter
- Mehrsprachigkeit (DE / EN)
