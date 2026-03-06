# Scholz Videowall

Eine browserbasierte IP-Kamera-Monitoring-App für Scholz Recycling GmbH.  
Unterstützt MJPEG-Streams von Mobotix, Axis, Hikvision und Custom-Kameras.

**Version:** 1.0.0  
**Lizenz:** Proprietär – Scholz Recycling GmbH

---

## Features

- **MJPEG-Livestreaming** direkt im Browser – kein Server, kein Plugin
- **Multi-Kamera-Dashboard** mit 4 bis 12 Kamera-Slots
- **Flexible Layouts** – Raster frei ziehbar (Spalten, Zeilen, Einzelkarten)
- **Benutzerverwaltung** – Login, Admin-Panel, Rollen (Admin / User)
- **Passwort-Hashing** – SHA-256, keine Klartextpasswörter
- **Konfigurationsexport** – YAML-Datei mit AES-256-GCM verschlüsselten Zugangsdaten
- **Benutzerdatenbank-Export** – alle Benutzer inkl. Kamera-Konfigurationen als YAML
- **Vollständig offline** – einzige Datei, kein Backend, kein Internet erforderlich

---

## Unterstützte Hersteller

| Hersteller | MJPEG-Pfad (Standard) |
|---|---|
| Mobotix | `/control/faststream.jpg?stream=full` |
| Axis | `/mjpg/video.mjpg` |
| Hikvision | `/streaming/channels/101/httppreview` |
| Custom | frei konfigurierbar |

---

## Systemvoraussetzungen

| Anforderung | Detail |
|---|---|
| Browser | Chrome 90+, Edge 90+, Firefox 88+ |
| Netzwerk | PC und Kameras im selben Netzwerk |
| Server | keiner – reine HTML-Datei |
| Internet | nicht erforderlich (nach erstem Laden) |

---

## Schnellstart

1. `Scholz-Videowall.html` auf einem PC öffnen, der im Kameranetzwerk ist
2. Login mit `admin` / `admin`
3. Passwort sofort ändern (🔑-Button im Header)
4. Kameras über **+ KAMERA** hinzufügen
5. Layout nach Bedarf anpassen

---

## Benutzerverwaltung

### Rollen

| Rolle | Rechte |
|---|---|
| **Admin** | Benutzer anlegen & löschen, Passwörter zurücksetzen, alle Funktionen |
| **User** | Eigene Kameras verwalten, eigenes Passwort ändern |

### Standard-Login

```
Benutzername: admin
Passwort:     admin
```

> ⚠️ Das Standardpasswort beim ersten Start sofort ändern!

### Passwörter

- Passwörter werden als **SHA-256-Hash** gespeichert – nie im Klartext
- Benutzerdaten liegen in der **SessionStorage** des Browsers (weg beim Tab-Schließen)
- Für dauerhafte Speicherung: Benutzerdatenbank über das Admin-Panel exportieren

---

## Konfigurationsdateien

### Kamera-Konfiguration (`Scholz-Videowall.yaml`)

Enthält Kamera-Einstellungen eines einzelnen Benutzers.  
Kamera-Zugangsdaten (Benutzername/Passwort) sind **AES-256-GCM verschlüsselt**.

```yaml
version: 2

settings:
  max_cameras: 4

cameras:
  - name:   Eingang Nord
    vendor: mobotix
    host:   192.168.1.100
    port:   80
    path:   /control/faststream.jpg?stream=full
    id:     cam_1234567890

# Passwörter AES-256-GCM verschlüsselt
enc_creds: a3Fz8Xk...base64...
```

### Benutzerdatenbank (`Scholz-Videowall-Users.yaml`)

Enthält alle Benutzer mit Rollen und Kamera-Konfigurationen.  
Passwörter sind als **SHA-256-Hash** gespeichert.

```yaml
# Scholz Videowall – Benutzerdatenbank
version: 1
users:
  - username: admin
    role:     admin
    pw_hash:  8c6976e5b5410415bde908bd4dee15dfb167a9c873fc4bb8a81f6f2ab448a918
    maxcams:  4
    cameras:  eyJpZCI6ImNhbV8x...base64...
```

> ⚠️ Beide Dateien sicher aufbewahren – z.B. in einem verschlüsselten Ordner.

---

## Datensicherheit

| Aspekt | Umsetzung |
|---|---|
| Passwort-Speicherung | SHA-256-Hash |
| Kamera-Zugangsdaten | AES-256-GCM, PBKDF2 (310.000 Iterationen) |
| Datenspeicherung | Nur SessionStorage (kein localStorage, kein Cookie) |
| Netzwerk | Direktverbindung Browser → Kamera, kein Proxy |
| Verschlüsselung | Web Crypto API (nativ im Browser, kein externes Framework) |

---

## Roadmap – Phase 2

- [ ] Zentraler Backend-Server (Node.js / Python) für Netzwerkbetrieb
- [ ] REST-API zur Benutzerverwaltung
- [ ] Mehrere gleichzeitige Clients (Videowall auf mehreren Bildschirmen)
- [ ] RTSP-zu-MJPEG-Proxy für Kameras ohne nativen MJPEG-Support
- [ ] Aufzeichnungsfunktion
- [ ] Bewegungserkennung / Alarmierung

---

## Projektstruktur

```
scholz-videowall/
├── Scholz-Videowall.html          # Hauptanwendung (alles in einer Datei)
├── README.md                      # Diese Datei
├── CHANGELOG.md                   # Versionshistorie
└── config/                        # Konfigurationsbeispiele (nicht einchecken!)
    ├── Scholz-Videowall.yaml      # Kamera-Konfiguration (Beispiel)
    └── Scholz-Videowall-Users.yaml  # Benutzerdatenbank (Beispiel)
```

> ⚠️ Die `config/`-Dateien enthalten sensible Daten und sollten **nicht** in Git eingecheckt werden. Dafür eine `.gitignore` anlegen.

---

## .gitignore (empfohlen)

```
config/
*.yaml
!README.md
```

---

## Entwicklung

Entwickelt mit Claude (Anthropic) – März 2026  
Betreut von: IT-Abteilung, Scholz Recycling GmbH
