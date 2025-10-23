# ContentFlow Modul - Verzeichnisstruktur

**Erstellungsdatum:** 2025-10-22
**Modul:** ContentFlow (cflow)
**Komplexität:** COMPLEX MODULE

---

## Vollständige Verzeichnisstruktur

```
bmad/cflow/
├── agents/                           # 7 KI-Agenten-Definitionen
│   ├── seo-strategist.md            # Topic Research & Keyword-Analyse
│   ├── content-interviewer.md       # Wissensextraktion durch Interviews
│   ├── content-writer.md            # Artikel-Erstellung (Newsletter + SEO)
│   ├── quality-validator.md         # SEO & Authentizitäts-Prüfung
│   ├── content-publisher.md         # Veröffentlichung (Webflow + Newsletter)
│   ├── social-distributor.md        # Social Media Repurposing
│   └── analytics-reporter.md        # KPI-Tracking & Reporting
│
├── workflows/                        # 4 Haupt-Workflows
│   ├── content-creation/            # Interview → Draft → Validate → Publish
│   │   ├── workflow.yaml           # Workflow-Konfiguration
│   │   ├── instructions.md         # Schritt-für-Schritt-Anweisungen
│   │   └── README.md               # Workflow-Dokumentation
│   │
│   ├── social-repurposing/         # Artikel → 5 Social-Assets
│   │   ├── workflow.yaml
│   │   ├── instructions.md
│   │   └── README.md
│   │
│   ├── seo-planning/               # GSC-Analyse → Monthly Content-Plan
│   │   ├── workflow.yaml
│   │   ├── instructions.md
│   │   ├── template.md             # Monthly-Content-Plan Template
│   │   └── README.md
│   │
│   └── performance-tracking/       # Datensammlung → Monthly Report
│       ├── workflow.yaml
│       ├── instructions.md
│       ├── template.md             # Monthly-Analytics-Report Template
│       └── README.md
│
├── tasks/                           # 3 Utility Tasks
│   ├── schema-generator.xml        # JSON-LD Schema-Generierung
│   ├── internal-link-finder.xml   # Relevante interne Links finden
│   └── authenticity-scorer.xml    # AI-Detection Score (0-100)
│
├── templates/                       # Template-Bibliothek
│   ├── content/                    # Content-Templates
│   │   ├── newsletter-template.md
│   │   ├── seo-article-template.md
│   │   ├── pillar-article-template.md
│   │   └── cluster-article-template.md
│   │
│   ├── reports/                    # Report-Templates
│   │   ├── monthly-content-plan-template.md
│   │   ├── monthly-analytics-report-template.md
│   │   └── validation-report-template.md
│   │
│   └── social/                     # Social-Media-Templates
│       ├── linkedin-mini-post-template.md
│       ├── linkedin-carousel-template.md
│       ├── instagram-reel-script-template.md
│       ├── instagram-carousel-template.md
│       ├── instagram-quote-template.md
│       ├── x-thread-template.md
│       └── facebook-story-template.md
│
├── data/                            # Daten-Management
│   ├── topic-maps/                 # Topic-Cluster & Pillar-Strukturen
│   │   ├── topic-map-master.yaml  # Master Topic-Map
│   │   ├── pillar-gesangstechnik.yaml
│   │   ├── pillar-blending.yaml
│   │   └── README.md
│   │
│   ├── interviews/                 # Interview-Archive
│   │   ├── 2025-10/                # Monatliche Archivierung
│   │   │   ├── interview-001-stimmanalyse.md
│   │   │   └── interview-002-hohe-toene.md
│   │   └── README.md
│   │
│   └── analytics/                  # Analytics-Historie
│       ├── 2025-10-analytics.json
│       ├── 2025-11-analytics.json
│       └── README.md
│
├── _module-installer/              # Installations-Konfiguration
│   ├── install-config.yaml        # Installation Questions & Config
│   ├── installer.js               # Custom Installation Logic (optional)
│   └── assets/                    # Assets für Installation
│       ├── tone-of-voice.md       # 65-seitiger ToV-Guide
│       ├── seo-masterplan.md      # SEO-Strategie-Dokument
│       └── example-topic-map.yaml
│
├── config.yaml                      # Modul-Konfiguration (generiert bei Installation)
└── README.md                        # Modul-Hauptdokumentation

```

