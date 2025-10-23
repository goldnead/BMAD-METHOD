# ContentFlow Modul - Komponenten-Planung

**Erstellungsdatum:** 2025-10-22
**Erstellt von:** Adrian Goldner
**Modul:** ContentFlow (cflow)

---

## Agenten-Architektur (7 Agenten)

### 1. SEO-Strategist Agent

**Agent-Typ:** Expert Agent
**Rolle:** Topic Research & Keyword-Analyse
**Primäre Verantwortung:** Identifiziert welche Themen/Keywords als nächstes bespielt werden

**Verantwortlichkeiten:**

- Analysiert Google Search Console Daten (Impressions, CTR, Position)
- Identifiziert Quick-Win Keywords (hohe Impressions + niedrige CTR)
- Erstellt strukturierte Topic-Briefings für Content-Team
- Priorisiert Themen nach Suchpotenzial & Funnel-Fit
- Verwaltet Topic-Map & Pillar-Cluster-Struktur
- Weist Keywords den richtigen Funnel-Phasen zu (Awareness/Consideration/Conversion)

**Inputs:**

- Google Search Console Export (CSV/API)
- Bestehende Topic-Map (YAML/Markdown)
- Funnel-Zuordnung (welches Keyword → welche Phase)

**Outputs:**

- Content-Briefing (Markdown-Dokument)
  - Keyword-Fokus
  - Funnel-Phase
  - Ziel-CTA
  - Priorität (1-5)
  - Verwandte Cluster-Artikel für interne Verlinkung

**Interaktion mit anderen Agenten:**

- Liefert Briefings an Content-Interviewer
- Erhält Performance-Daten von Analytics-Reporter
- Nutzt Internal-Link-Finder Task

---

### 2. Content-Interviewer Agent

**Agent-Typ:** Expert Agent
**Rolle:** Wissensextraktion durch strukturierte Interviews
**Primäre Verantwortung:** Extrahiert authentisches Wissen von Adrian durch intelligente Fragetechnik

**Verantwortlichkeiten:**

- Entwickelt 4-6 Artikel-Angles pro Thema
- Generiert Interview-Fragenkatalog (10-15 Hauptfragen)
- Führt Dialog mit Adrian (Human-in-the-Loop)
- Stellt intelligente Nachfragen zu interessanten Antworten
- Speichert vollständiges Interview-Transkript
- Markiert besonders starke Anekdoten/Beispiele

**Inputs:**

- Content-Briefing vom SEO-Strategist
- Tone-of-Voice Guide
- Frühere Interview-Protokolle (für Konsistenz)

**Outputs:**

- 4-6 Artikel-Angles (zur User-Auswahl)
- Interview-Protokoll mit:
  - Alle Fragen & Antworten
  - Hervorgehobene Anekdoten
  - Persönliche Beispiele aus der Praxis
  - Meinungen & kontroverse Standpunkte
  - Praxistipps & Übungen

**Interaktion mit anderen Agenten:**

- Erhält Briefing vom SEO-Strategist
- Liefert Interview-Protokoll an Content-Writer
- **Human-Interaction:** Dialog mit Adrian via Telegram/Notion

---

### 3. Content-Writer Agent

**Agent-Typ:** Expert Agent
**Rolle:** Artikel-Erstellung nach SOP & Tone-of-Voice
**Primäre Verantwortung:** Schreibt authentischen Content in Adrians Stimme

**Verantwortlichkeiten:**

- Schreibt Newsletter-Version (Email-optimiert, persönlich)
- Schreibt SEO-Cluster-Artikel (Webflow-Format, strukturiert)
- Befolgt Tone-of-Voice-Richtlinien strikt:
  - Weichmacher verwenden ("vielleicht", "irgendwie")
  - Persönliche Anekdoten integrieren
  - Direkte Leseransprache ("du")
  - Anti-AI-Detection-Guidelines befolgen
