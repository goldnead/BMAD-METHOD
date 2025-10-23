# ContentFlow

**Interview-basiertes Content-Produktions-System mit KI-Agenten-Flotte**

Version: 1.0.0-alpha
Autor: Adrian Goldner
Lizenz: MIT
Modul-Code: `cflow`
Komplexität: COMPLEX MODULE

---

## 🎯 Überblick

ContentFlow ist ein intelligentes Content-Produktions-System, das durch orchestrierte KI-Agenten wöchentlich authentischen, SEO-optimierten Content erstellt - vom Newsletter über Website-Artikel bis zu Social Media Posts.

**Was macht ContentFlow anders?**

1. **Interview-basierte Wissensextraktion** - Kein "Prompt → Output", sondern strukturierte Gespräche, die deine einzigartige Stimme bewahren
2. **Authentizitäts-Validation** - Dedicated Agent prüft auf AI-Fingerprints und stellt sicher, dass Content wie DU klingst
3. **End-to-End-Workflow** - Von Keyword-Research bis Social Distribution, alles orchestriert
4. **Topic-First SEO** - Nicht Keyword-Stuffing, sondern Themenautorität aufbauen
5. **Multi-Platform Output** - 1 Artikel → Newsletter + SEO-Post + 5 Social-Media-Assets

---

## 🚀 Quick Start

### Installation

```bash
# BMAD-Installer verwenden
bmad install

# ContentFlow auswählen
☑ ContentFlow

# Fragen beantworten (API-Keys, Strategy, Automation Level)
# Config wird generiert: bmad/cflow/config.yaml
```

### Erste Schritte

1. **Topic-Map erstellen**

   ```bash
   # Kopiere Example als Basis
   cp bmad/cflow/data/topic-maps/example-topic-map.yaml \
      bmad/cflow/data/topic-maps/topic-map-master.yaml

   # Editiere: Definiere Pillars & Cluster-Artikel
   nano bmad/cflow/data/topic-maps/topic-map-master.yaml
   ```

2. **Google Search Console Daten laden**

   ```bash
   # Exportiere GSC-Daten (letzter Monat) als CSV
   # Oder: API-Key wurde bereits in config.yaml eingetragen
   ```

3. **Ersten Content-Creation Workflow starten**

   ```bash
   # Via Slash-Command
   /cflow:workflow:content-creation

   # Oder Agent direkt laden
   /cflow:seo-strategist
   ```

---

## 📦 Was ist enthalten?

### 🤖 7 KI-Agenten

| Agent                   | Rolle                               | Typ    |
| ----------------------- | ----------------------------------- | ------ |
| **SEO-Strategist**      | Topic Research & Keyword-Analyse    | Expert |
| **Content-Interviewer** | Wissensextraktion durch Interviews  | Expert |
| **Content-Writer**      | Newsletter + SEO-Artikel-Erstellung | Expert |
| **Quality-Validator**   | SEO & Authentizitäts-Prüfung        | Expert |
| **Content-Publisher**   | Webflow + Newsletter Publishing     | Simple |
| **Social-Distributor**  | Multi-Platform Social-Content       | Expert |
| **Analytics-Reporter**  | KPI-Tracking & Reporting            | Simple |

### 🔄 4 Haupt-Workflows

| Workflow                 | Typ         | Dauer     | Output                             |
| ------------------------ | ----------- | --------- | ---------------------------------- |
| **Content-Creation**     | Interactive | 3-5 Tage  | Published Newsletter + SEO-Artikel |
| **Social-Repurposing**   | Action      | 1-2 Std   | 5 Social-Media-Posts (scheduled)   |
| **SEO-Planning**         | Document    | 30-60 Min | Monthly Content-Plan               |
| **Performance-Tracking** | Action      | 15-30 Min | Monthly Analytics-Report           |

### 🛠️ 3 Utility Tasks

- **Schema-Generator** - JSON-LD für Article/FAQ/Product
- **Internal-Link-Finder** - Findet relevante interne Links
- **Authenticity-Scorer** - Bewertet Text auf AI-Fingerprints (0-100)

### 📄 14 Content-Templates

