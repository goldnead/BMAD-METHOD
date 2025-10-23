# SEO Planning Workflow

**Monatliche Content-Planung basierend auf GSC-Datenanalyse, Topic-Map Review und Priority-Matrix für strategische SEO-Content-Entwicklung**

**Typ:** Document Workflow
**Dauer:** 30-60 Minuten
**Output:** Monthly Content Plan

---

## 🎯 Zweck

Dieser Workflow erstellt datengestützte, strategische Content-Pläne basierend auf Performance-Analyse, Topic-Map Review und priorisierter Keyword-Recherche. Er stellt sicher, dass Content-Erstellung auf business-relevanten, SEO-optimierten Themen basiert.

**Ideal für:**

- Monatliche Content-Strategie-Planung
- Datengetriebene Topic-Selection
- Resource Planning und Zeitmanagement
- SEO-Performance-Optimierung

---

## 🔄 Workflow-Übersicht

```
1. GSC ANALYSIS → Performance Review (15 Min)
2. TOPIC MAP REVIEW → Gap Analysis (15 Min)
3. PRIORITY MATRIX → Topic Ranking (10 Min)
4. CONTENT CALENDAR → 4-Wochen Plan (10 Min)
5. RESOURCE PLANNING → Team & Time (5 Min)
6. USER APPROVAL → Plan Finalisierung (5 Min)
7. IMPLEMENTATION → Vorbereitung (5 Min)
```

**Gesamte User-Zeit:** ~60 Minuten
**System-Zeit:** ~30 Minuten Analyse

---

## 📊 Output-Dokument

### Monthly Content Plan enthält:

- **Executive Summary** mit strategischen Fokusbereichen
- **Performance Review** des Vormonats
- **Topic Map Updates** und Gap-Analyse
- **Priority Matrix Results** mit gerankten Topics
- **Content Calendar** für 4 Wochen
- **Resource Planning** mit Zeitplanung
- **Success Metrics** und KPIs
- **Implementation Plan** mit Meilensteinen

---

## 📋 Benötigte Ressourcen

### Erforderliche Daten:

- `topic-map-master.yaml` - Master Topic-Map mit Pillars & Clusters
- `gsc-exports/current-month.csv` - Aktueller Monat GSC-Daten
- `gsc-exports/previous-month.csv` - Vorheriger Monat für Vergleich
- `monthly-analytics.csv` - Website Analytics Daten
- `priority-matrix.yaml` - Konfiguration für Priority-Berechnung
- `seasonal-trends.csv` - Saisonale Trends und Events

### Erforderliche APIs:

- **Google Search Console API** - Für automatischen Daten-Import
- **Google Analytics API** - Für Traffic- und Conversion-Daten

---

## 🚀 Nutzung

### Start des Workflows:

```bash
# Via Slash-Command
/cflow:workflow:seo-planning

# Manuelles Starten empfohlen am Monatsende
# für die Planung des kommenden Monats
```

### Vorbereitung:

1. **GSC-Daten Exportieren:**
   - Exportiere letzten Monat als CSV
   - Exportiere vorherigen Monat als Vergleich
   - Speichere im gsc-exports Ordner

2. **Analytics Daten vorbereiten:**
   - Exportiere Website Analytics des letzten Monats
   - Speichere als monthly-analytics.csv

3. **Topic-Map aktualisieren:**
   - Prüfe ob topic-map-master.yaml aktuell ist
   - Ergänze neue Topics falls vorhanden

---

## ⚙️ Konfiguration

### Wichtige Settings in `workflow.yaml`:

```yaml
# Planning Parameters
planning_horizon: 'monthly' # monthly | quarterly
content_velocity: 8 # Artikel pro Monat
min_priority_score: 70 # Mindest-Score für Topics

# Priority Matrix Weights
priority_weights:
  search_volume: 0.3 # Keyword-Suchvolumen
  competition: 0.25 # Wettbewerbssituation
  business_value: 0.25 # Geschäftlicher Nutzen
  trending_score: 0.2 # Aktuelle Trends

# Team Configuration
content_team:
  - role: 'Subject Matter Expert'
    name: '{user_name}'
    availability: '30 hours/month'
```

### Customization:

- **Content Velocity:** Anzahl geplanter Artikel pro Monat anpassen
- **Priority Weights:** Je nach Business-Fokus anpassen
- **Planning Horizon:** Quarterly für langfristige Planung
- **Team Availability:** Realistische Kapazitäten eintragen

---

## 📈 Priority Matrix Berechnung

### Score-Komponenten:

**Search Volume (30%)**

- Monatliche Suchvolumen für Keywords
- Trend-Entwicklung der letzten 12 Monate
- Seasonale Schwankungen

**Competition (25%)**

- Keyword Difficulty Score
- SERP-Competition Analyse
- Domain-Authority der Konkurrenz

**Business Value (25%)**

- Relevanz für Geschäftsziele
- Conversion-Potenzial
- Target-Keyword Alignment

