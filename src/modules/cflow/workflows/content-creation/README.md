# Content Creation Workflow

**Interview-basierter Content-Produktions-Workflow mit KI-Agenten-Flotte**

**Typ:** Interactive Workflow
**Dauer:** 3-5 Tage (inkl. Human-in-Loop)
**Output:** Published Newsletter + SEO-Artikel

---

## 🎯 Zweck

Dieser Workflow orchestriert den kompletten Content-Erstellungsprozess von der Keyword-Recherche bis zum Publishing - alles dabei preserving der authentischen Stimme des Autors durch strukturierte Interviews.

**Ideal für:**

- Wöchentliche Content-Produktion
- Newsletter-First Strategie
- SEO-optimierten Website-Content
- Multi-Platform Distribution

---

## 🔄 Workflow-Übersicht

```
1. SEO-STRATEGIST → Content-Briefing (30 Min)
2. INTERVIEWER → Angle Selection (15 Min)
3. INTERVIEWER → Interview Phase (30-60 Min User-Time)
4. INTERVIEWER → Deep-Dive (15 Min User-Time)
5. INTERVIEWER → Interview Protocol (automatisch)
6. WRITER → Draft Creation (automatisch, 2-3 Std)
7. VALIDATOR → Quality Check (automatisch, 15 Min)
8. USER APPROVAL → Final Review (10-20 Min User-Time)
9. PUBLISHER → Publishing (automatisch, 5 Min)
10. SOCIAL → Auto-Repurposing (optional, 15 Min)
```

**Gesamte User-Zeit:** ~1.5-2 Stunden verteilt über 3-5 Tage
**System-Zeit:** Automatisch zwischendurch

---

## 📋 Benötigte Ressourcen

### Erforderliche Dateien (müssen vorhanden sein):

- `topic-map-master.yaml` - Master Topic-Map mit Pillars & Clusters
- `tone-of-voice-guide.md` - 65-seitiger ToV-Guide
- `gsc-exports/latest.csv` - Google Search Console Export (letzter Monat)
- `authenticity-scorer.xml` - Validierungs-Task für AI-Fingerprinting

### Erforderliche Agenten:

- `seo-strategist.md` - Topic Research & Keyword-Analyse
- `content-interviewer.md` - Interview-Führung & Protokoll
- `content-writer.md` - Newsletter & SEO-Artikel-Erstellung
- `quality-validator.md` - SEO & Authentizitäts-Validierung
- `content-publisher.md` - Webflow & Brevo Publishing
- `social-distributor.md` - Multi-Platform Social Content

### Erforderliche API-Keys:

- Google Search Console API
- Webflow API (Publishing)
- Brevo API (Newsletter)
- Optional: Social Media Scheduler API

---

## 🚀 Nutzung

### Start des Workflows:

```bash
# Via Slash-Command
/cflow:workflow:content-creation

# Oder direkter Agent-Aufruf
/cflow:seo-strategist
```

### Vorbereitung:

1. **Topic-Map sicherstellen:**

   ```bash
   cp bmad/cflow/data/topic-maps/example-topic-map.yaml \
      bmad/cflow/data/topic-maps/topic-map-master.yaml
   # Editieren mit deinen Pillars & Clusters
   ```

2. **GSC-Daten vorbereiten:**
   - Exportiere letzte 30 Tage als CSV
   - Speichere als `bmad/cflow/data/gsc-exports/latest.csv`

3. **API-Keys konfigurieren:**
   - Prüfe `bmad/cflow/config.yaml` für API-Keys
   - Teste API-Connectivity vor Start

---

## 🎭 Human-in-Loop Punkte

### 1. Angle Selection (Step 2)

- System präsentiert 4-6 kreative Artikel-Angles
- Du wählst 1-2 favorisierte Ansätze
- Dauer: 5-10 Minuten

### 2. Interview Phase (Steps 4-5)