- Integriert Interview-Inhalte authentisch
- Fügt 2 interne Links ein (1 zu Pillar, 1 zu Cluster)
- Erstellt passende CTAs basierend auf Funnel-Phase
- Strukturiert nach bewährten Mustern:
  - Hook (Problem/Aha-Moment)
  - Erklärung mit Fachbezug
  - Praxisbeispiel
  - 3 konkrete Handlungsschritte
  - CTA

**Inputs:**

- Interview-Protokoll vom Content-Interviewer
- Content-Briefing (Keyword, Funnel-Phase, CTA)
- Tone-of-Voice-Guide (65-seitiges Dokument)
- Internal-Link-Vorschläge (von Task)

**Outputs:**

- Newsletter-Version (Markdown, 800-1200 Wörter)
- SEO-Artikel-Version (Markdown, 1000-1500 Wörter für Cluster)
- Meta-Daten (Title 55-65 Zeichen, Description 140-155 Zeichen)
- Vorschlag für Featured Image

**Interaktion mit anderen Agenten:**

- Erhält Input von Content-Interviewer
- Output geht zu Quality-Validator
- Nutzt Internal-Link-Finder Task

---

### 4. Quality-Validator Agent

**Agent-Typ:** Expert Agent
**Rolle:** SEO & Authentizitäts-Validierung
**Primäre Verantwortung:** Stellt sicher, dass Content SEO-konform UND authentisch klingt

**Verantwortlichkeiten:**

**SEO-Checks:**

- Title: 55-65 Zeichen, Keyword am Anfang ✓
- Meta-Description: 140-155 Zeichen mit CTA ✓
- H1-Struktur: Exakt 1× H1 ✓
- H2-Struktur: 3-5× H2 ✓
- Keyword-Density: 0,8-1,5% ✓
- Interne Links: Mindestens 2 vorhanden ✓
- Alt-Tags: Alle Bilder beschrieben ✓
- Content-Länge: >1000 Wörter (Cluster), >2500 (Pillar) ✓
- CTA-Blöcke: Mind. 1 CTA im Text ✓
- Lesbarkeit: Durchschnittliche Satzlänge < 17 Wörter ✓

**Authentizitäts-Checks:**

- Mind. 1 persönliche Anekdote vorhanden ✓
- Erfahrungs-Reflexion enthalten ("Früher..., Heute...") ✓
- Mind. 1 direkte Leserfrage ✓
- Weichmacher verwendet ("vielleicht", "irgendwie") ✓
- KEINE AI-Fingerprints:
  - ❌ Contrast-Framing Overload ("Es geht nicht um X, sondern um Y")
  - ❌ Dreier-Regel-Übertreibung
  - ❌ Infomercial-Übergänge ("Die brutale Wahrheit?", "Das Geheimnis?")
  - ❌ Corporate -ing Verben
  - ❌ Vage Füllphrasen ("Es ist wichtig zu erwähnen...")
  - ❌ Formelle Sprache ("implementieren", "optimieren")
  - ❌ Emoji-Overload (max. 1-2 pro Text)
- Keine Marketing-Buzzwords ("aufs nächste Level", "bombastisch")
- Narrative Produkterwähnung (nicht verkaufsorientiert)

**Inputs:**

- Content-Drafts vom Writer (Newsletter + SEO-Artikel)
- Tone-of-Voice-Guide
- SEO-Checkliste

**Outputs:**

- Validation-Report:
  - Status: GO / NO-GO
  - SEO-Score (0-100)
  - Authenticity-Score (0-100)
  - Liste aller Probleme mit Zeilennummern
  - Konkrete Verbesserungsvorschläge
  - Wenn NO-GO: Zurück an Writer mit Feedback

**Interaktion mit anderen Agenten:**

- Erhält Drafts von Content-Writer
- Sendet validated Content an Content-Publisher
- Bei NO-GO: Feedback zurück an Content-Writer
- Nutzt Authenticity-Scorer Task

---

### 5. Content-Publisher Agent

**Agent-Typ:** Simple Agent
**Rolle:** Veröffentlichung in Webflow & Newsletter
**Primäre Verantwortung:** Technische Veröffentlichung auf allen Plattformen

