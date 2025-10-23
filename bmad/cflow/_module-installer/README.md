# ContentFlow Module Installer

Dieser Ordner enthält alle Installations-Konfigurationen für das ContentFlow-Modul.

## Dateien in diesem Ordner

### `install-config.yaml`

Die Hauptkonfigurationsdatei für die Installation.

**Definiert:**

- Modul-Metadaten (code, name)
- Willkommens-Nachricht
- Interactive Felder (API-Keys, Strategy, Automation Level)
- Static Felder (Paths, Advanced Settings)

**Während Installation:**

1. User wird durch alle Interactive Felder geführt
2. Antworten werden gespeichert
3. Static Felder werden automatisch gesetzt
4. Output: `bmad/cflow/config.yaml` (generierte Config)

### `installer.js` (optional - aktuell nicht vorhanden)

Custom Installation Logic (falls benötigt).

**Wann nötig:**

- API-Key-Validierung vor Installation
- Datenbank-Setup
- Externe Service-Registration
- Komplexe File-Transformationen

**Aktueller Status:** Nicht implementiert. ContentFlow braucht keine custom Logic - Standard-Installer reicht.

### `/assets/` - Installation Assets

Dateien, die während Installation kopiert/verwendet werden:

#### `tone-of-voice.md` (65 Seiten)

Adrian Goldners kompletter Tone-of-Voice-Guide.

**Verwendet von:**

- Content-Writer Agent (befolgt ToV-Richtlinien)
- Quality-Validator Agent (prüft Authentizität gegen ToV)

**Wird kopiert nach:** `bmad/cflow/_module-installer/assets/`
_(bleibt im Installer-Ordner, wird referenziert)_

#### `seo-masterplan.md` (SEO-Strategie)

Komplettes SEO-Strategie-Dokument mit:

- Topic-Map-Strategie
- Pillar/Cluster-Struktur
- Keyword-Research-Methodik
- Technical SEO Standards

**Verwendet von:**

- SEO-Strategist Agent (als Strategie-Referenz)
- Content-Writer Agent (für SEO-Best-Practices)

**Wird kopiert nach:** `bmad/cflow/_module-installer/assets/`
_(bleibt im Installer-Ordner, wird referenziert)_

#### `example-topic-map.yaml` (Topic-Map Template)

Beispiel Topic-Map mit 2 Pillars + Clusters.

**Verwendet als:**

- Template für User's eigene Topic-Map
- Referenz für Struktur
- Beispiel-Daten für Testing

**Wird kopiert nach:** `bmad/cflow/data/topic-maps/example-topic-map.yaml`
_(User kopiert dann zu topic-map-master.yaml und passt an)_

## Installation Flow

### 1. Pre-Installation

```
User führt aus: bmad install
→ Installer scannt /bmad/*/_module-installer/
→ Findet ContentFlow (cflow)
→ Zeigt in Auswahl-Liste
```

### 2. Module Selection

```
User wählt: ☑ ContentFlow
→ Installer liest install-config.yaml
→ Zeigt Welcome-Prompt
```

### 3. Interactive Questions

```
Installer stellt 10 Fragen:
1. Google Search Console API Key
2. Webflow API Key
3. Brevo API Key
4. Plausible API Key (optional)
5. Thrivecart API Key (optional)
6. Social Media API Key (optional)
7. Monthly Article Goal (Single-Select)
8. Newsletter Frequency (Single-Select)
9. Social Platforms (Multi-Select)
10. Automation Level (Single-Select)

User beantwortet alle erforderlichen Felder.
```

### 4. Config Generation

```
Installer generiert: bmad/cflow/config.yaml
Inhalt:
- User's Antworten aus Interactive Fields
- Static Values aus install-config.yaml
- Inherited Values (user_name, communication_language, output_folder)
- Resolved Paths ({project-root} → absoluter Pfad)
```

### 5. File Operations

```
Installer kopiert Assets:
- assets/*.md → bleiben in _module-installer/assets/
- example-topic-map.yaml → bmad/cflow/data/topic-maps/

Installer erstellt Verzeichnisse:
- bmad/cflow/data/interviews/{current-month}/
- bmad/cflow/data/analytics/
```

