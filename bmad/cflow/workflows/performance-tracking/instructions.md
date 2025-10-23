# Performance Tracking Workflow Instructions

<critical>The workflow execution engine is governed by: {project-root}/bmad/core/tasks/workflow.xml</critical>
<critical>You MUST have already loaded and processed: {project-root}/bmad/cflow/workflows/performance-tracking/workflow.yaml</critical>
<critical>Communicate in {communication_language} throughout the workflow process</critical>
<critical>This is an autonomous workflow designed to run automatically with minimal human interaction</critical>

<workflow>

<step n="1" goal="Multi-API Data Collection">
<action>Initiiere die Datensammlung von allen konfigurierten Plattformen</action>
<action>Google Search Console API Abruf:</action>
  - Performance-Daten für den letzten Monat
  - Keyword-Rankings und Positionen
  - Click-Through-Raten und Impressions
  - Index-Coverage und crawling Stats
  - Page-Level Performance-Daten
<action>Plausible Analytics API Abruf:</action>
  - Website-Traffic und Unique Visitors
  - Page-Views und Session-Duration
  - Bounce-Rate und Scroll-Tiefe
  - Conversion-Events und Goals
  - Traffic-Quellen und Referrer
<action>Brevo API Abruf:</action>
  - Newsletter Kampagnen Performance
  - Open-Rates, Click-Rates, Bounce-Rates
  - Subscriber Growth und Churn
  - Lead-Generation und Conversion-Daten
  - Revenue Attribution von E-Mail-Kampagnen
<action>Social Media API Abrufe:</action>
  - LinkedIn Performance (Impressions, Engagement)
  - Instagram Analytics (Reach, Engagement Rate)
  - X/Twitter Performance (Impressions, Engagements)
  - Facebook Insights (Reach, Interactions)
  - Social Media Follower Growth
<action>Validiere die gesammelten Daten:</action>
  - Prüfe auf Datenlücken oder Anomalien
  - Validiere Zeitstempel und Datumsbereiche
  - Stelle Konsistenz zwischen Plattformen sicher
  - Erstelle Data-Quality Report
<action>Aggregiere und bereinige die Rohdaten:</action>
  - Normalisiere Zeitstempel und Formate
  - Entferne Duplikate und offensichtliche Fehler
  - Berechne abgeleitete Metriken
  - Speichere die bereinigten Daten als JSON-Export
<action>Speichere die Data-Aggregation als {performance_dashboard}</action>
<template-output>data_collection_complete</template-output>
</step>

<step n="2" goal="Performance Analysis & Insights">
<action>Lade die aggregierten Daten aus {performance_dashboard}</action>
<action>Führe vergleichende Analyse durch:</action>
  - Vergleich mit Vormonat (MoM Growth)
  - Vergleich mit Vorjahreszeitraum (YoY Growth)
  - Trend-Analyse über die letzten 6 Monate
  - Identifiziere Wachstums-Muster und Zyklen
<action>Analysiere SEO-Performance-Trends:</action>
  - Organic Traffic Entwicklung und Seasonalitäten
  - Keyword-Ranking Verbesserungen vs. Verluste
  - CTR-Optimierungen und ihre Auswirkungen
  - Topical Authority und Domain Authority Trends
<action>Analysiere Content-Performance-Korrelationen:</action>
  - Zusammenhang zwischen Authenticity-Score und Traffic
  - Impact von Publishing-Frequenz auf Performance
  - Correlation von Social Shares und SEO-Rankings
  - Content-Type Performance (Pillar vs. Cluster)
<action>Analysiere Business-Impact-Metriken:</action>
  - Lead-Generation Trends und Conversion-Rates
  - Newsletter Performance und Subscriber Growth
  - Social Media ROI und Engagement-Trends
  - Cost-per-Acquisition Entwicklung
<action>Identifiziere Success Patterns:</action>
  - Welche Content-Themes performen am besten?
  - Welche Publishing-Times sind optimal?
  - Welche Plattformen generieren besten ROI?
  - Welche Content-Formate haben höchste Engagement?
