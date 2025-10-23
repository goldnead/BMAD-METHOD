# Social Repurposing Workflow Instructions

<critical>The workflow execution engine is governed by: {project-root}/bmad/core/tasks/workflow.xml</critical>
<critical>You MUST have already loaded and processed: {project-root}/bmad/cflow/workflows/social-repurposing/workflow.yaml</critical>
<critical>Communicate in {communication_language} throughout the workflow process</critical>
<critical>This is an intent-based workflow - focus on creative content adaptation rather than prescriptive steps</critical>

<workflow>

<step n="1" goal="Input Analysis & Context Loading">
<action>Prüfe ob der latest_article Pfad existiert: {latest_article}</action>
<check if="latest_article not found">
  <ask>Kein aktueller Artikel gefunden. Bitte gib den Pfad zum neuesten veröffentlichten Artikel an:</ask>
  <action>Warte auf User-Input mit Artikel-Pfad</action>
</check>
<action>Lade den neuesten veröffentlichten Artikel und analysiere:</action>
  - Haupt-Thema und Kernbotschaften
  - Wichtigste Erkenntnisse und quotable Zitate
  - Call-to-Action und Landing-Page
  - Ziel-Keywords und Hashtags
  - Artikel-Struktur für Content-Chunks
<action>Lade das Publishing-Log aus: {publishing_log}</action>
<action>Extrahiere Metadaten:</action>
  - Veröffentlichungsdatum und Plattformen
  - Newsletter Performance (Open-Rate, Clicks)
  - SEO-Artikel Performance (falls verfügbar)
  - User-Engagement Signale
<action>Erstelle eine Content-Analyse mit:</action>
  - 3-5 Key Messages für Social Media
  - 2-3 quotable Zitate von {user_name}
  - Optimaler Call-to-Action für Social
  - Hashtag-Vorschläge (Brand + Trending)
<action>Speichere die Analyse als {article_analysis}</action>
<template-output>article_analysis_complete</template-output>
</step>

<step n="2" goal="Social-Distributor: Multi-Platform Creation">
<action>Lade den Social-Distributor Agenten aus: {project-root}/bmad/cflow/agents/social-distributor.md</action>
<action>Lade Social Media Templates aus: {social_templates}</action>
<action>Der Social-Distributor erstellt 5 Social-Media-Assets basierend auf der Analyse:</action>

**LinkedIn Assets:**

- **Mini-Post:** 200-300 Worte, professioneller Ton, Insight-Sharing
- **Carousel:** 5-7 Slides mit Artikel-Highlights, statisch oder animiert

**Instagram Assets:**

- **Reel Script:** 30-60 Sekunden Skript für Video-Content
- **Carousel:** 5-10 visuelle Folien mit Key Takeaways
- **Quote Card:** Visuelles Zitat von {user_name} mit Branding

**X Asset:**

- **Thread:** 3-5 Tweets mit Artikel-Deep-Dive, Thread-Struktur

**Facebook Asset:**

- **Story:** Interaktive Story mit Swipe-Up Link zum Artikel

<action>Für jedes Asset gilt:</action>

- Adaption an Plattform-Specifics (Tone, Format, Länge)
- Einhaltung der maximalen Zeichenanzahl
- Integration von {user_name} authentischer Stimme
- Klare Call-to-Actions mit Tracking-Links
- Brand-konsistente visuelle Elemente
  <action>Speichere alle Social-Assets als {social_assets_draft}</action>
  <template-output>social_assets_created</template-output>
  </step>