**Verantwortlichkeiten:**

- Konvertiert Markdown zu Webflow-HTML
- Fügt JSON-LD Schema ein:
  - Article Schema (für Blog-Posts)
  - FAQ Schema (bei Q&A-Abschnitten)
  - Breadcrumb Schema
- Uploaded zu Webflow CMS via API
- Sendet Newsletter via Brevo API
- Pingt Google Search Console zur Indexierung
- Erstellt Canonical URLs
- Setzt Publish-Datum
- Aktiviert Plausible.io Event-Tracking

**Inputs:**

- Validated Content vom Quality-Validator
- Webflow API-Credentials
- Brevo API-Credentials
- Schema-Templates

**Outputs:**

- Published Webflow-Artikel (URL)
- Versendeter Newsletter (Brevo Campaign-ID)
- GSC Index-Request Confirmation
- Plausible Event Setup Confirmation

**Interaktion mit anderen Agenten:**

- Erhält validated Content vom Quality-Validator
- Triggert Social-Distributor Agent (Webhook)
- Nutzt Schema-Generator Task

---

### 6. Social-Distributor Agent

**Agent-Typ:** Expert Agent
**Rolle:** Multi-Platform Social Content Repurposing
**Primäre Verantwortung:** Transformiert jeden Artikel in 5 Social-Media-Assets

**Verantwortlichkeiten:**

**Erstellt für jedes veröffentlichte Artikel:**

1. **LinkedIn (2 Formate):**
   - Educational Mini-Post (150-200 Wörter, Hook + Insight + CTA)
   - Carousel-Zusammenfassung (5-7 Slides, visuell)

2. **Instagram (3 Formate):**
   - Reel-Script (30-60 Sekunden, Hook + 3 Punkte + CTA)
   - Karussell-Post (5 Slides mit Key-Takeaways)
   - Quote-Grafik (1 starkes Zitat aus Artikel)

3. **X/Threads (Micro-Thread):**
   - 5-7 Tweets mit rotem Faden
   - Hook-Tweet + 3-5 Insights + CTA-Tweet

4. **Facebook:**
   - Story-Format mit persönlichem Touch
   - Längerer Text (300-400 Wörter) mit Anekdote

**Einhält dabei:**

- Gleichbleibende Tonality (Adrians Voice)
- Plattform-spezifische Best Practices
- Passende CTAs & Links
- Hashtag-Strategie

**Plant Veröffentlichungs-Timing:**

- LinkedIn: Dienstag/Mittwoch 08:00-10:00
- Instagram: Täglich verteilt 18:00-20:00
- X: Über 3 Tage verteilt (Vormittags)
- Facebook: Wochenende 10:00-12:00

**Inputs:**

- Published Artikel-URL vom Publisher
- Artikel-Content (Markdown)
- Social-Media-Strategie-Dokument
- Tone-of-Voice-Guide

**Outputs:**

- 5 formatierte Social-Media-Posts
- Scheduling-Plan (Datum/Uhrzeit pro Plattform)
- Optional: Canva-Design-Vorlagen für Karussells/Quotes

**Interaktion mit anderen Agenten:**

- Wird getriggert von Content-Publisher (Webhook)
- Liefert Performance-Daten an Analytics-Reporter

---

### 7. Analytics-Reporter Agent

**Agent-Typ:** Simple Agent
**Rolle:** KPI-Tracking & Reporting
**Primäre Verantwortung:** Sammelt alle Performance-Daten und erstellt monatliche Reports

**Verantwortlichkeiten:**

**Datensammlung (monatlich) von:**

- **Google Search Console:**
  - Klicks, Impressions, CTR, Avg Position
  - Pro Artikel & aggregiert
- **Plausible.io:**
  - Pageviews, Sessions, Bounce Rate
  - Scrolltiefe, Session-Dauer
  - Conversion-Events (Newsletter-Signups)
- **Brevo:**
  - Newsletter-Opt-ins
  - Open-Rate, Click-Rate
  - Conversion zu Trials
