# Content Creation Workflow Validation Checklist

## Workflow Structure Validation

- [ ] Alle 12 Schritte sind vorhanden und nummeriert
- [ ] Jeder Schritt hat ein klares Ziel definiert
- [ ] Intent-basierter Stil ist konsistent angewendet
- [ ] Kritische Header sind vorhanden (workflow.xml Referenz)
- [ ] Alle {variable} Platzhalter sind korrekt formatiert
- [ ] XML-Tags sind korrekt geschlossen und formatiert

## Input Files Validation

- [ ] workflow.yaml ist vorhanden und vollständig ausgefüllt
- [ ] config_source Referenz zeigt auf existierende cflow/config.yaml
- [ ] Alle Data-File Pfade existieren:
  - [ ] {project-root}/bmad/cflow/data/topic-maps/topic-map-master.yaml
  - [ ] {project-root}/bmad/cflow/data/tone-of-voice-guide.md
  - [ ] {project-root}/bmad/cflow/data/gsc-exports/latest.csv
  - [ ] {project-root}/bmad/cflow/tasks/authenticity-scorer.xml
- [ ] Alle Agent-File Pfade sind korrekt:
  - [ ] seo-strategist.md
  - [ ] content-interviewer.md
  - [ ] content-writer.md
  - [ ] quality-validator.md
  - [ ] content-publisher.md
  - [ ] social-distributor.md

## Step Logic Validation

### Step 1: SEO-Strategist

- [ ] Agent wird korrekt geladen
- [ ] GSC-Daten werden analysiert
- [ ] Topic-Map wird ausgewertet
- [ ] Content-Briefing wird erstellt und gespeichert
- [ ] User-Zustimmung wird eingeholt

### Step 2-3: Angle Selection & Questions

- [ ] Interviewer Agent wird korrekt geladen
- [ ] 4-6 Angles werden generiert
- [ ] User-Auswahl wird verarbeitet
- [ ] 10-15 strukturierte Fragen werden erstellt

### Step 4-6: Interview Process

- [ ] Plattform-Konfiguration funktioniert
- [ ] Fragen werden zugestellt (Telegram/Notion/Manual)
- [ ] Deep-Dive Nachfragen werden generiert
- [ ] Interview-Protokoll wird erstellt

### Step 7: Content Creation

- [ ] Content-Writer wird korrekt geladen
- [ ] Tone-of-Voice-Guide wird berücksichtigt
- [ ] Newsletter-Version wird erstellt
- [ ] SEO-Artikel-Version wird erstellt
- [ ] Beide Versionen speichern authentische Stimme

### Step 8: Quality Validation

- [ ] Quality-Validator wird korrekt geladen
- [ ] Authenticity-Scorer wird aufgerufen
- [ ] 10 SEO-Checks werden durchgeführt
- [ ] 8 Authenticity-Checks werden durchgeführt
- [ ] Scores werden berechnet und validiert
- [ ] Validierungs-Report wird erstellt

### Step 9: User Approval

- [ ] Entwürfe werden präsentiert
- [ ] Validierungs-Report wird gezeigt
- [ ] User-Entscheidung wird verarbeitet
- [ ] Revision-Loop funktioniert bei Bedarf

### Step 10: Publishing

- [ ] Content-Publisher wird korrekt geladen
- [ ] Webflow API Publishing funktioniert
- [ ] Brevo Newsletter-Versand funktioniert
- [ ] GSC Index-Request wird gesendet
- [ ] Publishing-Log wird erstellt

### Step 11: Social Distribution (Optional)

- [ ] Social-Distributor wird nur bei User-Zustimmung geladen
- [ ] 5 Social-Media-Assets werden erstellt
- [ ] Scheduling wird konfiguriert

## Output File Validation

- [ ] Alle Output-Dateien sind mit {date} Variablen versehen
- [ ] Output-Ordner {output_folder} wird korrekt verwendet
- [ ] Output-Dateinamen sind konsistent:
  - [ ] content-briefing-{date}.md
  - [ ] interview-protocol-{date}.md
  - [ ] newsletter-draft-{date}.md
  - [ ] seo-article-draft-{date}.md
  - [ ] validation-report-{date}.md
  - [ ] publishing-log-{date}.md

## Error Handling Validation

- [ ] Conditional Logic funktioniert korrekt:
  - [ ] authenticity_score < authenticity_min_score Trigger
  - [ ] User "Nein/Bearbeiten" Response Trigger
  - [ ] Optional Step 11 funktioniert
- [ ] Goto-Anweisungen führen zu korrekten Schritten
- [ ] Fallback-Mechanismen sind implementiert

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
- [ ] User-Experience ist logisch und intuitiv

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