---

## Verzeichnis-Beschreibungen

### `/agents/` - Agenten-Definitionen

Enthält die 7 KI-Agenten als BMAD-konforme Agent-Markdown-Dateien.

**Struktur jeder Agent-Datei:**

- Agent-Metadaten (Name, Typ, Rolle)
- Verantwortlichkeiten
- Input/Output-Spezifikationen
- Interaktion mit anderen Agenten
- Beispiel-Prompts
- Aktivierungs-Anweisungen

**7 Agenten:**

1. `seo-strategist.md` - Topic Research & Keyword-Analyse
2. `content-interviewer.md` - Interview-Dialog & Wissensextraktion
3. `content-writer.md` - Newsletter + SEO-Artikel-Erstellung
4. `quality-validator.md` - SEO & Authentizitäts-Prüfung
5. `content-publisher.md` - Webflow + Newsletter Publishing
6. `social-distributor.md` - Multi-Platform Social-Content
7. `analytics-reporter.md` - KPI-Tracking & Reporting

---

### `/workflows/` - Workflow-Definitionen

4 Haupt-Workflows, jeweils in eigenem Unterordner.

**Struktur jedes Workflow-Ordners:**

- `workflow.yaml` - Workflow-Konfiguration (BMAD-Standard)
- `instructions.md` - Detaillierte Schritt-für-Schritt-Anweisungen
- `template.md` - Output-Template (falls Document-Workflow)
- `README.md` - Workflow-Dokumentation & Verwendung

**4 Workflows:**