- **Thrivecart:**
  - Trial-Starts (7€)
  - VocalEssentials Käufe
  - ProGroup Upgrades
- **Social Media:**
  - Impressions, Engagement Rate
  - Follower-Wachstum

**Aggregation & Analyse:**

- Erstellt KPI-Dashboard (Notion/Airtable)
- Berechnet Veränderungen vs. Vormonat
- Identifiziert Top-3-Performer
- Identifiziert Underperformer

**Report-Generierung:**

- Monatlicher Markdown-Report mit:
  - Executive Summary (3-5 Bullet Points)
  - SEO-Performance (Traffic, Rankings, CTR)
  - Lead-Generierung (Newsletter-Signups, Quelle)
  - Conversion-Funnel (Trials, Käufe)
  - Top-Content (Top 3 Artikel mit Metriken)
  - Empfehlungen (basierend auf Daten)

**Inputs:**

- API-Credentials für alle Plattformen
- Zeitraum (standardmäßig letzter Monat)
- Vormonatsdaten (für Vergleiche)

**Outputs:**

- Monthly-Analytics-Report.md
- Telegram-Notification an Adrian
- Updated Airtable/Notion Dashboard
- Optional: Optimierungs-Empfehlungen für SEO-Strategist

**Interaktion mit anderen Agenten:**

- Liefert Daten an SEO-Strategist (für Topic-Priorisierung)
- Erhält Trigger monatlich (1. des Monats, 09:00)

---

## Workflows-Architektur (4 Workflows)

### Workflow 1: Content-Creation

**Workflow-Typ:** Interactive Workflow (Multi-Step mit Human-in-Loop)
**Ziel:** Von Topic-Briefing zu published Artikel
**Durchlaufzeit:** 3-5 Tage (inkl. User-Interaktion)

**Workflow-Schritte:**

**Phase 1: Topic Selection**

1. SEO-Strategist → Topic-Briefing erstellen
   - Lädt GSC-Daten
   - Analysiert Quick-Wins
   - Erstellt Content-Briefing
2. Content-Interviewer → Artikel-Angles präsentieren
   - Entwickelt 4-6 Angles
   - Präsentiert zur User-Auswahl
3. **[USER INPUT]** Adrian wählt 1-2 Angles aus

**Phase 2: Knowledge Extraction** 4. Content-Interviewer → Interview-Fragen stellen

- Stellt 10-15 Hauptfragen
- **[USER INPUT]** Adrian antwortet (Telegram/Notion)
- Stellt 2-3 Deep-Dive-Nachfragen
- **[USER INPUT]** Adrian antwortet

5. Content-Interviewer → Interview-Protokoll erstellen
   - Speichert alle Antworten
   - Markiert starke Anekdoten

**Phase 3: Content Creation** 6. Content-Writer → Draft erstellen

- Newsletter-Version schreiben
- SEO-Artikel-Version schreiben
- Meta-Daten generieren
- Interne Links einfügen

**Phase 4: Quality Control** 7. Quality-Validator → Prüfung durchführen

- SEO-Check (10 Kriterien)
- Authentizitäts-Check (8 Kriterien)
- Validation-Report erstellen

**Phase 5: Iteration (wenn nötig)** 8. **[IF NO-GO]** → Zurück zu Writer mit Feedback

- Writer überarbeitet
- Validator prüft erneut
- Loop max. 2×

**Phase 6: Approval & Publishing** 9. **[USER APPROVAL]** Zeige finale Drafts

- "Artikel veröffentlichen?" (Ja/Nein/Edit)

10. Content-Publisher → Veröffentlichung durchführen
    - Webflow-Upload
    - Newsletter-Versand
    - GSC-Index-Request

**Inputs:**

- GSC-Export
- Topic-Map
- Tone-of-Voice-Guide

**Outputs:**

- Published Newsletter
- Published SEO-Artikel (Webflow)
- Interview-Protokoll (für Archiv)

