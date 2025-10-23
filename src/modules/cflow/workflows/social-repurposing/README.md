# Social Repurposing Workflow

**Automatisches Repurposing von veröffentlichten Artikeln zu 5 Social-Media-Assets mit Multi-Platform Scheduling**

**Typ:** Action Workflow
**Dauer:** 1-2 Stunden
**Output:** 5 Social-Media-Assets (scheduled)

---

## 🎯 Zweck

Dieser Workflow transformiert automatisch veröffentlichte Blog-Artikel in plattformspezifische Social-Media-Content und plant die optimale Veröffentlichung über mehrere Plattformen.

**Ideal für:**

- Multi-Platform Content Distribution
- Zeitersparnis bei Social Media Erstellung
- Konsistente Brand-Presence
- Traffic-Generierung aus Social Media

---

## 🔄 Workflow-Übersicht

```
1. INPUT ANALYSIS → Artikel-Analyse & Metadaten (15 Min)
2. SOCIAL-DISTRIBUTOR → 5 Social-Assets erstellen (45 Min)
3. USER REVIEW → Optional Approval (10 Min)
4. SCHEDULING → Multi-Platform Publishing (15 Min)
5. COMPLETION → Summary & Analytics Prep (5 Min)
```

**Gesamte User-Zeit:** 0-25 Minuten (je nach Review-Option)
**System-Zeit:** Automatisch

---

## 📱 Erstellt Social Media Assets

### LinkedIn (2 Assets)

- **Mini-Post:** 200-300 Worte, professioneller Ton, Insight-Sharing
- **Carousel:** 5-7 Slides mit Artikel-Highlights, statisch oder animiert

### Instagram (3 Assets)

- **Reel Script:** 30-60 Sekunden Skript für Video-Content
- **Carousel:** 5-10 visuelle Folien mit Key Takeaways
- **Quote Card:** Visuelles Zitat mit Branding

### X (1 Asset)

- **Thread:** 3-5 Tweets mit Artikel-Deep-Dive, Thread-Struktur

### Facebook (1 Asset)

- **Story:** Interaktive Story mit Swipe-Up Link zum Artikel

**Gesamt: 5 Social-Media-Assets**

---

## 📋 Benötigte Ressourcen

### Erforderliche Dateien:

- `latest-article.md` - Neuester veröffentlichter Artikel
- `publishing-log-latest.md` - Publishing-Log mit Metadaten
- `social/` - Social Media Templates (LinkedIn, Instagram, X, Facebook)

### Erforderliche Agenten:

- `social-distributor.md` - Multi-Platform Social Content Creation

### Erforderliche APIs:

- **Social Media Scheduler API** (Publer/Metricool) - Für Auto-Scheduling
- **Image Generation API** (Optional) - Für visuelle Assets

---

## 🚀 Nutzung

### Start des Workflows:

```bash
# Via Slash-Command
/cflow:workflow:social-repurposing

# Oder nach Content-Creation Workflow
# Wird automatisch als optionaler Schritt angeboten
```

### Vorbereitung:

1. **Veröffentlichter Artikel verfügbar:**
   - Content-Creation Workflow muss ausgeführt worden sein
   - Artikel muss im Published-Ordner liegen

2. **Social Media Scheduler API:**
   - API-Key in config.yaml eintragen
   - Plattform-Zugänge konfigurieren

3. **Brand Guidelines:**
   - Social Templates sollten brand-konfiguriert sein
   - Hashtags und Brand-Voice definieren

---

## ⚙️ Konfiguration

### Wichtige Settings in `workflow.yaml`:

```yaml
# User Control
enable_user_review: true # User Approval vor Publishing
auto_schedule_social: true # Automatisches Scheduling

# Scheduling Strategy
scheduling_strategy: 'optimal-times' # optimal-times | immediate
time_zone: 'Europe/Berlin'
posting_frequency: 'spread-over-3-days'

# Platforms
social_platforms: ['linkedin', 'instagram', 'x', 'facebook']
```

### Customization:

