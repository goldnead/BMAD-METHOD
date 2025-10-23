# Content Creation Workflow Instructions

<critical>The workflow execution engine is governed by: {project-root}/bmad/core/tasks/workflow.xml</critical>
<critical>You MUST have already loaded and processed: {project-root}/bmad/cflow/workflows/content-creation/workflow.yaml</critical>
<critical>Communicate in {communication_language} throughout the workflow process</critical>
<critical>This is an intent-based workflow - focus on guiding the user naturally rather than prescriptive questions</critical>

<workflow>

<step n="1" goal="SEO-Strategist: Topic Research & Briefing">
<action>Lade den SEO-Strategist Agenten aus: {config_source}:seo_strategist</action>
<action>Der SEO-Strategist analysiert die GSC-Daten aus: {gsc_data}</action>
<action>Der SEO-Strategist prüft die Topic-Map aus: {topic_map}</action>
<action>Der SEO-Strategist identifiziert Quick-Win Keywords mit hohem Potenzial</action>
<action>Der SEO-Strategist erstellt ein detailliertes Content-Briefing mit:</action>
  - Ziel-Keywords und Suchintention
  - Wichtige Sub-Topics und Questions
  - Empfohlene Artikel-Struktur
  - Interne Linking-Opportunities
  - Ziel-URL und Meta-Informationen
<action>Speichere das Content-Briefing als {output_folder}/content-briefing-{date}.md</action>
<action>Zeige {user_name} das Content-Briefing und hole Zustimmung zur Fortsetzung</action>
</step>

<step n="2" goal="Content-Interviewer: Angle Selection">
<action>Lade den Content-Interviewer Agenten aus: {config_source}:content_interviewer</action>
<action>Der Content-Interviewer generiert 4-6 kreative Artikel-Angles basierend auf dem Content-Briefing</action>
<action>Präsentiere die Angles {user_name} mit klarer Beschreibung jedes Ansatzes</action>
<ask>Welcher Angle (oder welche 2 Angles) sprechen dich am meisten an? Bitte wähle 1-2 Optionen aus.</ask>
<action>Speichere die gewählten Angles als Teil des Interview-Kontexts</action>
</step>

<step n="3" goal="Content-Interviewer: Interview Questions Generation">
<action>Der Content-Interviewer erstellt 10-15 strukturierte Interview-Fragen basierend auf:</action>
  - Gewählten Angles aus Schritt 2
  - Content-Briefing aus Schritt 1
  - Tone-of-Voice-Guide aus: {tone_of_voice_guide}
  - Zielgruppe und Content-Ziele
<action>Die Fragen sollen persönliche Erfahrungen, konkrete Beispiele und Meinungen anregen</action>
<action>Speichere die Interview-Fragen als {output_folder}/interview-questions-{date}.md</action>
</step>

<step n="4" goal="User Interview Phase">
<action>Konfiguriere das Interview-Setup basierend auf {interview_platform}</action>
<check if="interview_platform == 'telegram'">
  <action>Sende die Interview-Fragen über den Telegram Bot an {user_name}</action>
  <action>Erkläre {user_name} den Interview-Prozess und ermutige zu detaillierten Antworten</action>
</check>
<check if="interview_platform == 'notion'">
  <action>Erstelle eine neue Notion-Seite mit den Interview-Fragen</action>
  <action>Sende den Link an {user_name} zur Beantwortung</action>
</check>
<check if="interview_platform == 'manual'">
  <action>Zeige {user_name} die Interview-Fragen direkt an</action>
  <action>Biete an, die Antworten schrittweise zu sammeln</action>
</check>
<ask>Bitte nimm dir Zeit (30-60 Minuten) für die Beantwortung der Fragen. Teile so viele persönliche Erfahrungen und konkrete Beispiele wie möglich. Ready wenn du mit der Interview-Phase fertig bist?</ask>
</step>

<step n="5" goal="Content-Interviewer: Deep-Dive Follow-up">
<action>Der Content-Interviewer analysiert die Interview-Antworten von {user_name}</action>
<action>Basierend auf den Antworten generiert der Agent 2-3 gezielte Deep-Dive-Nachfragen</action>
<action>Die Nachfragen sollen auf interessante Aspekte, Widersprüche oder unbearbeitete Themen eingehen</action>
<action>Sende die Nachfragen über das gleiche Kanal wie in Schritt 4</action>
<ask>Bitte beantworte die Nachfragen, um deine Perspektive weiter zu vertiefen.</ask>
</step>

<step n="6" goal="Content-Interviewer: Interview Protocol Creation">
<action>Der Content-Interviewer erstellt ein umfassendes Interview-Protokoll aus:</action>
  - Allen Interview-Fragen und Antworten
  - Deep-Dive Nachfragen und Antworten
  - Zusammenfassung der wichtigsten Insights
  - Direkte Zitate und persönliche Anekdoten
  - Thematische Cluster und Key Messages
<action>Das Protokoll soll die authentische Stimme von {user_name} bewahren</action>
<action>Speichere das Interview-Protokoll als {interview_protocol}</action>
<template-output>interview_complete</template-output>
</step>

<step n="7" goal="Content-Writer: Draft Creation">
<action>Lade den Content-Writer Agenten aus: {config_source}:content_writer</action>
<action>Der Content-Writer lädt den Tone-of-Voice-Guide aus: {tone_of_voice_guide}</action>
<action>Der Content-Writer analysiert das Interview-Protokoll aus: {interview_protocol}</action>
<action>Der Content-Writer erstellt die Newsletter-Version:</action>
  - Persönlicher E-Mail-Stil
  - Direkte Ansprache der Leser
  - Storytelling mit persönlichen Anekdoten
  - Clear Call-to-Action
