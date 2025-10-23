# SEO Planning Workflow Validation Checklist

## Workflow Structure Validation

- [ ] Alle 7 Schritte sind vorhanden und nummeriert
- [ ] Jeder Schritt hat ein klares Ziel definiert
- [ ] Intent-basierter Stil ist konsistent angewendet
- [ ] Kritische Header sind vorhanden (workflow.xml Referenz)
- [ ] Alle {variable} Platzhalter sind korrekt formatiert
- [ ] XML-Tags sind korrekt geschlossen und formatiert

## Input Files Validation

- [ ] workflow.yaml ist vorhanden und vollständig ausgefüllt
- [ ] config_source Referenz zeigt auf existierende cflow/config.yaml
- [ ] Alle Data-File Pfade sind logisch konfiguriert:
  - [ ] {project-root}/bmad/cflow/data/topic-maps/topic-map-master.yaml
  - [ ] {project-root}/bmad/cflow/data/gsc-exports/current-month.csv
  - [ ] {project-root}/bmad/cflow/data/gsc-exports/previous-month.csv
  - [ ] {project-root}/bmad/cflow/data/analytics/monthly-analytics.csv
  - [ ] {project-root}/bmad/cflow/data/priority-matrix.yaml
  - [ ] {project-root}/bmad/cflow/data/seasonal-trends.csv

## Template Validation

- [ ] template.md ist vorhanden und vollständig strukturiert
- [ ] Alle Template-Variablen sind korrekt formatiert ({{variable}})
- [ ] Template-Struktur folgt Content-Plan Best Practices
- [ ] Alle wichtigen Sektionen sind vorhanden:
  - [ ] Executive Summary
  - [ ] Performance Review
  - [ ] Topic Map Review
  - [ ] Priority Matrix Results
  - [ ] Content Calendar
  - [ ] Resource Planning
  - [ ] Success Metrics
  - [ ] Implementation Plan

## Step Logic Validation

### Step 1: GSC Data Analysis

- [ ] GSC-Daten für aktuellen und vorherigen Monat werden geladen
- [ ] Performance-Kennzahlen werden korrekt analysiert
- [ ] Quick-Win Opportunities werden identifiziert
- [ ] Top Performing Keywords werden extrahiert
- [ ] Content Gaps werden erkannt
- [ ] Strategische Insights werden generiert
- [ ] GSC-Analyse-Report wird gespeichert

### Step 2: Topic-Map Review

- [ ] Topic-Map wird geladen und analysiert
- [ ] Coverage Analysis wird durchgeführt
- [ ] Pillar/Cluster Balance wird überprüft
- [ ] Topic Performance wird bewertet
- [ ] Internal Linking wird geprüft
- [ ] Content Gaps und Opportunities werden identifiziert
- [ ] Topic-Map Review wird gespeichert

### Step 3: Priority Matrix Application

- [ ] Priority-Matrix wird geladen
- [ ] Seasonal-Trends werden berücksichtigt
- [ ] Priority-Scores werden korrekt berechnet
- [ ] Topics werden nach Score segmentiert
- [ ] Zusätzliche Faktoren werden integriert
- [ ] Priority-Analyse wird erstellt und gespeichert

### Step 4: Content Calendar Creation

- [ ] Content-Kalender für 4 Wochen wird erstellt
- [ ] {{content_velocity}} Topics werden berücksichtigt
- [ ] Topic-Map Balance wird sichergestellt
- [ ] Content-Type Vielfalt wird implementiert
- [ ] Team-Kapazitäten werden berücksichtigt
- [ ] Seasonal Content wird integriert
- [ ] Detaillierter Zeitplan wird erstellt

### Step 5: Resource Planning

- [ ] Team-Ressourcen werden analysiert
- [ ] Interview-Zeit für {user_name} wird geplant
- [ ] Meilensteine und Deadlines werden definiert
- [ ] Buffer-Zeiten werden eingeplant
- [ ] Resource-Plan wird erstellt und gespeichert

### Step 6: User Approval

- [ ] Template wird geladen und korrekt gefüllt
- [ ] Alle Analysen werden integriert
- [ ] Plan wird {user_name} präsentiert
- [ ] User-Feedback wird verarbeitet
- [ ] Final-Approval wird eingeholt
- [ ] Finaler Plan wird gespeichert

### Step 7: Implementation Preparation