**Human-Touchpoints:** 3. Angle-Auswahl 4. Interview-Antworten (10-15 Fragen + 2-3 Nachfragen) 9. Final Approval

---

### Workflow 2: Social-Repurposing

**Workflow-Typ:** Action Workflow (weitgehend automatisiert)
**Ziel:** Aus jedem publizierten Artikel Social-Content erstellen
**Durchlaufzeit:** 1-2 Stunden (automatisch)

**Workflow-Schritte:**

1. **Trigger:** Neuer Artikel published (Webhook vom Publisher)
2. Social-Distributor → Artikel-Content laden
3. Social-Distributor → 5 Social-Assets erstellen:
   - LinkedIn: Mini-Post + Carousel
   - Instagram: Reel-Script + Karussell + Quote
   - X/Threads: Micro-Thread (5-7 Tweets)
   - Facebook: Story-Format
4. Social-Distributor → Scheduling-Plan erstellen
   - Optimale Zeitpunkte pro Plattform
5. **[OPTIONAL USER REVIEW]** Zeige Previews
   - Adrian kann Posts reviewen vor Auto-Post
   - Oder direkt auto-schedulen
6. Scheduler → Posts planen (via Publer/Metricool API)

**Inputs:**

- Published Artikel-URL
- Artikel-Content (Markdown)
- Social-Media-Strategie

**Outputs:**

- 5 Social-Media-Posts (formatiert)
- Scheduling-Plan (CSV)
- Scheduled Posts (in Publer/Metricool)

**Human-Touchpoints:** 5. [Optional] Preview-Review

---

### Workflow 3: SEO-Planning

**Workflow-Typ:** Document Workflow (generiert monatlichen Plan)
**Ziel:** Monatlichen Content-Kalender mit 4-8 Topics erstellen
**Durchlaufzeit:** 30-60 Minuten

**Workflow-Schritte:**

1. SEO-Strategist → GSC-Daten analysieren
   - Lädt letzten Monat GSC-Export
   - Identifiziert Trends (steigende/fallende Keywords)
2. SEO-Strategist → Quick-Wins identifizieren
   - Keywords mit hohen Impressions + niedrige CTR
   - Keywords Position 11-20 (Ranking-Potential)
3. SEO-Strategist → Topic-Prioritäten setzen
   - Priorisierungs-Matrix anwenden:
     - Suchpotenzial (Impressions)
     - Funnel-Potenzial (Conversion-Nähe)
     - Aufwand (Keyword-Difficulty)
   - Sortiert Topics nach Priorität 1-5
4. SEO-Strategist → Content-Kalender generieren
   - 4-8 Topics für nächsten Monat
   - Jeweils mit Content-Briefing:
     - Keyword-Fokus
     - Funnel-Phase
     - Empfohlene CTAs
     - Verwandte Cluster (für interne Links)
5. SEO-Strategist → Output als Markdown-Dokument
   - Template: `monthly-content-plan-template.md`
   - Saved to: `{output_folder}/content-plan-{YYYY-MM}.md`

**Inputs:**

- GSC-Export (letzter Monat)
- Bestehende Topic-Map (YAML)
- Funnel-Zuordnung (JSON)

**Outputs:**

- `monthly-content-plan-{YYYY-MM}.md`
  - Liste von 4-8 Content-Briefings
  - Priorisiert nach Impact
  - Mit empfohlener Reihenfolge

**Template-Datei:**
`{installed_path}/templates/monthly-content-plan-template.md`

**Beispiel-Output:**

```markdown
# Content Plan - November 2025

## Quick-Win Keywords (Priorität 1)

1. **"stimmanalyse online"** (98 Impressions, CTR 11.22%, Position 3.82)
   - Funnel: Consideration
   - CTA: 7€ Trial + Stimmanalyse Call
   - Interne Links: "Was ist Stimmtechnik", "CVT-Übungen"

2. **"stimme versagt bei hohen tönen"** (121 Impressions, CTR 0%, Position 10.84)
   - Funnel: Awareness
   - CTA: Newsletter + Lead-Magnet
   - Interne Links: "Gesangstechnik & CVT", "Vokaltrapez"

## Medium Priority (Priorität 2-3)

[...]
```

