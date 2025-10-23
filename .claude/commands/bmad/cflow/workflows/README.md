# CFLOW Workflows

## Available Workflows in cflow

**content-creation**

- Path: `bmad/cflow/workflows/content-creation/workflow.yaml`
- Interview-basierter Content-Produktions-Workflow mit KI-Agenten-Flotte für Newsletter und SEO-Artikel

**performance-tracking**

- Path: `bmad/cflow/workflows/performance-tracking/workflow.yaml`
- Monatliche KPI-Analyse und Reporting über alle Plattformen (SEO, Newsletter, Social Media, Analytics) mit Business Impact Assessment

**seo-planning**

- Path: `bmad/cflow/workflows/seo-planning/workflow.yaml`
- Monatliche Content-Planung basierend auf GSC-Datenanalyse, Topic-Map Review und Priority-Matrix für strategische SEO-Content-Entwicklung

**social-repurposing**

- Path: `bmad/cflow/workflows/social-repurposing/workflow.yaml`
- Automatisches Repurposing von veröffentlichten Artikeln zu 5 Social-Media-Assets mit Multi-Platform Scheduling

## Execution

When running any workflow:

1. LOAD {project-root}/bmad/core/tasks/workflow.xml
2. Pass the workflow path as 'workflow-config' parameter
3. Follow workflow.xml instructions EXACTLY
4. Save outputs after EACH section

## Modes

- Normal: Full interaction
- #yolo: Skip optional steps
