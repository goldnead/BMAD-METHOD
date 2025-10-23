# SEO Planning Workflow Instructions

<critical>The workflow execution engine is governed by: {project-root}/bmad/core/tasks/workflow.xml</critical>
<critical>You MUST have already loaded and processed: {project-root}/bmad/cflow/workflows/seo-planning/workflow.yaml</critical>
<critical>Communicate in {communication_language} throughout the workflow process</critical>
<critical>This is an intent-based workflow - focus on strategic planning guidance rather than prescriptive analysis</critical>

<workflow>

<step n="1" goal="GSC Data Analysis & Performance Review">
<action>Lade die GSC-Daten für den aktuellen und vorherigen Monat:</action>
  - Aktuelle Daten: {gsc_data_current}
  - Vorherige Daten: {gsc_data_previous}
<action>Analysiere die Performance-Entwicklung:</action>
  - Klicks, Impressions, CTR, Durchschnittsposition
  - Top 20 Keywords nach Impressions und Klicks
  - Pages mit hoher Impressions aber niedriger CTR (Quick-Wins)
  - Keyword-Wachstum compared to Vormonat
  - Device- und Standort-Verteilung
<action>Identifiziere strategische Insights:</action>
  - Welche Topics performen am besten?
  - Wo gibt es unerwartete Performance-Sprünge?
  - Welche Keywords haben hohes Potenzial aber niedrige CTR?
  - Seasonale Trends oder externe Einflüsse?
<action>Erstelle einen GSC-Analyse-Report mit:</action>
  - Executive Summary der Performance
  - Top Performing Keywords und Pages
  - Quick-Win Opportunities (hohe Impressions, niedrige CTR)
  - Content Gaps (Keywords ohne passende Content)
  - Handlungsempfehlungen für Content-Planung
<action>Speichere den Report als {gsc_analysis_report}</action>
<template-output>gsc_analysis_complete</template-output>
</step>

<step n="2" goal="Topic-Map Review & Gap Analysis">
<action>Lade die aktuelle Topic-Map: {topic_map_master}</action>
<action>Führe eine comprehensive Topic-Map Analyse durch:</action>
  - **Coverage Analysis:** Welche Topics haben bereits Content?
  - **Pillar/Cluster Balance:** Ist das Verhältnis 1:8+ erreicht?
  - **Topic Performance:** Welche Themen generieren Traffic?
  - **Content Quality:** Ist der aktuelle Content SEO-optimiert?
  - **Internal Linking:** Gibt es Lücken in der internen Verlinkung?
<action>Vergleiche die Topic-Map mit GSC-Performance-Daten:</action>
  - Welche Topics überperformen Erwartungen?
  - Wo gibt es Diskrepanzen zwischen Planung und Realität?
  - Welche unterperformenden Topics benötigen Optimierung?
<action>Identifiziere Content-Opportunities:</action>
  - **White Spaces:** Topics ohne Konkurrenz aber mit Suchvolumen
  - **Content Upgrades:** Bestehende Artikel mit Neu-Optimierungspotenzial
  - **Cluster Extensions:** Additional Cluster-Artikel für erfolgreiche Pillars
  - **New Pillars:** Brand neue Themenbereiche mit hohem Potenzial
<action>Erstelle ein Topic-Map Review mit:</action>
  - Status-Quo Analyse und Health-Check
  - Identifizierte Gaps und Opportunities
  - Empfohlene Updates und Ergänzungen
  - Priorisierte Maßnahmen für die nächsten 30 Tage
<action>Speichere das Review als {topic_map_review}</action>
<template-output>topic_map_review_complete</template-output>
</step>

<step n="3" goal="Priority Matrix Application">
<action>Lade die Priority-Matrix-Konfiguration: {priority_matrix}</action>
<action>Lade Seasonal-Trends-Daten: {seasonal_trends}</action>
<action>Wende die Priority-Matrix auf alle identifizierten Topics an:</action>
  - **Search Volume Analysis:** Keyword-Daten und Trend-Analyse
  - **Competition Assessment:** Keyword-Difficulty und SERP-Analyse
  - **Business Value Evaluation:** Relevanz für Geschäftsziele
  - **Trending Score:** Aktuelle Trends und saisonale Relevanz
