# Social Repurposing Workflow Validation Checklist

## Workflow Structure Validation

- [ ] Alle 5 Schritte sind vorhanden und nummeriert
- [ ] Jeder Schritt hat ein klares Ziel definiert
- [ ] Intent-basierter Stil ist konsistent angewendet
- [ ] Kritische Header sind vorhanden (workflow.xml Referenz)
- [ ] Alle {variable} Platzhalter sind korrekt formatiert
- [ ] XML-Tags sind korrekt geschlossen und formatiert

## Input Files Validation

- [ ] workflow.yaml ist vorhanden und vollständig ausgefüllt
- [ ] config_source Referenz zeigt auf existierende cflow/config.yaml
- [ ] Alle Data-File Pfade sind logisch konfiguriert:
  - [ ] {project-root}/bmad/cflow/data/published/latest-article.md
  - [ ] {project-root}/bmad/cflow/data/published/publishing-log-latest.md
  - [ ] {project-root}/bmad/cflow/templates/social/
- [ ] Social-Distributor Agent Pfad ist korrekt:
  - [ ] {project-root}/bmad/cflow/agents/social-distributor.md

## Step Logic Validation

### Step 1: Input Analysis

- [ ] Latest-Artikel-Pfad wird validiert
- [ ] Fallback für fehlenden Artikel funktioniert
- [ ] Artikel-Analyse umfasst alle wichtigen Aspekte
- [ ] Publishing-Log wird korrekt geladen und analysiert
- [ ] Content-Analyse wird gespeichert

### Step 2: Social Asset Creation

- [ ] Social-Distributor Agent wird korrekt geladen
- [ ] Social Templates werden ausgeladen
- [ ] Alle 5 Asset-Typen werden erstellt:
  - [ ] LinkedIn Mini-Post (200-300 Worte)
  - [ ] LinkedIn Carousel (5-7 Slides)
  - [ ] Instagram Reel Script (30-60 Sek)
  - [ ] Instagram Carousel (5-10 Folgen)
  - [ ] Instagram Quote Card
  - [ ] X Thread (3-5 Tweets)
  - [ ] Facebook Story mit Swipe-Up
- [ ] Plattform-spezifische Adaptionen werden berücksichtigt
- [ ] Brand-Konsistenz wird sichergestellt
- [ ] Alle Assets werden gespeichert

### Step 3: User Review (Optional)

- [ ] enable_user_review Konfiguration wird geprüft
- [ ] Asset-Vorschau wird klar präsentiert
- [ ] User-Entscheidungs-Optionen funktionieren:
  - [ ] Approve All
  - [ ] Edit Specific
  - [ ] Approve Some
- [ ] Feedback-Verarbeitung funktioniert korrekt
- [ ] Übersprung-Option funktioniert bei deaktiviertem Review

### Step 4: Scheduling & Publishing

- [ ] auto_schedule_social Konfiguration wird geprüft
- [ ] API-Konnektivität wird validiert
- [ ] Optimale Posting-Zeiten werden berechnet
- [ ] Scheduling-Strategien funktionieren:
  - [ ] optimal-times
  - [ ] immediate
- [ ] Tracking-Parameter werden hinzugefügt
- [ ] Hashtag-Strategie wird implementiert
- [ ] Manuelle Alternative funktioniert bei deaktiviertem Auto-Scheduling
- [ ] Scheduling-Log wird erstellt

## Output File Validation

- [ ] Alle Output-Dateien sind mit {date} Variablen versehen
- [ ] Output-Ordner {output_folder} wird korrekt verwendet
- [ ] Output-Dateinamen sind konsistent:
  - [ ] social-analysis-{date}.md
  - [ ] social-assets-{date}.md
  - [ ] social-scheduling-{date}.md
  - [ ] manual-posting-guide-{date}.md (optional)

## Configuration Validation

### Social Platforms

- [ ] social_platforms Liste ist vollständig
- [ ] content_types pro Plattform sind definiert
- [ ] max_post_length für jede Plattform ist korrekt
- [ ] platform_specific_content ist aktiviert

### Scheduling Settings

- [ ] scheduling_strategy ist konfiguriert
- [ ] time_zone ist korrekt gesetzt
- [ ] posting_frequency ist definiert
- [ ] optimal_scheduling ist aktiviert

### Hashtag Strategy

- [ ] auto_hashtags ist konfiguriert
- [ ] brand_hashtags sind definiert
- [ ] trending_hashtags ist aktiviert

## Error Handling Validation

- [ ] Conditional Logic funktioniert korrekt:
  - [ ] enable_user_review Trigger
  - [ ] auto_schedule_social Trigger
  - [ ] latest_article not found Trigger
- [ ] API-Fallback-Mechanismen sind implementiert
- [ ] User-Input-Validierung funktioniert

## Social Media Specific Validation

### Content Quality

- [ ] Assets sind plattformspezifisch angepasst
- [ ] Call-to-Actions sind klar und präsent
- [ ] Tracking-Links sind korrekt implementiert
- [ ] Visuelle Konsistenz ist sichergestellt

### Compliance

- [ ] Zeichenzahl-Limits werden eingehalten
- [ ] Hashtag-Best Practices werden befolgt
- [ ] Community-Guidelines werden respektiert
- [ ] Brand-Voice ist konsistent

## BMAD Standards Compliance

- [ ] Standard Config Block ist in workflow.yaml vorhanden
- [ ] Alle Pfad-Konventionen werden befolgt
- [ ] Template-output Tags sind korrekt platziert
- [ ] Variable-Namings folgen snake_case Konvention
- [ ] Communication Language wird durchgehend verwendet

## Final Validation

### Workflow Configuration

- [ ] workflow.yaml Syntax ist valide
- [ ] Alle Variablen sind korrekt referenziert
- [ ] Keine veralteten Platzhalter vorhanden

### Instructions Quality

- [ ] Alle Schritte sind klar verständlich
- [ ] Intent-basierter Stil ist konsistent
- [ ] Keine Hardcoded-Werte wo Variablen sein sollten
- [ ] Social Media Best Practices sind integriert

### Integration Readiness

- [ ] Alle externen Abhängigkeiten sind dokumentiert
- [ ] API-Setup-Anweisungen sind klar
- [ ] Workflow kann autonom durchlaufen werden
- [ ] Menschliche Interaktionspunkte sind definiert

### Documentation

- [ ] README für den Workflow ist vorhanden
- [ ] Zweck und Nutzung sind erklärt
- [ ] Troubleshooting Hinweise sind enthalten

## Issues Found

_Keine Issues bekannt - Workflow ist ready für Testing_