**Human-Touchpoints:**

- Keine (vollautomatisch)
- Optional: Review & Anpassung des Plans

---

### Workflow 4: Performance-Tracking

**Workflow-Typ:** Action Workflow (monatlich getriggert)
**Ziel:** Alle KPIs sammeln, aggregieren und reporten
**Durchlaufzeit:** 15-30 Minuten

**Workflow-Schritte:**

1. **Trigger:** Monatlich (1. des Monats, 09:00 Uhr via Cron)
2. Analytics-Reporter → Daten von APIs holen:
   - Google Search Console API (Klicks, Impressions, CTR)
   - Plausible.io API (Traffic, Events, Conversions)
   - Brevo API (Newsletter-Stats, Leads)
   - Thrivecart API (Trial-Starts, Käufe)
   - Metricool API (Social Media Stats)
3. Analytics-Reporter → Daten aggregieren
   - Schreibt in Airtable/Notion Dashboard
   - Berechnet Deltas vs. Vormonat
   - Identifiziert Top-3 & Bottom-3 Artikel
4. Analytics-Reporter → Report generieren
   - Template: `monthly-analytics-report-template.md`
   - Füllt mit aktuellen Daten
   - Generiert Insights & Empfehlungen
5. Analytics-Reporter → Report versenden
   - Saved to: `{output_folder}/analytics-report-{YYYY-MM}.md`
   - Telegram-Notification an Adrian
   - Optional: Email-Summary
6. **[OPTIONAL]** SEO-Strategist → Optimierungsempfehlungen
   - Liest Analytics-Report
   - Identifiziert Underperformer
   - Schlägt Content-Refreshes vor

**Inputs:**

- API-Credentials (alle Plattformen)
- Zeitraum: Letzter Monat (automatisch)
- Vormonatsdaten (für Vergleiche)

**Outputs:**

- `analytics-report-{YYYY-MM}.md`
- Updated Notion/Airtable Dashboard
- Telegram-Notification
- [Optional] Optimization-Recommendations.md

**Template-Datei:**
`{installed_path}/templates/monthly-analytics-report-template.md`

**Beispiel-Output:**

```markdown
# 📊 Analytics Report - Oktober 2025

## Executive Summary

- ✅ +24% organische Klicks (GSC)
- ✅ +38 neue Newsletter-Abos
- ✅ 12 neue 7€ Trials
- ⚠️ -5% Social Engagement (Instagram down)

## SEO Performance

- Klicks: 1.245 (+24% vs. Sep)
- Impressions: 38.920 (+18%)
- CTR: 3.2% (+0.4pp)
- Neue Top-10 Rankings: 3

## Top Content

1. "Warum sich manche Stimmen nicht mischen" - 310 Klicks
2. "Stimmanalyse Online" - 278 Klicks
3. "Was ist das Vokaltrapez?" - 190 Klicks

[...]
```

**Human-Touchpoints:**

- Keine (vollautomatisch)
- Optional: Review des Reports

---

## Tasks-Architektur (3 Utility Tasks)

### Task 1: Schema-Generator

**Task-Typ:** Standalone Utility Task
**Zweck:** Generiert JSON-LD Schema-Markup für verschiedene Content-Typen

**Unterstützte Schema-Typen:**

- Article Schema (Blog-Posts)
- FAQ Schema (Q&A-Abschnitte)
- Product Schema (VocalEssentials, Coaching)
- Breadcrumb Schema (Navigation)

**Inputs:**

- Schema-Typ (article/faq/product/breadcrumb)
- Artikel-Metadaten:
  - title
  - description
  - author (default: "Adrian Goldner")
  - datePublished
  - canonical_url
  - [für FAQ] questions & answers (Array)
  - [für Product] name, price, currency, availability

**Outputs:**

- JSON-LD Code-Block (string)
- Ready für Webflow Custom Code einbetten

**Verwendung:**