- **Platform Selection:** Anpassen an deine aktiven Plattformen
- **Posting Frequency:** Sofort vs. verteilt über 3 Tage
- **User Review:** Deaktivieren für vollautomatischen Betrieb
- **Hashtag Strategy:** Brand vs. Trending Hashtags

---

## 📊 Output-Dateien

Alle Dateien werden im `{output_folder}` gespeichert:

- `social-analysis-{date}.md` - Artikel-Analyse für Social Media
- `social-assets-{date}.md` - Alle 5 erstellten Social-Assets
- `social-scheduling-{date}.md` - Publishing-Plan mit Zeitstempeln
- `manual-posting-guide-{date}.md` - Alternative bei deaktiviertem Auto-Scheduling

---

## 🎭 Human-in-Loop Punkte

### User Review (Optional - Step 3)

Wenn `enable_user_review: true`:

- **Asset Vorschau:** Alle 5 Social-Assets werden gezeigt
- **Approval Optionen:**
  - Approve All (alles veröffentlichen)
  - Edit Specific (bestimmte Assets überarbeiten)
  - Approve Some (nur ausgewählte veröffentlichen)
- **Dauer:** 5-15 Minuten

Wenn `enable_user_review: false`:

- Volle Automatisierung ohne User-Interaktion

---

## 📈 Success Metrics

### Content Quality:

- Alle 5 Asset-Typen erfolgreich erstellt
- Plattform-spezifische Adaptionen korrekt
- Brand-Konsistenz gewahrt

### Publishing Success:

- Scheduling-Erfolgsrate ≥ 95%
- API-Fehler < 5%
- Tracking-Links korrekt implementiert

### User Experience:

- Review-Zeit ≤ 15 Minuten
- Approval-Rate ≥ 80%
- Manual Fallback funktioniert

---

## 🛠️ Troubleshooting

### "Kein aktueller Artikel gefunden"

```bash
# Prüfe ob Content-Creation Workflow gelaufen ist
ls bmad/cflow/data/published/latest-article.md

# Oder gib manuell den Artikel-Pfad an beim Workflow-Start
```

### "Social Media Scheduler API fehlgeschlagen"

- API-Key in config.yaml prüfen
- Plattform-Zugänge validieren
- Netzwerk-Verbindung sicherstellen
- Fallback: Manuelles Posting-Guide wird erstellt

### "Assets nicht plattformspezifisch genug"

- Social Templates überprüfen
- Brand Guidelines aktualisieren
- Hashtag-Strategie anpassen

### "Keine visuellen Assets erstellt"

- Image Generation API konfigurieren
- Manuelles Template-Setup prüfen
- Fallback auf Text-Only Assets

---

## 🔄 Integration mit anderen Workflows

### Wird ausgelöst von:

- **Content-Creation Workflow** - Optionaler Step 11
- **Manuell** - Direkter Workflow-Aufruf

### Löst aus:

- **Performance-Tracking Workflow** - Social Media Analytics
- **Social Media Monitoring** - Engagement Tracking

---

## 🎯 Best Practices

### Content Strategy:

- Artikel-Kernbotschaften konsistent kommunizieren
- Starke Call-to-Actions für Traffic-Generierung
- Visuelle Brand-Konsistenz sicherstellen

### Scheduling Strategy:

- Optimal posting times für jede Plattform nutzen
- Content über mehrere Tage verteilen für bessere Reach
- Zeit-zonen für internationale Zielgruppe beachten

### Engagement:

- Social Media Monitoring einrichten
- Auf Kommentare und Messages zeitnah reagieren
- Performance für zukünftige Optimierung nutzen

---

## 📞 Support

**Issues:** GitHub Issues im BMAD Repository
**Documentation:** Agent-spezifische READMEs
**Help:** Social Media Plattform Docs

---

## 🔮 Zukunftsfähige Erweiterungen

### Additional Platforms:

- TikTok (Vertical Video Content)
- Pinterest (Infographics & Ideas)
- LinkedIn Articles (Long-form)

### Advanced Features:

- A/B-Testing für Post-Timing
- AI-generierte visuelle Assets
- Real-time Trend Integration
- Community Management Automation

---

**Built with ❤️ using the BMAD Method Framework**

_Social Repurposing Workflow - Maximize Your Content Reach_