- **Content:** Newsletter, SEO-Artikel, Pillar, Cluster
- **Reports:** Content-Plan, Analytics-Report, Validation-Report
- **Social:** LinkedIn (Mini-Post + Carousel), Instagram (Reel + Carousel + Quote), X (Thread), Facebook (Story)

---

## 🎯 Wer sollte ContentFlow nutzen?

### Ideal für:

✅ **Content Creators** mit Newsletter-First-Strategie
✅ **Coaches & Consultants** die Content als Lead-Gen nutzen
✅ **SEO-Marketer** die Authentizität bewahren wollen
✅ **Experten** die ihre Expertise skalieren möchten

### Perfekt wenn du:

- Wöchentlich oder zweiwöchentlich Newsletter versendest
- SEO-Sichtbarkeit aufbauen willst
- Multi-Platform (Website + Social) bespielst
- Deine persönliche Stimme bewahren willst
- Zeitmangel für Content-Produktion hast

### Nicht geeignet wenn:

❌ Du nur sporadisch Content erstellst (< 1× pro Monat)
❌ Du keine Newsletter-Liste hast oder aufbauen willst
❌ Du ausschließlich auf Social Media fokussiert bist (ohne Website)
❌ Du vollautomatischen Content ohne Human-Review willst

---

## 🔧 Wie funktioniert ContentFlow?

### Content-Creation Workflow (Hauptprozess)

```
┌─────────────────────────────────────────────────────────┐
│ 1. SEO-STRATEGIST: Topic Research                      │
│    → Analysiert GSC-Daten                               │
│    → Identifiziert Quick-Win Keywords                   │
│    → Erstellt Content-Briefing                          │
└─────────────────────────────────────────────────────────┘
                          ↓
┌─────────────────────────────────────────────────────────┐
│ 2. CONTENT-INTERVIEWER: Angle Selection                │
│    → Präsentiert 4-6 Artikel-Angles                     │
│    → [USER] Wählt 1-2 Angles aus                        │
└─────────────────────────────────────────────────────────┘
                          ↓
┌─────────────────────────────────────────────────────────┐
│ 3. CONTENT-INTERVIEWER: Interview Phase                │
│    → Stellt 10-15 strukturierte Fragen                  │
│    → [USER] Beantwortet (Telegram/Notion)              │
│    → Stellt 2-3 Deep-Dive-Nachfragen                    │
│    → [USER] Beantwortet                                 │
│    → Erstellt Interview-Protokoll                       │
└─────────────────────────────────────────────────────────┘
                          ↓
┌─────────────────────────────────────────────────────────┐
│ 4. CONTENT-WRITER: Draft Creation                      │
│    → Newsletter-Version (Email-Format)                  │
│    → SEO-Artikel-Version (Webflow-Format)              │
│    → Befolgt Tone-of-Voice-Guide strikt                 │
│    → Integriert Interview-Inhalte authentisch          │
│    → Fügt 2 interne Links ein                           │
└─────────────────────────────────────────────────────────┘
                          ↓
┌─────────────────────────────────────────────────────────┐
│ 5. QUALITY-VALIDATOR: Prüfung                          │
│    → SEO-Check (10 Kriterien)                           │
│    → Authentizitäts-Check (8 Kriterien)                 │
│    → Authenticity-Score (0-100)                         │
│    → Bei NO-GO: Zurück zu Writer (max. 2×)             │
└─────────────────────────────────────────────────────────┘
                          ↓
┌─────────────────────────────────────────────────────────┐
│ 6. [USER APPROVAL]: Finale Review                      │
│    → Zeigt Newsletter + SEO-Artikel                     │
│    → "Artikel veröffentlichen?" (Ja/Nein/Edit)          │
└─────────────────────────────────────────────────────────┘
                          ↓
┌─────────────────────────────────────────────────────────┐
│ 7. CONTENT-PUBLISHER: Publishing                       │
│    → Webflow-Upload (mit Schema)                        │
│    → Newsletter-Versand (Brevo)                         │
│    → GSC-Index-Request                                  │
└─────────────────────────────────────────────────────────┘
                          ↓
┌─────────────────────────────────────────────────────────┐
│ 8. SOCIAL-DISTRIBUTOR: Auto-Repurposing (optional)     │
│    → 5 Social-Media-Assets erstellen                    │
│    → Scheduling (Publer/Metricool)                      │
└─────────────────────────────────────────────────────────┘
```