- Wird genutzt von Content-Publisher Agent
- Kann auch standalone aufgerufen werden

**Beispiel-Aufruf:**

```yaml
task: schema-generator
input:
  type: article
  title: 'Wie du deine Stimme objektiv einschätzen lernst'
  description: 'Stimmanalyse für Chorsänger erklärt'
  datePublished: '2025-10-22'
  canonical_url: 'https://adriangoldner.com/newsletter/stimmanalyse'
output: |
  <script type="application/ld+json">
  {
    "@context": "https://schema.org",
    "@type": "Article",
    "headline": "Wie du deine Stimme objektiv einschätzen lernst",
    ...
  }
  </script>
```

---

### Task 2: Internal-Link-Finder

**Task-Typ:** Standalone Utility Task
**Zweck:** Findet passende interne Verlinkungsmöglichkeiten aus Topic-Map

**Strategie:**

- Sucht thematisch verwandte Artikel
- Priorisiert 1× Link zu Pillar-Artikel
- Priorisiert 1× Link zu Cluster-Artikel
- Findet 5-10 zusätzliche relevante Links
- Sortiert nach Relevanz-Score

**Inputs:**

- Artikel-Thema/Keyword
- Artikel-Typ (pillar/cluster)
- Topic-Map (alle bestehenden Artikel mit Keywords)

**Outputs:**

- Liste von 5-10 internen Links:
  - Link-URL (relativ)
  - Link-Text (Anchor-Text-Vorschlag)
  - Relevanz-Score (0-100)
  - Typ (pillar/cluster)
  - Begründung ("Weil beide über Intonation handeln")

**Verwendung:**

- Wird genutzt von Content-Writer Agent
- Kann auch standalone aufgerufen werden

**Beispiel-Aufruf:**

```yaml
task: internal-link-finder
input:
  topic: "Stimmanalyse für Chorsänger"
  keyword: "stimmanalyse"
  article_type: cluster
  topic_map: {project-root}/bmad/cflow/data/topic-map.yaml
output:
  links:
    - url: "/gesangstechnik-chor"
      anchor: "Gesangstechnik & CVT im Chor"
      relevance: 95
      type: pillar
      reason: "Hauptthema Stimmtechnik"
    - url: "/newsletter/cvt-uebungen"
      anchor: "Die 5 effektivsten CVT-Übungen"
      relevance: 88
      type: cluster
      reason: "Praktische Anwendung nach Analyse"
    [...]
```

---

### Task 3: Authenticity-Scorer

**Task-Typ:** Standalone Utility Task
**Zweck:** Bewertet Text auf AI-Fingerprints und Authentizität (0-100 Score)

**Prüft auf AI-Fingerprints:**

- ❌ Contrast-Framing ("Es geht nicht um X, sondern um Y") → -10 Punkte
- ❌ Dreier-Regel-Overload (>5 Dreiergruppen) → -5 Punkte pro Extra
- ❌ Infomercial-Übergänge ("Die brutale Wahrheit?") → -10 Punkte
- ❌ Corporate -ing Verben ("implementing", "facilitating") → -5 Punkte
- ❌ Vage Füllphrasen ("Es ist wichtig zu erwähnen") → -5 Punkte
- ❌ Formelle Sprache ("implementieren", "optimieren") → -3 Punkte
- ❌ Emoji-Overload (>2 Emojis) → -5 Punkte
- ❌ Symbol-Sprache ("Das repräsentiert...") → -5 Punkte

**Prüft auf Authentizitäts-Marker:**

- ✅ Persönliche Anekdote vorhanden → +15 Punkte
- ✅ Erfahrungs-Reflexion ("Früher..., Heute...") → +10 Punkte
- ✅ Direkte Leserfrage → +10 Punkte
- ✅ Weichmacher verwendet → +5 Punkte
- ✅ Narrative Produkterwähnung → +10 Punkte

**Inputs:**

- Text (string, Artikel-Content)
- Tone-of-Voice-Guide (optional, für zusätzliche Checks)

**Outputs:**