<action>Identifiziere Optimization Opportunities:</action>
  - Unterperformende Keywords mit hohem Potenzial
  - Content-Gaps mit hoher Nachfrage
  - Technical SEO Issues die Performance beeinträchtigen
  - Conversion-Optimization Opportunities
<action>Erstelle Performance Insights mit:</action>
  - Klar identifizierten Mustern und Trends
  - Unerwarteten Ergebnissen und Anomalien
  - Datengestützten Hypothesen für Optimierungen
  - Priorisierten Action Items basierend auf Impact
<template-output>performance_analysis_complete</template-output>
</step>

<step n="3" goal="Content Performance Deep-Dive">
<action>Lade Content Performance Log aus: {content_performance_log}</action>
<action>Führe detaillierte Content-Analyse durch:</action>
  - Performance jedes einzelnen Artikels der letzten 30 Tage
  - Traffic-Quellen und User-Journey Analyse
  - Social Media Performance pro Content
  - Conversion Attribution zu spezifischen Artikeln
<action>Identifiziere Top-Performer:</action>
  - Top 10 Artikel nach Traffic und Engagement
  - Top 5 Artikel nach Conversions und Business Impact
  - Content mit höchstem Social Media ROI
  - Artikel mit besten Authenticity-Scores
<action>Analysiere Underperformer:</action>
  - Artikel unter Performance-Erwartungen
  - Content mit hoher Production Cost aber niedrigem ROI
  - Technical SEO Issues die Performance begrenzen
  - Content-Format oder Topic Performance Probleme
<action>Bewerte Content-Quality vs. Performance Correlation:</action>
  - Zusammenhang zwischen Authenticity-Score und User-Engagement
  - Impact von Article-Length und Depth auf Performance
  - Correlation von Internal Linking und SEO-Rankings
  - Influence von Publishing-Time auf initial Performance
<action>Analysiere Topic-Cluster Performance:</action>
  - Pillar-Artikel Performance und Cluster-Synergien
  - Internal Linking Effectiveness zwischen Clustern
  - Topic Authority Development über Zeit
  - Content-Gap Identification innerhalb Clusters
<action>Erstelle Content Insights Report mit:</action>
  - Detaillierter Analyse der besten und schlechtesten Inhalte
  - Handlungsempfehlungen für Content-Optimierung
  - Identifizierten Content-Opportunities
  - Empfehlungen für zukünftige Content-Strategie
<action>Speichere die Content Insights als {content_insights}</action>
<template-output>content_analysis_complete</template-output>
</step>

<step n="4" goal="Business Impact Assessment">
<action>Berechne den Business Impact basierend auf den gesammelten Performance-Daten</action>
<action>Lead Generation Analyse:</action>
  - Gesamtzahl generierter Leads im Monat
  - Lead-Quality und Conversion-Rate
  - Cost-per-Lead Entwicklung und Optimierung
  - Lead-Quellen und Channel Effectiveness
<action>Revenue Attribution:</action>
  - Direkter Revenue generiert durch Content
  - Indirekter Revenue durch Brand-Awareness
  - Lifetime-Value (LTV) von Content-generierten Leads
  - Revenue-per-Artikel und Content-ROI
<action>Cost Analysis:</action>
  - Content Production Costs (basierend auf business_value_assumptions)
  - Tool- und API-Kosten für Analytics
  - Time-Investment von {user_name} und Team
  - Gesamtkosten vs. generierter Revenue
<action>Berechne ROI und Business Metrics:</action>
  - Return on Investment für Content-Marketing
  - Customer Acquisition Cost (CAC) Reduction
  - Marketing Efficiency Ratio (MER)
  - Content-Generated Revenue vs. Gesamt-Revenue
<action>Analysiere Channel-Effectiveness:</action>
  - SEO vs. Newsletter vs. Social Media Performance
  - Multi-Touch-Attribution und Customer Journey
  - Channel-spezifische Conversion-Rates
  - Cross-Channel Synergien und Interactions
<action>Bewerte Business Value Alignment:</action>
  - Alignment von Content-Performance mit Geschäftszielen
  - Impact auf Brand-Awareness und Authority
  - Contribution zu Strategic Initiatives
  - Long-term Business Value Creation