<action>Berechne Priority-Scores für jedes Topic:</action>
  - Search Volume × {priority_weights.search_volume}
  - Competition Score × {priority_weights.competition}
  - Business Value × {priority_weights.business_value}
  - Trending Score × {priority_weights.trending_score}
<action>Segmentiere Topics nach Priority-Scores:</action>
  - **High Priority (≥80):** Sofortige Bearbeitung empfohlen
  - **Medium Priority (70-79):** In diesem Monat berücksichtigen
  - **Low Priority (<70):** Später oder bei Kapazität bearbeiten
<action>Integriere zusätzliche Faktoren:</action>
  - **Seasonal Adjustments:** Berücksichtige saisonale Trends
  - **Content Velocity:** Passt zur geplanten Content-Frequenz?
  - **Resource Requirements:** Ist genug Kapazität vorhanden?
  - **Dependencies:** Gibt es Voraussetzungen oder Abhängigkeiten?
<action>Erstelle eine Priority-Analyse mit:</action>
  - Gerankte Topic-Liste mit Scores und Begründung
  - Visualisierung der Priority-Verteilung
  - Empfehlung für die Top {{content_velocity}} Topics
  - Begründung für Priority-Entscheidungen
<action>Speichere die Analyse als {priority_analysis}</action>
<template-output>priority_analysis_complete</template-output>
</step>

<step n="4" goal="Content Calendar Creation">
<action>Bereite die Content-Planung für {{planning_horizon}} vor</action>
<action>Erstelle einen 4-Wochen Content-Kalender basierend auf:</action>
  - Top {{content_velocity}} Topics aus Priority-Analyse
  - Topic-Map Balance (Pillar vs. Cluster)
  - Content-Type Vielfalt (Pillar, Cluster, Newsletter)
  - Team-Kapazitäten und Interview-Zeiten
<action>Plane die Content-Verteilung strategisch:</action>
  - **Week 1:** 1 Pillar-Artikel + 1 Cluster-Artikel
  - **Week 2:** 2 Cluster-Artikel + Newsletter
  - **Week 3:** 1 Pillar-Artikel + 1 Cluster-Artikel
  - **Week 4:** 2 Cluster-Artikel + Buffer/Contingency
<action>Berücksichtige bei der Planung:</action>
  - **Interview-Zeit für {user_name}:** 30-60 Min pro Artikel
  - **Content Creation Time:** 2-3 Tage pro Artikel
  - **Validation & Publishing:** 1-2 Tage pro Artikel
  - **Social Media Repurposing:** Optional 1 Tag nach Publishing
<action>Integriere Seasonal und Trending Content:</action>
  - Feiertage und saisonale Events
  - Industry Trends und News-Jacking Opportunities
  - Product Launches oder Unternehmens-News
<action>Erstelle einen detaillierten Content-Kalender mit:</action>
  - Wöchentlicher Planung mit konkreten Themen
  - Content-Type Zuordnung und Ziele
  - Time estimates und Deadlines
  - Abhängigkeiten und Voraussetzungen
<action>Speichere den Kalender als Teil des Monthly Content Plans</action>
<template-output>content_calendar_complete</template-output>
</step>

<step n="5" goal="Resource Planning & Assignment">
<action>Analysiere die verfügbaren Ressourcen basierend auf workflow.yaml Konfiguration</action>
<action>Erstelle einen detaillierten Resource-Plan:</action>
  - **{user_name} als Subject Matter Expert:** Interview-Zeit planen
  - **Content Writer Capacity:** Artikelerstellung Zeitplan
  - **SEO Specialist:** Keyword-Recherche und Optimierung
  - **Publisher:** Content-Distribution und Analytics