**Trending Score (20%)**

- Aktuelle Google Trends
- Social Media Trends
- Industry News & Events

### Priority-Levels:

- **High Priority (≥80):** Sofortige Bearbeitung empfohlen
- **Medium Priority (70-79):** In diesem Monat berücksichtigen
- **Low Priority (<70):** Später oder bei Kapazität bearbeiten

---

## 📅 Content Calendar Features

### Wöchentliche Struktur:

- **Week 1:** 1 Pillar + 1 Cluster + Newsletter
- **Week 2:** 2 Cluster + Social Prep
- **Week 3:** 1 Pillar + 1 Cluster + Newsletter
- **Week 4:** 2 Cluster + Analytics Review

### Planungs-Aspekte:

- **Interview-Zeit:** 30-60 Min pro Artikel für {user_name}
- **Creation Time:** 2-3 Tage pro Artikel
- **Validation:** 1-2 Tage Quality-Check
- **Publishing:** Wie im Kalender geplant

### Content-Type Balance:

- **Pillar Articles (25%):** Fundamentale Topics
- **Cluster Articles (50%):** Spezifische Sub-Topics
- **Newsletter Content (15%):** E-Mail-First-Ansatz
- **Social Media (10%):** Distribution Content

---

## 🎯 Success Metrics & KPIs

### SEO Metrics:

- **Organic Traffic Growth:** Ziel +15% pro Monat
- **Keyword Rankings:** Top 10 für 80% der Ziel-Keywords
- **Click-Through Rate:** Verbesserung um 5%
- **Index Coverage:** 95% der Seiten indexiert

### Content Metrics:

- **Content Output:** {{content_velocity}} Artikel pro Monat
- **Quality Score:** Authenticity ≥ 71/100
- **Engagement:** Social Shares ≥ 10 pro Artikel
- **Backlinks:** 2+ neue Backlinks pro Pillar-Artikel

### Business Metrics:

- **Lead Generation:** +20% durch Content
- **Newsletter Growth:** +10% durch Content-Opt-In
- **Conversion Rate:** +3% durch besser targeting
- **Revenue Attribution:** Messbarer ROI

---

## 🛠️ Troubleshooting

### "GSC-Daten nicht gefunden"

```bash
# Exportiere manuell aus Google Search Console
# Performance → Export → CSV (letzter Monat)
# Speichere als gsc-exports/current-month.csv
```

### "Topic-Map unvollständig"

```bash
# Überprüfe topic-map-master.yaml
# Ergänze fehlende Pillars oder Clusters
# Prüfe interne Linking-Struktur
```

### "Priority Score zu niedrig"

- Priority Weights in workflow.yaml anpassen
- Business Value stärker gewichten
- Competition Score manuell korrigieren

### "Resource Plan nicht realistisch"

- Team Availability in workflow.yaml anpassen
- Content Velocity reduzieren
- External Resources in Betracht ziehen

---

## 🔄 Integration mit anderen Workflows

### Löst aus:

- **Content-Creation Workflow** - Basierend auf geplanten Topics
- **Social-Repurposing Workflow** - Für geplante Distribution
- **Performance-Tracking Workflow** - Für Monats-Review

### Wird beeinflusst durch:

- **Previous Performance Data** - Aus Analytics
- **Market Trends** - Aus externen Quellen
- **Business Goals** - Aus strategischer Planung

---

## 🎯 Best Practices

### Data-Driven Planning:

- Immer auf aktuellen GSC-Daten basieren
- Performance-Trends über mehrere Monate analysieren
- Competitor-Monitoring integrieren
- User-Signale aus Analytics berücksichtigen

### Strategic Alignment:

- Content-Topics mit Geschäftszielen abgleichen
- Target-Audience Personas berücksichtigen
- Customer Journey in Planung integrieren
- Brand-Voice konsistent halten

### Resource Management:

- Realistische Zeitplanung erstellen
- Team-Kapazitäten respektieren
- Buffer-Zeiten einplanen
- Quality über Quantity priorisieren

### Continuous Improvement:

- Monthly Reviews durchführen
- Plan-Performance analysieren
- Strategie anpassen basierend auf Results
- Learning-Loops für zukünftige Planung

---

## 📞 Support

**Issues:** GitHub Issues im BMAD Repository
**Documentation:** SEO-Best-Practice Guides
**Help:** Google Search Console Documentation

---

## 🔮 Zukunftsfähige Erweiterungen

### Advanced Analytics:

- Predictive Analytics für Topic-Selection
- AI-gestützte Trend-Analyse
- Automated Competitor-Monitoring
- Real-time Performance-Tracking

### Strategic Features:

- Multi-quarter Planning
- Budget Planning Integration
- ROI-Projections und Forecasting
- Global Market Expansion Planning

---

**Built with ❤️ using the BMAD Method Framework**

_SEO Planning Workflow - Strategic Content Planning Made Easy_