<action>Der Content-Writer erstellt die SEO-Artikel-Version:</action>
  - SEO-optimierte Struktur (H1, H2, H3)
  - Keyword-Integration (natürlich, nicht forciert)
  - Meta-Description und Snippet-Optimierung
  - 2+ interne Links zu relevanten Artikeln
<action>Beide Versionen sollen die authentische Stimme von {user_name} widerspiegeln</action>
<action>Speichere den Newsletter-Entwurf als {newsletter_draft}</action>
<action>Speichere den SEO-Artikel-Entwurf als {seo_article_draft}</action>
<template-output>drafts_created</template-output>
</step>

<step n="8" goal="Quality-Validator: Content Validation">
<action>Lade den Quality-Validator Agenten aus: {config_source}:quality_validator</action>
<action>Der Quality-Validator führt 10 SEO-Checks durch:</action>
  - Keyword-Relevanz und -Dichte
  - Meta-Optimierung
  - Interne Linking-Qualität
  - Content-Struktur und Lesbarkeit
  - Unique Value Proposition
<action>Der Quality-Validator führt 8 Authenticity-Checks durch:</action>
  - Abwesenheit von AI-Fingerprints
  - Persönliche Stimme und Stil
  - Authentische Anekdoten und Beispiele
  - Konsistenz mit Tone-of-Voice
<action>Der Quality-Validator nutzt den Authenticity-Scorer aus: {authenticity_scorer}</action>
<action>Erstelle einen detaillierten Validierungs-Report mit:</action>
  - SEO-Score (0-100)
  - Authenticity-Score (0-100)
  - Spezifischen Verbesserungsvorschlägen
  - Entscheidung: GO/NO-GO für Publishing
<action>Speichere den Validierungs-Report als {validation_report}</action>
<check if="authenticity_score < {authenticity_min_score}">
  <action>Markiere den Content als NO-GO und empfehle Revision</action>
  <goto step="7">Zurück zum Content-Writer für Überarbeitung</goto>
</check>
<template-output>validation_complete</template-output>
</step>

<step n="9" goal="User Approval: Final Review">
<action>Präsentiere {user_name} den Newsletter-Entwurf und SEO-Artikel-Entwurf</action>
<action>Zeige auch den Validierungs-Report mit Scores und Empfehlungen</action>
<action>Fasse die wichtigsten Qualitätsmerkmale und Verbesserungen zusammen</action>
<ask>Bist du zufrieden mit den Entwürfen und möchtest du sie veröffentlichen? [Ja/Nein/ Bearbeiten]</ask>
<check if="user_response == 'Nein' or user_response == 'Bearbeiten'">
  <ask>Was möchtest du ändern? Bitte gib spezifische Feedback zu: Newsletter, SEO-Artikel, oder beides.</ask>
  <action>Nehme das Feedback auf und gehe zurück zum Content-Writer für Revision</action>
  <goto step="7">Überarbeitung basierend auf User-Feedback</goto>
</check>
<action>Speichere die finale User-Entscheidung im Publishing-Log</action>
</step>

<step n="10" goal="Content-Publisher: Publishing">
<action>Lade den Content-Publisher Agenten aus: {config_source}:content_publisher</action>
<action>Der Content-Publisher veröffentlicht den SEO-Artikel über Webflow API:</action>
  - Erstelle JSON-LD Schema (Article, FAQ wenn relevant)
  - Veröffentliche auf der Ziel-URL aus dem Briefing
  - Füge interne Links hinzu
  - Optimiere Meta-Tags und Snippets
<action>Der Content-Publisher versendet den Newsletter über Brevo API:</action>
  - Personalisiere die E-Mail mit {user_name} Signatur
  - Füge Tracking-Links hinzu
  - Plane den Versand für optimale Zeit
<action>Der Content-Publisher sendet Index-Request an Google Search Console</action>
<action>Erstelle ein detailliertes Publishing-Log mit:</action>
  - Veröffentlichte URLs und IDs
  - Versand-Statistiken (Newsletter)
  - Index-Request Status
  - Erfolgsmeldungen oder Fehler
<action>Speichere das Publishing-Log als {publishing_log}</action>
<template-output>content_published</template-output>
</step>

<step n="11" goal="Social-Distributor: Auto-Repurposing (Optional)" optional="true">
<ask>Möchtest du aus dem veröffentlichten Artikel automatisch Social-Media-Content erstellen? [Ja/Nein]</ask>
<check if="user_response == 'Ja'">
  <action>Lade den Social-Distributor Agenten aus: {config_source}:social_distributor</action>
  <action>Der Social-Distributor erstellt 5 Social-Media-Assets:</action>
    - LinkedIn Mini-Post und Carousel
    - Instagram Reel Script und Carousel
    - X Thread (3-5 Tweets)
    - Facebook Story
  <action>Der Social-Distributor plant die Posts basierend auf optimalen Zeiten</action>
  <action>Erstelle einen Social-Media-Report mit allen erstellten Inhalten</action>
</check>
</step>

<step n="12" goal="Workflow Completion">
<action>Erstelle eine Zusammenfassung für {user_name} mit:</action>
  - Link zum veröffentlichten SEO-Artikel
  - Newsletter-Versand-Statistiken
  - Authenticity-Score und Validierungs-Report
  - Social-Media-Links (falls erstellt)
  - Nächste Schritte und Empfehlungen
<action>Danke {user_name} für die Teilnahme am Content-Creation Workflow</action>
<action>Speichere alle relevanten Dateien im {output_folder} Ordner</action>
<action>Biete an, den Workflow in 1-2 Wochen für den nächsten Artikel zu wiederholen</action>
</step>

</workflow>