<action>Plane die Interview-Zeit für {user_name}:</action>
  - Berechne {{content_velocity}} × 30-60 Minuten Interview-Zeit
  - Verteile Interviews über den Monat für bessere Zeitplanung
  - Berücksichtige Availability und Präferenzen
  - Erstelle Interview-Einladungen mit Themen und Fragen
<action>Definiere Meilensteine und Deadlines:</action>
  - **Interview Complete:** 2 Tage vor Content Creation Start
  - **Draft Ready:** 3 Tage nach Interview
  - **Validation Complete:** 1 Tag nach Draft
  - **Publishing Date:** Wie im Content-Kalender geplant
<action>Plane Buffer-Zeiten und Contingency:</action>
  - 15% Buffer für unvorhergesehene Verzögerungen
  - Backup-Themes für falls Interviews ausfallen
  - Flexibilität für trending Topics oder urgente Inhalte
<action>Erstelle einen Resource-Plan mit:</action>
  - Team-Zuweisung und Verfügbarkeit
  - Detaillierter Zeitplan mit Meilensteinen
  - Kapazitätsplanung und Workload-Verteilung
  - Risiko-Mitigation für Ressourcen-Engpässe
<action>Speichere den Resource-Plan als {resource_plan}</action>
<template-output>resource_planning_complete</template-output>
</step>

<step n="6" goal="User Approval & Finalization">
<action>Lade die Template-Datei: {template}</action>
<action>Fülle das Template mit allen gesammelten Daten und Analysen:</action>
  - Executive Summary basierend auf allen Analysen
  - Performance Review aus GSC-Analyse
  - Topic Map Updates aus der Review
  - Priority Matrix Ergebnisse
  - Content Calendar mit Resource-Plan
  - Success Metrics und KPIs
<action>Präsentiere {user_name} den kompletten Monthly Content Plan</action>
<action>Führe durch den Plan und hebe die wichtigsten Punkte hervor:</action>
  - Strategische Fokusbereiche und warum diese gewählt wurden
  - Erwartete Ergebnisse und KPI-Ziele
  - Zeitlicher Aufwand und Commitment für {user_name}
  - nächste Schritte zur Implementierung
<ask>Wie findest du den Content-Plan? Gibt es Anpassungen oder möchtest du den Plan so finalisieren?</ask>
<check if="user_response == 'Anpassungen'">
  <ask>Welche Bereiche möchtest du anpassen? Themen, Zeitplan, Ressourcen oder Ziele?</ask>
  <action>Nehme das Feedback auf und überarbeite den Plan entsprechend</action>
  <action>Zeige die überarbeiteten Bereiche zur Final-Approval</action>
</check>
<action>Nach Final-Approval:</action>
  - Speichere den finalen Plan als {default_output_file}
  - Setze das Approval-Datum im Dokument
  - Bereite die Implementierung basierend auf dem Plan vor
  - Erstelle erste Interview-Einladungen für Week 1
<action>Danke {user_name} für die Zusammenarbeit beim Planning</action>
<template-output>content_plan_approved</template-output>
</step>

<step n="7" goal="Implementation Preparation">
<action>Erstelle die ersten Schritte zur Implementierung des Plans:</action>
  - Interview-Einladungen für Week 1 Themen vorbereiten
  - Content-Creation Workflows initialisieren
  - Tracking und Monitoring einrichten
  - Team-Mitglieder über den Plan informieren
<action>Erstelle einen Implementation-Checklist für {user_name}:</action>
  - Interview-Termine bestätigen
  - Benötigte Materialien und Daten vorbereiten
  - Calendar-Einträge für Content-Meetings
  - Access zu relevanten Tools und Plattformen
<action>Setze Reminder für nächste Schritte:</action>
  - Weekly Check-ins für Plan-Progress
  - Monthly Review Meeting für Performance
  - Quarterly Planning Session für nächsten Plan
<action>Speichere alle relevanten Dateien im {output_folder}</action>
<action>Beende den Workflow mit klaren nächsten Schritten</action>
</step>

</workflow>