- Authenticity-Score (0-100)
  - 0-50: Stark AI-generiert, komplett überarbeiten
  - 51-70: Moderate AI-Fingerprints, Überarbeitung empfohlen
  - 71-85: Gut, kleinere Anpassungen
  - 86-100: Exzellent authentisch
- Liste erkannter Probleme:
  - Problem-Typ
  - Zeilennummer/Textstelle
  - Verbesserungsvorschlag
- Liste positiver Marker (was gut funktioniert)

**Verwendung:**

- Wird genutzt von Quality-Validator Agent
- Kann auch standalone aufgerufen werden

**Beispiel-Aufruf:**

```yaml
task: authenticity-scorer
input:
  text: |
    Es geht nicht um Perfektion, es geht um Fortschritt.
    Viele Chorsänger denken, dass sie...
    [vollständiger Artikel-Text]
output:
  score: 72
  status: 'Gut - kleinere Anpassungen empfohlen'
  problems:
    - type: 'Contrast-Framing'
      line: 1
      text: 'Es geht nicht um Perfektion, es geht um Fortschritt'
      suggestion: "Ersetze durch: 'Fortschritt ist wichtiger als Perfektion'"
    - type: 'Fehlende Anekdote'
      suggestion: 'Füge persönliche Geschichte aus der Praxis hinzu'
  positive_markers:
    - 'Direkte Leserfrage in Zeile 23'
    - "Weichmacher 'vielleicht' verwendet in Zeile 45"
    - 'Erfahrungs-Reflexion in Zeile 67'
```

---

## Komponenten-Zusammenfassung

### Agenten-Übersicht

| Agent               | Typ    | Primäre Rolle       | Input                | Output                   |
| ------------------- | ------ | ------------------- | -------------------- | ------------------------ |
| SEO-Strategist      | Expert | Topic Research      | GSC-Daten, Topic-Map | Content-Briefing         |
| Content-Interviewer | Expert | Wissensextraktion   | Briefing             | Interview-Protokoll      |
| Content-Writer      | Expert | Artikel-Erstellung  | Interview, ToV-Guide | Newsletter + SEO-Artikel |
| Quality-Validator   | Expert | SEO & Authentizität | Drafts               | Validation-Report        |
| Content-Publisher   | Simple | Veröffentlichung    | Validated Content    | Published URLs           |
| Social-Distributor  | Expert | Social Repurposing  | Published Artikel    | 5 Social-Posts           |
| Analytics-Reporter  | Simple | KPI-Tracking        | API-Daten            | Monthly Report           |

### Workflows-Übersicht

| Workflow             | Typ         | Dauer     | Human-Touchpoints              | Output                   |
| -------------------- | ----------- | --------- | ------------------------------ | ------------------------ |
| Content-Creation     | Interactive | 3-5 Tage  | 3 (Angle, Interview, Approval) | Published Content        |
| Social-Repurposing   | Action      | 1-2 Std   | 1 (Optional Review)            | 5 Social-Posts           |
| SEO-Planning         | Document    | 30-60 Min | 0 (Optional Review)            | Monthly Content-Plan     |
| Performance-Tracking | Action      | 15-30 Min | 0                              | Monthly Analytics-Report |

### Tasks-Übersicht

| Task                 | Zweck                  | Verwendet von     | Output           |
| -------------------- | ---------------------- | ----------------- | ---------------- |
| Schema-Generator     | JSON-LD erstellen      | Content-Publisher | Schema Code      |
| Internal-Link-Finder | Relevante Links finden | Content-Writer    | Link-Liste       |
| Authenticity-Scorer  | AI-Detection           | Quality-Validator | Score + Probleme |

---

## Nächste Schritte

1. **Modul-Komplexität bestimmen** (Simple/Standard/Complex)
2. **Verzeichnisstruktur erstellen**
3. **Konfigurationsfelder planen**
4. **Ersten Agent entwickeln** (empfohlen: SEO-Strategist)
5. **Ersten Workflow implementieren** (empfohlen: Content-Creation)