1. **content-creation/** - Haupt-Content-Produktions-Workflow
   - Typ: Interactive Workflow (Multi-Step mit Human-in-Loop)
   - Dauer: 3-5 Tage
   - Output: Published Newsletter + SEO-Artikel

2. **social-repurposing/** - Social-Media-Automatisierung
   - Typ: Action Workflow (automatisiert)
   - Dauer: 1-2 Stunden
   - Output: 5 Social-Media-Posts (scheduled)

3. **seo-planning/** - Monatliche Content-Planung
   - Typ: Document Workflow
   - Dauer: 30-60 Minuten
   - Output: Monthly-Content-Plan.md

4. **performance-tracking/** - Analytics & Reporting
   - Typ: Action Workflow (monatlich getriggert)
   - Dauer: 15-30 Minuten
   - Output: Monthly-Analytics-Report.md

---

### `/tasks/` - Utility Tasks

3 wiederverwendbare Task-Definitionen (BMAD XML-Format).

**Tasks:**

1. `schema-generator.xml` - Generiert JSON-LD Schema-Markup
   - Unterstützt: Article, FAQ, Product, Breadcrumb
   - Verwendet von: Content-Publisher Agent

2. `internal-link-finder.xml` - Findet relevante interne Links
   - Sucht in Topic-Map nach verwandten Artikeln
   - Verwendet von: Content-Writer Agent

3. `authenticity-scorer.xml` - Bewertet Text auf AI-Fingerprints
   - Score 0-100
   - Prüft auf 8 AI-Fingerprints + 5 Authentizitäts-Marker
   - Verwendet von: Quality-Validator Agent

---

### `/templates/` - Template-Bibliothek

Wiederverwendbare Content-, Report- und Social-Media-Templates.

**Unterordner:**

**`/templates/content/`** - Content-Erstellungs-Templates

- `newsletter-template.md` - Email-Newsletter-Struktur
- `seo-article-template.md` - SEO-optimierter Blog-Artikel
- `pillar-article-template.md` - Pillar-Content (2500+ Wörter)
- `cluster-article-template.md` - Cluster-Artikel (1000+ Wörter)

**`/templates/reports/`** - Report-Templates

- `monthly-content-plan-template.md` - SEO-Planning Output
- `monthly-analytics-report-template.md` - Performance-Tracking Output
- `validation-report-template.md` - Quality-Validator Output

**`/templates/social/`** - Social-Media-Templates

- LinkedIn: Mini-Post + Carousel
- Instagram: Reel-Script + Carousel + Quote
- X/Threads: Thread-Struktur
- Facebook: Story-Format

---

### `/data/` - Daten-Management

Persistente Daten, die von Workflows und Agenten genutzt werden.

**Unterordner:**

**`/data/topic-maps/`** - SEO-Topic-Strukturen

- `topic-map-master.yaml` - Master-Übersicht aller Pillars & Clusters
- `pillar-gesangstechnik.yaml` - Pillar #1 mit allen Cluster-Artikeln
- `pillar-blending.yaml` - Pillar #2
- Jeder Pillar verlinkt seine 8+ Cluster-Artikel

**Beispiel topic-map-master.yaml:**

```yaml
pillars:
  - id: pillar-001
    name: "Gesangstechnik & CVT im Chor"
    url: "/gesangstechnik-chor"
    keyword_focus: "stimmtechnik"
    funnel_phase: awareness
    clusters:
      - id: cluster-001
        name: "Was ist Stimmtechnik wirklich"
        url: "/newsletter/stimmtechnik"
        keyword: "stimmtechnik"
        status: published
        published_date: "2025-10-15"
      [...]
```

**`/data/interviews/`** - Interview-Archive

- Organisiert nach Monat: `2025-10/`, `2025-11/`
- Jedes Interview als Markdown-Datei
- Enthält Fragen, Antworten, Anekdoten
- Wird referenziert von published Content

**`/data/analytics/`** - Analytics-Historie

- Monatliche JSON-Exports von allen APIs
- GSC, Plausible, Brevo, Thrivecart, Social Media
- Ermöglicht Trend-Analysen über Zeit

---

### `/_module-installer/` - Installations-Konfiguration

Installations-Infrastruktur für BMAD-Installer.

**Dateien:**

**`install-config.yaml`** - Installation Questions & Module Config

- Definiert Konfigurations-Felder
- Interactive (fragt User) vs. Static (hardcoded)
- Single-Select, Multi-Select, Text-Input
- Default-Werte

**`installer.js`** (optional) - Custom Installation Logic

- Wird ausgeführt nach File-Copy, vor IDE-Config
- Für spezielle Setup-Schritte (z.B. API-Key-Validierung)
- Erhält Zugriff auf config-Werte

**`/assets/`** - Installation-Assets

- `tone-of-voice.md` - 65-seitiger ToV-Guide (aus tmp/)
- `seo-masterplan.md` - SEO-Strategie (aus tmp/)
- `example-topic-map.yaml` - Beispiel-Topic-Map
- Diese werden bei Installation nach `data/` kopiert

---

## Generierte Dateien (nach Installation)

Diese Dateien existieren NICHT im Source-Modul, sondern werden bei Installation generiert:

**`config.yaml`** - Modul-Konfiguration

- Generiert aus install-config.yaml
- Enthält User-Antworten + Static Values
- Wird von allen Agenten/Workflows gelesen

**Beispiel-Struktur:**

```yaml
# ContentFlow Module Configuration
# Generated: 2025-10-22T10:30:00Z

# Core Config (inherited from BMAD)
user_name: Adrian
communication_language: German
document_output_language: German
output_folder: '{project-root}/docs'

# ContentFlow-specific Config
api_keys:
  google_search_console: '[USER INPUT]'
  webflow: '[USER INPUT]'
  brevo: '[USER INPUT]'
  plausible: '[USER INPUT]'

paths:
  topic_map: '{project-root}/bmad/cflow/data/topic-maps/topic-map-master.yaml'
  interview_archive: '{project-root}/bmad/cflow/data/interviews'
  tone_of_voice_guide: '{project-root}/bmad/cflow/_module-installer/assets/tone-of-voice.md'

content_strategy:
  monthly_article_goal: 8
  newsletter_frequency: 'weekly'
  social_platforms: ['linkedin', 'instagram', 'x', 'facebook']

automation_level: 'semi-auto' # 'manual' | 'semi-auto' | 'full-auto'
```

---

## Dateinamens-Konventionen

### Agenten

- Kebab-case: `seo-strategist.md`, `content-writer.md`
- Immer `.md` Extension
- Beschreibende Namen basierend auf Rolle

### Workflows

- Ordnername: kebab-case (`content-creation`)
- Workflow-Config: immer `workflow.yaml`
- Instructions: immer `instructions.md`
- Template: immer `template.md` (falls Document-Workflow)

### Tasks

- Kebab-case: `schema-generator.xml`
- Immer `.xml` Extension (BMAD-Task-Format)
- Beschreibende Namen basierend auf Funktion

### Templates

- Kebab-case mit `-template` Suffix
- `newsletter-template.md`, `linkedin-mini-post-template.md`
- Immer `.md` Extension

### Data Files

- Topic-Maps: `topic-map-*.yaml` oder `pillar-*.yaml`
- Interviews: `interview-{NNN}-{topic-slug}.md`
- Analytics: `{YYYY-MM}-analytics.json`

---

## Dateigröße-Schätzungen

| Verzeichnis           | Anzahl Dateien  | Geschätzte Größe             |
| --------------------- | --------------- | ---------------------------- |
| `/agents/`            | 7               | ~70 KB (10 KB pro Agent)     |
| `/workflows/`         | 16 (4 × 4)      | ~160 KB                      |
| `/tasks/`             | 3               | ~15 KB                       |
| `/templates/`         | 14              | ~70 KB                       |
| `/data/`              | Initial: ~10    | ~50 KB                       |
| `/_module-installer/` | ~5              | ~100 KB (ToV-Guide ist groß) |
| **TOTAL (Initial)**   | **~55 Dateien** | **~465 KB**                  |

**Nach 6 Monaten Nutzung:**

- `/data/interviews/` wächst: ~50 Interviews = ~500 KB
- `/data/analytics/` wächst: ~6 Monate = ~30 KB
- **Total nach 6M:** ~1 MB

---

## Zugriffsmuster

### Welche Dateien lesen welche Agenten/Workflows?

**SEO-Strategist Agent:**

- Liest: `data/topic-maps/topic-map-master.yaml`
- Liest: `data/analytics/{YYYY-MM}-analytics.json` (GSC-Daten)
- Schreibt: `templates/reports/monthly-content-plan-template.md` (via SEO-Planning Workflow)

**Content-Interviewer Agent:**

- Liest: `config.yaml` (user_name für Ansprache)
- Schreibt: `data/interviews/{YYYY-MM}/interview-{NNN}-{topic}.md`

**Content-Writer Agent:**

- Liest: `data/interviews/{YYYY-MM}/interview-{NNN}-{topic}.md`
- Liest: `_module-installer/assets/tone-of-voice.md`
- Liest: `data/topic-maps/topic-map-master.yaml` (für interne Links)
- Verwendet: `templates/content/newsletter-template.md`
- Verwendet: `templates/content/seo-article-template.md`

**Quality-Validator Agent:**

- Liest: `_module-installer/assets/tone-of-voice.md` (Authentizitäts-Kriterien)
- Verwendet: Task `tasks/authenticity-scorer.xml`
- Verwendet: `templates/reports/validation-report-template.md`

**Content-Publisher Agent:**

- Liest: `config.yaml` (API-Keys)
- Verwendet: Task `tasks/schema-generator.xml`

**Social-Distributor Agent:**

- Verwendet: `templates/social/*.md` (alle Social-Templates)
- Liest: `config.yaml` (social_platforms)

**Analytics-Reporter Agent:**

- Liest: `config.yaml` (API-Keys)
- Schreibt: `data/analytics/{YYYY-MM}-analytics.json`
- Verwendet: `templates/reports/monthly-analytics-report-template.md`

---

## Nächste Schritte

1. ✅ Verzeichnisstruktur erstellt
2. ⏭️ Konfigurationsfelder planen (`install-config.yaml`)
3. ⏭️ Ersten Agent erstellen (Empfehlung: SEO-Strategist)
4. ⏭️ Ersten Workflow implementieren (Empfehlung: Content-Creation)
5. ⏭️ Templates befüllen
6. ⏭️ Installer einrichten
7. ⏭️ README.md schreiben
8. ⏭️ Roadmap generieren

---

**Dokumentations-Status:**

- [x] Modul-Identität definiert
- [x] Komponenten geplant
- [x] Komplexität bestimmt (COMPLEX)
- [x] Verzeichnisstruktur erstellt
- [ ] Konfiguration geplant
- [ ] Implementierung gestartet