<action>Erstelle Business Impact Analysis mit:</action>
  - Klar quantifiziertem Business Impact
  - ROI-Berechnungen und Cost-Benefit Analysis
  - Strategischen Empfehlungen für Business Growth
  - Benchmark gegen vorherige Perioden und Ziele
<action>Speichere die Business Impact Analyse als {business_impact}</action>
<template-output>business_impact_complete</template-output>
</step>

<step n="5" goal="Report Generation & Distribution">
<action>Lade die Template-Datei: {template}</action>
<action>Fülle das Template mit allen Analysen und Daten:</action>
  - Executive Summary basierend auf Key Insights
  - Performance Overview mit allen KPIs
  - Detaillierte Analyse aus allen vorherigen Schritten
  - Visualisierungen und Charts für Dashboard
  - Handlungsempfehlungen und nächste Schritte
<action>Generiere das Monthly Analytics Report:</action>
  - Fülle alle Template-Variablen mit berechneten Werten
  - Erstelle Executive Summary mit 3-5 Key Takeaways
  - Füge Actionable Recommendations hinzu
  - Formatiere für Lesbarkeit und Impact
<action>Validiere den erstellten Report:</action>
  - Prüfe Datenkonsistenz und Plausibilität
  - Stelle sicher dass alle wichtigen Insights enthalten sind
  - Validiere Berechnungen und Kennzahlen
  - Korrigiere offensichtliche Fehler oder Inkonsistenzen
<action>Speichere den finalen Report als {default_output_file}</action>
<check if="auto_distribute == true">
  <action>Versende den Report an konfigurierte Stakeholder:</action>
  - E-Mail-Versand an {user_name} und Team
  - Optional: Telegram-Benachrichtigung mit Summary
  - Optional: Slack-Integration für Team-Notification
  - Speichere Versand-Protokoll und Status
</check>
<check if="enable_alerts == true">
  <action>Prüfe auf Performance Alerts basierend auf alert_thresholds:</action>
  - Traffic Decline > {{traffic_decline}}%
  - Keyword Ranking Drop > {{ranking_drop}} Positionen
  - Newsletter Bounce Rate > {{newsletter_bounce_rate}}%
  - Andere konfigurierte Thresholds
  <check if="alerts_triggered == true">
    <action>Sende Alert-Benachrichtigungen über alert_channels</action>
    <action>Inkludiere spezifische Alert-Beschreibungen und Empfehlungen</action>
  </check>
</check>
<action>Erstelle Summary für {user_name} mit:</action>
  - Den wichtigsten Performance-Highlights
  - Kritischen Areas of Concern
  - Top 3 Recommended Actions
  - Geplanter Timeline für nächste Schritte
<action>Plane nächste Ausführung des Workflows basierend auf reporting_period</action>
<template-output>report_generation_complete</template-output>
</step>

<step n="6" goal="Workflow Completion & Archive">
<action>Archiviere alle generierten Dateien und Daten:</action>
  - Speichere Report im {output_folder} mit Versionskontrolle
  - Archiviere Rohdaten für historische Analyse
  - Aktualisiere Performance-Trends für zukünftige Vergleiche
  - Bereinige temporäre Dateien und Cache
<action>Aktualisiere Dashboard-Daten für nächste Ausführung:</action>
  - Speichere aktuelle Werte als "previous_period" Referenz
  - Aktualisiere Trends und Prognosen
  - Bereite Daten für Month-over-Month Vergleiche vor
  - Validiere Daten-Integrität für nächste Runde
<action>Dokumentiere Workflow-Ausführung:</action>
  - Log-Daten für Debugging und Optimierung
  - Performance-Metriken des Workflows selbst
  - Identifizierte Issues oder Anomalien
  - Optimierungspotenziale für zukünftige Ausführungen
<action>Beende den Workflow mit Status-Update:</action>
  - Zusammenfassung der generierten Reports
  - Bestätigung der erfolgreichen Datensammlung
  - Hinweis auf nächste geplante Ausführung
  - Kontaktinformationen für Support oder Fragen
</step>

</workflow>