- 10-15 strukturierte Fragen über Telegram/Notion
- 2-3 Deep-Dive Nachfragen
- Dauer: 30-60 Minuten

### 3. Final Approval (Step 9)

- Newsletter + SEO-Artikel werden gezeigt
- Validierungs-Report mit Scores
- Publishing-Entscheidung
- Dauer: 10-20 Minuten

---

## 📊 Output-Dateien

Alle Dateien werden im `{output_folder}` gespeichert (standardmäßig `docs/`):

- `content-briefing-{date}.md` - SEO-Analyse und Strategie
- `interview-protocol-{date}.md` - Komplettes Interview-Protokoll
- `newsletter-draft-{date}.md` - Newsletter-Entwurf
- `seo-article-draft-{date}.md` - SEO-Artikel-Entwurf
- `validation-report-{date}.md` - Qualitäts-Validierung
- `publishing-log-{date}.md` - Publishing-Ergebnisse

---

## ⚙️ Konfiguration

### Wichtige Settings in `workflow.yaml`:

```yaml
# Validierung
authenticity_min_score: 71 # Mindest-Score für Publishing
max_validation_iterations: 2 # Max. Revisionen

# Interview-Konfiguration
interview_platform: 'telegram' # telegram | notion | manual

# Publishing
auto_schedule_social: false # Social Media automatisch planen
```

### Customization:

- **Authenticity-Score** anpassen in `config.yaml`
- **Interview-Plattform** ändern bei Bedarf
- **Social Platforms** in `config.yaml` konfigurieren

---

## 🛠️ Troubleshooting

### "Topic-Map nicht gefunden"

```bash
# Kopiere Example als Basis
cp bmad/cflow/data/topic-maps/example-topic-map.yaml \
   bmad/cflow/data/topic-maps/topic-map-master.yaml
```

### "Authenticity-Score zu niedrig"

- Interview-Antworten waren zu generisch
- Neu interviewen mit konkreteren Beispielen
- Score-Schwelle in config.yaml senken

### "Webflow Publishing fehlgeschlagen"

- API-Key in config.yaml prüfen
- Webflow Berechtigungen überprüfen
- Netzwerk-Verbindung sicherstellen

### "Keine Social-Posts erstellt"

- `auto_schedule_social: true` setzen
- Social Platform APIs in config.yaml eintragen

---

## 🔄 Integration mit anderen Workflows

### Nachfolgende Workflows:

- **Social-Repurposing Workflow** - Erstellt zusätzliche Social-Assets
- **Performance-Tracking Workflow** - Analysiert Publishing-Ergebnisse

### Vorausgehende Workflows:

- **SEO-Planning Workflow** - Erstellt monatliche Content-Pläne

---

## 📈 Success Metrics

### Qualität:

- Authenticity-Score ≥ 71/100
- SEO-Score ≥ 80/100
- User-Approval Rate ≥ 90%

### Effizienz:

- User-Time ≤ 2 Stunden pro Artikel
- System-Zeit ≤ 4 Stunden
- Publishing-Erfolgsrate ≥ 95%

---

## 🎯 Best Practices

### Interview-Qualität:

- Konkrete Beispiele aus der Praxis teilen
- Persönliche Meinungen aussprechen
- Anekdoten erzählen (machen Content authentisch)

### Content-Strategie:

- Newsletter-First Ansatz beibehalten
- Interne Links systematisch einbauen
- Topic-Authorität schrittweise aufbauen

### Workflow-Optimierung:

- Konsistente Cadence einhalten
- Validierungs-Reports ernst nehmen
- Social Distribution automatisieren

---

## 📞 Support

**Issues:** GitHub Issues im BMAD Repository
**Documentation:** `/docs/cflow-*.md` Dateien
**Help:** Agent-spezifische READMEs in `/agents/`

---

**Built with ❤️ using the BMAD Method Framework**

_Content Creation Workflow - Authentic Content at Scale_