**Zeitaufwand:**

- **Interview-Phase:** 30-60 Min (deine aktive Zeit)
- **Review-Phase:** 10-20 Min (finale Approval)
- **System-Zeit:** 2-3 Tage (automatisch)
- **Total Durchlaufzeit:** 3-5 Tage (inkl. Human-in-Loop)

---

## 🎨 Authentizität bewahren - Wie?

### 1. Interview-basierte Wissensextraktion

Statt "Schreib mir einen Artikel über X", führt der Content-Interviewer einen strukturierten Dialog:

**Beispiel-Interview-Sequenz:**

```
Agent: "Wann hast du zum ersten Mal bemerkt, dass..."
Du: [Persönliche Anekdote aus der Praxis]

Agent: "Kannst du das an einer konkreten Probe illustrieren?"
Du: [Detailliertes Beispiel]

Agent: "Was würdest du jemandem raten, der..."
Du: [Deine Meinung & Empfehlung]
```

Das Interview-Protokoll wird dann vom Content-Writer verwendet, um einen Artikel in **DEINER Stimme** zu schreiben.

### 2. Tone-of-Voice-Guide Integration

Dein 65-seitiger Tone-of-Voice-Guide wird von zwei Agenten verwendet:

- **Content-Writer:** Befolgt ToV-Richtlinien beim Schreiben
- **Quality-Validator:** Prüft ob Text nach dir klingt

### 3. Authenticity-Scorer (0-100 Punkte)

Der Quality-Validator nutzt den Authenticity-Scorer Task, der prüft auf:

**AI-Fingerprints (Abzüge):**

- ❌ Contrast-Framing ("Es geht nicht um X, sondern um Y")
- ❌ Dreier-Regel-Overload
- ❌ Infomercial-Übergänge ("Die brutale Wahrheit?")
- ❌ Corporate-Sprache ("implementieren", "optimieren")
- ❌ Vage Füllphrasen

**Authentizitäts-Marker (Punkte):**

- ✅ Persönliche Anekdote
- ✅ Erfahrungs-Reflexion ("Früher..., Heute...")
- ✅ Direkte Leserfragen
- ✅ Weichmacher ("vielleicht", "irgendwie")

**Minimum Score zum Publishing:** 71/100
(konfigurierbar in `config.yaml`)

---

## 📊 Was du messen kannst

### Monatliche Analytics-Reports

Der Analytics-Reporter sammelt automatisch KPIs von:

**SEO (Google Search Console):**

- Klicks, Impressions, CTR, Avg Position
- Pro Artikel & aggregiert
- Quick-Win Keywords (hohe Impressions + niedrige CTR)

**Traffic (Plausible.io):**

- Pageviews, Sessions, Bounce Rate
- Scrolltiefe, Session-Dauer
- Conversion-Events

**Newsletter (Brevo):**

- Opt-ins, Open-Rate, Click-Rate
- Conversion zu Trials

**Revenue (Thrivecart):**

- Trial-Starts, Käufe, Upsells

**Social Media (Metricool):**

- Impressions, Engagement Rate, Follower-Wachstum

**Output:**

- `docs/analytics-report-{YYYY-MM}.md`
- Optional: Telegram-Notification

---

## 🗂️ Verzeichnisstruktur

```
bmad/cflow/
├── agents/              # 7 Agent-Definitionen
├── workflows/           # 4 Workflow-Ordner
├── tasks/               # 3 Utility Tasks
├── templates/           # 14 Content-Templates
├── data/                # Topic-Maps, Interviews, Analytics
├── _module-installer/   # Installation-Config
├── config.yaml          # Generierte Konfiguration
└── README.md            # Diese Datei
```

Detaillierte Struktur: Siehe [Directory Structure Documentation](../../docs/cflow-directory-structure.md)

---

## 🔐 Erforderliche API-Keys

### Mindestanforderungen (Required):

1. **Google Search Console API**
   - Für: Keyword-Analyse, Topic-Research
   - Setup: https://developers.google.com/webmaster-tools/v1/how-tos/authorizing