### 6. Optional: Custom Installer

```
Falls installer.js existiert:
→ Führt install(options) Function aus
→ options = { projectRoot, config, installedIDEs, logger }
→ Bei Error: Installation abbricht

Aktuell: Nicht vorhanden, wird übersprungen.
```

### 7. IDE Configuration

```
Installer erstellt Slash-Commands:
- /cflow:seo-strategist
- /cflow:content-interviewer
- /cflow:content-writer
- /cflow:quality-validator
- /cflow:content-publisher
- /cflow:social-distributor
- /cflow:analytics-reporter

Installer registriert Workflows:
- /cflow:workflow:content-creation
- /cflow:workflow:social-repurposing
- /cflow:workflow:seo-planning
- /cflow:workflow:performance-tracking
```

### 8. Post-Installation

```
Installer zeigt Success-Message:
"✅ ContentFlow erfolgreich installiert!"
"→ Config: bmad/cflow/config.yaml"
"→ Agents: 7 verfügbar"
"→ Workflows: 4 verfügbar"
"→ Nächste Schritte:"
"   1. Topic-Map erstellen: bmad/cflow/data/topic-maps/topic-map-master.yaml"
"   2. Ersten Workflow starten: /cflow:workflow:content-creation"
```

## Post-Installation Tasks (User)

Nach erfolgreicher Installation muss User:

### 1. Topic-Map erstellen

```bash
# Kopiere Example als Basis
cp bmad/cflow/data/topic-maps/example-topic-map.yaml \
   bmad/cflow/data/topic-maps/topic-map-master.yaml

# Editiere topic-map-master.yaml:
# - Definiere eigene Pillars
# - Definiere Cluster-Artikel
# - Setze Keywords & Funnel-Phases
```

### 2. Google Search Console verbinden

```
1. Exportiere GSC-Daten (letzter Monat)
2. Speichere als CSV: bmad/cflow/data/analytics/gsc-export-{YYYY-MM}.csv
3. Oder: API-Key in config.yaml eintragen (wurde schon gemacht)
```

### 3. Ersten Workflow testen

```
Starte Content-Creation Workflow:
/cflow:workflow:content-creation

Oder lade Agenten direkt:
/cflow:seo-strategist
```

### 4. (Optional) Topic-Map mit bestehenden Artikeln füllen

```
Falls du bereits Artikel hast:
1. Öffne topic-map-master.yaml
2. Füge bestehende Artikel als Cluster hinzu
3. Markiere als status: published
4. Setze published_date
```

## Troubleshooting

### "API-Key ungültig" Error

```
Öffne: bmad/cflow/config.yaml
Überprüfe api_keys Sektion:
- google_search_console_api
- webflow_api
- brevo_api

Trage korrekte Keys ein.
```

### "Topic-Map nicht gefunden"

```
Erstelle: bmad/cflow/data/topic-maps/topic-map-master.yaml
Verwende example-topic-map.yaml als Basis.
```

### "Tone-of-Voice-Guide nicht gefunden"

```
Prüfe ob existiert:
bmad/cflow/_module-installer/assets/tone-of-voice.md

Falls nicht: Re-Installation durchführen.
```

## Updates & Maintenance

### Module Update

```bash
# Bei neuer ContentFlow-Version:
bmad update cflow

# Installer merged neue Features in bestehende config.yaml
# Bestehende Daten bleiben erhalten
```

### Config ändern

```bash
# Editiere direkt:
nano bmad/cflow/config.yaml

# Oder Re-Run Installer:
bmad install --force cflow
```

### Reset Module

```bash
# ACHTUNG: Löscht alle Daten!
rm -rf bmad/cflow/data/*
rm bmad/cflow/config.yaml

# Dann Re-Install:
bmad install cflow
```

## Support

Bei Problemen:

1. Prüfe Logs: `bmad/cflow/logs/installer.log` (falls vorhanden)
2. Validiere config.yaml Syntax
3. GitHub Issues: https://github.com/adriangoldner/bmad-method/issues