<step n="3" goal="User Review (Optional)">
<check if="enable_user_review == true">
  <action>Präsentiere {user_name} alle erstellten Social-Assets in einer übersichtlichen Vorschau</action>
  <action>Zeige für jedes Asset:</action>
    - Plattform und Asset-Typ
    - Vollständigen Text/Content
    - Visual Mockups (wenn möglich)
    - Vorgeschlagenen Posting-Zeitpunkt
  <ask>Wie findest du die Social-Assets? Möchtest du etwas ändern oder direkt approvals? [Approve All/Edit Specific/Approve Some]</ask>
  <check if="user_response == 'Edit Specific'">
    <ask>Welche Assets möchtest du bearbeiten? Bitte gib spezifisches Feedback.</ask>
    <action>Nehme das Feedback auf und überarbeite die gewünschten Assets</action>
  </check>
  <check if="user_response == 'Approve Some'">
    <ask>Welche Assets sollen veröffentlicht werden? Bitte liste die Plattformen und Typen.</ask>
    <action>Markiere nur die ausgewählten Assets für Publishing</action>
  </check>
  <action>Speichere die finale User-Entscheidung</action>
</check>
<check if="enable_user_review == false">
  <action>Überspringe User Review und gehe direkt zum Scheduling</action>
</check>
<template-output>user_review_complete</template-output>
</step>

<step n="4" goal="Scheduling & Publishing">
<action>Prüfe ob Social Media Scheduler API konfiguriert ist</action>
<check if="auto_schedule_social == true">
  <action>Lade die Social Media Scheduler API Konfiguration</action>
  <action>Berechne optimale Posting-Zeiten basierend auf:</action>
    - Plattform-spezifischen Peak-Times
    - {time_zone} Zeitzone
    - {posting_frequency} Strategie
  <check if="scheduling_strategy == 'optimal-times'">
    <action>Plane die Posts über die nächsten 3 Tage verteilt:</action>
      - LinkedIn: Dienstag/Donnerstag 09:00-11:00
      - Instagram: Montag/Mittwoch/Freitag 18:00-20:00
      - X: Mehrmals täglich, breaking-news style
      - Facebook: Samstag/Sonntag 14:00-16:00
  </check>
  <check if="scheduling_strategy == 'immediate'">
    <action>Plane alle Posts innerhalb der nächsten 2 Stunden</action>
  </check>
  <action>Veröffentliche die approved Assets über die API:</action>
    - Füge Tracking-Parameters hinzu (UTM für Analytics)
    - Integriere brand_hashtags: {brand_hashtags}
    - Füge trending_hashtags hinzu wenn aktiviert
  <action>Erstelle einen Social-Scheduling-Log mit:</action>
    - Alle geplanten Posts mit Zeitstempeln
    - Post-IDs und Plattform-Links
    - Tracking-Parameter und Hashtags
    - Veröffentlichungs-Status
  <action>Speichere den Scheduling-Log als {social_scheduling_log}</action>
</check>
<check if="auto_schedule_social == false">
  <action>Erstelle die Social-Assets als Download-Ready Dateien</action>
  <action>Generiere eine manuelle Posting-Anleitung mit:</action>
    - Copy-Paste Text für jede Plattform
    - Optimale Posting-Zeiten Empfehlungen
    - Hashtag-Strategie und Link-Tracking
    - Visuelle Asset Spezifikationen
  <action>Speichere die manuelle Anleitung als {output_folder}/manual-posting-guide-{date}.md</action>
</check>
<template-output>social_scheduling_complete</template-output>
</step>

<step n="5" goal="Workflow Completion & Summary">
<action>Erstelle eine Zusammenfassung für {user_name} mit:</action>
  - Anzahl erstellter Social-Assets: 5
  - Veröffentlichungsplan (wenn auto_schedule_social aktiviert)
  - Links zur Vorschau der geplanten Posts
  - Empfehlungen für das Engagement
  - Nächste Schritte (Monitoring, Responding)
<action>Speichere alle relevanten Dateien im {output_folder} Ordner</action>
<action>Biete an, den Performance-Tracking Workflow in 1 Woche auszuführen</action>
<action>Erinnere {user_name} daran, die Social-Media-Performance zu überwachen</action>
</step>

</workflow>