2. **Webflow API**
   - Für: Content-Publishing
   - Setup: Webflow Account → Settings → Integrations → API Access

3. **Brevo API** (ehemals Sendinblue)
   - Für: Newsletter-Versand, Lead-Tracking
   - Setup: Brevo Account → Settings → API Keys

### Optional (Empfohlen):

4. **Plausible.io API**
   - Für: Traffic-Analytics, Conversions
   - Kann später nachgetragen werden

5. **Thrivecart API**
   - Für: Revenue-Tracking
   - Kann später nachgetragen werden

6. **Social Media Scheduler API** (Publer oder Metricool)
   - Für: Auto-Scheduling von Social Posts
   - Kann später nachgetragen werden

**API-Keys werden während Installation abgefragt und in `config.yaml` gespeichert.**

---

## 📚 Dokumentation

### Planungs-Dokumente (in `/docs/`)

- [Module Identity](../../docs/cflow-module-identity.md) - Zweck, Zielgruppe, Vision
- [Components Planning](../../docs/cflow-module-components.md) - Agenten, Workflows, Tasks
- [Directory Structure](../../docs/cflow-directory-structure.md) - Vollständige Struktur

### Workflow-Dokumentation (in `/workflows/`)

- [Content-Creation Workflow](workflows/content-creation/README.md)
- [Social-Repurposing Workflow](workflows/social-repurposing/README.md)
- [SEO-Planning Workflow](workflows/seo-planning/README.md)
- [Performance-Tracking Workflow](workflows/performance-tracking/README.md)

### Agent-Dokumentation (in `/agents/`)

- Jeder Agent hat eigene Markdown-Datei mit:
  - Rolle & Verantwortlichkeiten
  - Input/Output-Spezifikationen
  - Interaktion mit anderen Agenten
  - Beispiel-Prompts

---

## 🎓 Best Practices

### 1. Topic-Map pflegen

- **Regelmäßig aktualisieren** (monatlich)
- **GSC-Daten integrieren** (Rankings, CTR)
- **Pillar-Cluster-Verhältnis:** 1:8+ (jeder Pillar 8+ Cluster)
- **Status tracken:** planned → draft → review → published

### 2. Interview-Qualität

- **Zeit nehmen:** 30-60 Min pro Interview
- **Konkrete Beispiele** aus der Praxis teilen
- **Persönliche Meinungen** aussprechen (kontrovers ist gut!)
- **Anekdoten erzählen** (machen Content authentisch)

### 3. SEO-Strategie

- **Topic-First:** Fokus auf Themenautorität, nicht einzelne Keywords
- **Long-Tail-Keywords:** Spezifische Fragen beantworten
- **Interne Verlinkung:** Jeder Artikel 2+ interne Links
- **Pillar-Cluster-Struktur:** Systematisch aufbauen

### 4. Content-Cadence

- **Konsistenz > Quantität:** Lieber 4/Monat konstant als 12/Monat sporadisch
- **Newsletter-First:** Jeder Artikel zuerst als Newsletter
- **Social-Repurposing:** Jeder Artikel → 5 Social-Assets
- **Evergreen-Fokus:** 80% Evergreen, 20% Timely

### 5. Authentizität bewahren

- **Interview nicht überspringen** (auch wenn verlockend)
- **Drafts reviewen** vor Publishing
- **Validation-Reports ernst nehmen** (Authenticity-Score < 71 → überarbeiten)
- **Tone-of-Voice-Guide aktualisieren** wenn sich deine Stimme entwickelt

---

## 🛠️ Konfiguration

### `config.yaml` Struktur

```yaml
# Core Config (inherited)
user_name: Adrian
communication_language: German
output_folder: '{project-root}/docs'

# API Keys
api_keys:
  google_search_console: '[REDACTED]'
  webflow: '[REDACTED]'
  brevo: '[REDACTED]'

# Content Strategy
monthly_article_goal: 8
newsletter_frequency: 'weekly'
social_platforms: ['linkedin', 'instagram', 'x', 'facebook']

# Automation
automation_level: 'semi-auto' # manual | semi-auto | full-auto

# Advanced Settings
authenticity_min_score: 71
max_validation_iterations: 2
auto_index_gsc: true
```

### Automation Levels erklärt