- [ ] Implementations-Schritte werden vorbereitet
- [ ] Interview-Einladungen werden erstellt
- [ ] Implementation-Checklist wird erstellt
- [ ] Reminder werden gesetzt
- [ ] Alle Dateien werden gespeichert

## Output File Validation

- [ ] Alle Output-Dateien sind mit {date} Variablen versehen
- [ ] Output-Ordner {output_folder} wird korrekt verwendet
- [ ] Output-Dateinamen sind konsistent:
  - [ ] monthly-content-plan-{date}.md
  - [ ] gsc-analysis-{date}.md
  - [ ] topic-map-review-{date}.md
  - [ ] priority-analysis-{date}.md
  - [ ] resource-plan-{date}.md

## Configuration Validation

### Planning Parameters

- [ ] planning_horizon ist korrekt gesetzt
- [ ] content_velocity ist realistisch definiert
- [ ] min_priority_score ist angemessen
- [ ] seasonal_adjustments sind konfiguriert

### Priority Matrix

- [ ] priority_weights sind korrekt konfiguriert
- [ ] Gewichtung summiert sich zu 1.0
- [ ] Alle relevanten Faktoren sind berücksichtigt

### Team Configuration

- [ ] Team-Mitglieder sind definiert
- [ ] Availability ist realistisch eingeplant
- [ ] Rollen sind klar zugewiesen

## Content Strategy Validation

### SEO Best Practices

- [ ] Keyword-Strategy ist integriert
- [ ] Topic-Cluster-Ansatz wird verfolgt
- [ ] Internal Linking ist geplant
- [ ] Performance-Tracking ist eingebaut

### Content Planning

- [ ] Balance zwischen Pillar und Cluster Content
- [ ] Vielfalt an Content-Types ist berücksichtigt
- [ ] Publishing-Cadence ist realistisch
- [ ] Quality Assurance ist eingeplant

### Business Alignment

- [ ] Geschäftsziele sind berücksichtigt
- [ ] Target Audience ist definiert
- [ ] Business Value ist Teil der Priority-Berechnung
- [ ] ROI-Messung ist geplant

## Error Handling Validation

- [ ] Fehlende Daten-Files werden abgefangen
- [ ] User-Input-Validierung funktioniert
- [ ] Feedback-Loops sind implementiert
- [ ] Contingency Planning ist vorhanden

## BMAD Standards Compliance

- [ ] Standard Config Block ist in workflow.yaml vorhanden
- [ ] Alle Pfad-Konventionen werden befolgt
- [ ] Template-output Tags sind korrekt platziert
- [ ] Variable-Namings folgen snake_case Konvention
- [ ] Communication Language wird durchgehend verwendet

## Strategic Planning Validation

### Data-Driven Approach

- [ ] Entscheidungen basieren auf GSC-Daten
- [ ] Performance-Analyse fließt in Planung ein
- [ ] Analytics werden für Erfolgsmessung genutzt
- [ ] Trend-Analyse ist integriert

### Resource Management

- [ ] Realistische Zeitplanung
- [ ] Team-Kapazitäten sind berücksichtigt
- [ ] Interview-Zeit ist angemessen eingeplant
- [ ] Buffer für unerwartete Ereignisse

### Continuous Improvement

- [ ] Performance-Tracking ist geplant
- [ ] Monthly Reviews sind eingeplant
- [ ] Optimization-Opportunities werden identifiziert
- [ ] Feedback-Loops sind implementiert

## Final Validation

### Workflow Configuration

- [ ] workflow.yaml Syntax ist valide
- [ ] Alle Variablen sind korrekt referenziert
- [ ] Keine veralteten Platzhalter vorhanden

### Instructions Quality

- [ ] Alle Schritte sind klar verständlich
- [ ] Intent-basierter Stil ist konsistent
- [ ] Strategische Planung wird gefördert
- [ ] User-Expertise wird respektiert

### Template Quality

- [ ] Template-Struktur ist logisch
- [ ] Alle Variablen sind korrekt platziert
- [ ] Business-Reporting-Format ist gewählt
- [ ] Visualisierungselemente sind eingeplant

### Integration Readiness

- [ ] Alle externen Abhängigkeiten sind dokumentiert
- [ ] API-Setup-Anweisungen sind klar
- [ ] Workflow kann autonom durchlaufen werden
- [ ] Menschliche Interaktionspunkte sind definiert

## Issues Found

_Keine Issues bekannt - Workflow ist ready für Testing_