| Level         | Human-Touchpoints | Beschreibung                                        |
| ------------- | ----------------- | --------------------------------------------------- |
| **manual**    | Alle Schritte     | Du approvierst Interview-Fragen, Drafts, Publishing |
| **semi-auto** | 3 Key-Decisions   | Du approvierst Angle, Interview, finale Drafts      |
| **full-auto** | 1 Final-Review    | System macht alles, du reviewst nur vor Go-Live     |

**Empfohlen:** `semi-auto` (Balance zwischen Kontrolle & Effizienz)

---

## 🚨 Troubleshooting

### "Topic-Map nicht gefunden"

```bash
# Erstelle Topic-Map aus Example
cp bmad/cflow/data/topic-maps/example-topic-map.yaml \
   bmad/cflow/data/topic-maps/topic-map-master.yaml

# Editiere und passe an
nano bmad/cflow/data/topic-maps/topic-map-master.yaml
```

### "API-Key ungültig"

```bash
# Öffne Config
nano bmad/cflow/config.yaml

# Prüfe api_keys Sektion
# Trage korrekte Keys ein
# Speichern & neu starten
```

### "Authenticity-Score zu niedrig"

```
Problem: Artikel hat Score < 71, wird nicht veröffentlicht

Lösungen:
1. Interview-Antworten waren zu generisch
   → Nochmal Interview durchführen mit konkreteren Beispielen

2. Content-Writer hat ToV nicht befolgt
   → Prüfe ob tone-of-voice.md korrekt geladen wurde

3. Thema ist sehr technisch/formal
   → Authenticity-Min-Score in config.yaml senken (z.B. auf 65)
```

### "Webflow-Publishing fehlgeschlagen"

```
1. Prüfe API-Key in config.yaml
2. Prüfe Webflow-Berechtigungen (Publishing-Rights?)
3. Prüfe ob Collection existiert (z.B. "Blog Posts")
4. Prüfe Netzwerk-Verbindung
```

### "Social-Distributor erstellt keine Posts"

```
Problem: Workflow läuft durch, aber keine Social-Posts

Ursachen:
1. social_platforms in config.yaml leer
   → Mindestens 1 Plattform auswählen

2. social_media_api nicht gesetzt
   → Optional, aber ohne API kein Auto-Scheduling
   → Posts werden als Drafts erstellt statt scheduled
```

---

## 🗺️ Roadmap

### Phase 1: Foundation ✅ (aktuell)

- ✅ 7 Agenten definiert
- ✅ 4 Workflows geplant
- ✅ Installation-Config erstellt
- ⏳ Agenten implementieren
- ⏳ Workflows implementieren

### Phase 2: Enhancement (Q1 2026)

- Advanced Authenticity-Checks (Stil-Fingerprinting)
- Performance-based Optimierung (A/B-Testing)
- Template-Library erweitern (mehr Content-Typen)
- Multi-Language Support (Englisch)

### Phase 3: Integration (Q2 2026)

- Notion-Integration (als Alternative zu Telegram für Interviews)
- Slack-Integration (Team-Collaboration)
- CMS-Erweiterung (WordPress, Ghost Support)
- Advanced Analytics Dashboard

### Phase 4: Scale (Q3 2026)

- AI-Learning von User-Feedback
- Community-Templates (Best-Practices-Library)
- Multi-Author Support
- Collaborative Workflows

---

## 🤝 Contributing

ContentFlow ist Open Source (MIT License).

**Beiträge willkommen für:**

- Neue Agent-Typen
- Zusätzliche Workflows
- Template-Erweiterungen
- Bug-Fixes & Verbesserungen

**Repository:** https://github.com/adriangoldner/bmad-method (example)

---

## 📜 Lizenz

MIT License

Copyright (c) 2025 Adrian Goldner

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

---

## 📞 Support

- **GitHub Issues:** https://github.com/adriangoldner/bmad-method/issues
- **Documentation:** `/docs/cflow-*.md`
- **Website:** https://adriangoldner.com
- **Email:** [contact@adriangoldner.com](mailto:contact@adriangoldner.com)

---

**Built with ❤️ using the BMAD Method Framework**

_ContentFlow - Authentic Content at Scale_
