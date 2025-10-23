# Cluster Article Template

**Format:** Web/Blog (Detailed Deep-Dive)
**Length:** 1200-2500 words
**Purpose:** Detailed coverage of ONE specific sub-topic within a broader pillar
**Tone:** Educational, detailed, actionable

---

## What is a Cluster Article?

A cluster article is a focused deep-dive that:

- Covers ONE specific aspect of a broader pillar topic
- Links back to the parent pillar page
- Links to sibling cluster articles when relevant
- Ranks for long-tail, specific keywords
- Provides exhaustive detail on the sub-topic

**Example Cluster Structure:**

```
PILLAR: "Content Marketing Strategie"
  ├── CLUSTER: "Content Audit durchführen" ← This template
  ├── CLUSTER: "Content Kalender erstellen"
  ├── CLUSTER: "SEO Content optimieren"
  └── CLUSTER: "Content Distribution Kanäle"
```

---

## Cluster Article Structure

### 1. SEO Meta Data

#### Meta Title (50-60 characters)

**Format:** [Specific Long-Tail Keyword] + [Benefit/Framework]

**Examples:**

- "Content Audit durchführen: 7-Schritte Framework + Template"
- "Email Segmentierung: Der komplette Guide mit Beispielen"
- "Landing Page Copywriting: 12 getestete Formeln"

**Rules:**

- Specific, long-tail keyword (3-5 words)
- Include tangible benefit or format (Framework, Guide, Template)
- More specific than pillar meta title

#### Meta Description (150-160 characters)

**Format:** [Specific problem] + [Concrete solution/framework] + [Unique benefit]

**Example:**
"Lerne wie du einen professionellen Content Audit durchführst. Mit 7-Schritte Framework,
Spreadsheet-Template und Praxisbeispielen. Inkl. Checkliste zum Download."

**Rules:**

- Address specific pain point
- Mention framework/template if included
- Promise concrete takeaway

#### Focus Keyword

**Primary:** Long-tail, specific keyword (e.g., "Content Audit durchführen")
**Secondary:** 2-3 related specific terms (e.g., "Content Audit Template", "Content Inventory", "Content Performance analysieren")

#### URL Slug

**Format:** `/blog/{specific-keyword-slug}`

**Example:** `/blog/content-audit-durchfuehren`

**Rules:**

- More specific than pillar slug
- Include long-tail keyword
- Avoid parent category in slug (already in URL structure)

---

### 2. Breadcrumb Navigation (Required!)

**Purpose:** Show relationship to pillar and improve UX

**Example:**

```
Home > Blog > Content Marketing Strategie > Content Audit durchführen
```

**Schema Markup:**
Use BreadcrumbList schema for SEO benefits

---

### 3. Hero Section

#### H1 Title

**Format:** [How to/The Complete Guide to] [Specific Task/Sub-Topic]

**Examples:**

```
# Wie du einen professionellen Content Audit durchführst (7-Schritte Framework)
# Email Segmentierung: Der komplette Praxis-Guide
# Landing Page Copywriting: 12 erprobte Formeln für mehr Conversions
```

**Alternative formats:**

```
# [Specific Topic]: Schritt-für-Schritt Anleitung
# Alles über [Specific Topic]: Von Basics bis Pro-Level
# Der einzige [Topic] Guide den du brauchst
```

#### Link to Parent Pillar (Required - Place Immediately After H1)

**Format:**

```
> 📚 **Teil der Serie:** [Pillar Title]
> Dieser Artikel ist Teil meines umfassenden Guides zu [Pillar Topic].
> → [Link to Pillar Page with descriptive anchor text]
```

**Example:**

```
> 📚 **Teil der Serie:** Content Marketing Strategie Guide
> Dieser Artikel ist Teil meines umfassenden Content Marketing Strategie Guides.
> → [Zum Haupt-Guide: Content Marketing Strategie meistern]
```

**Why this matters:**

- Establishes topic cluster architecture
- Passes link equity to pillar
- Helps reader navigate to broader context
- Signals to Google this is part of authoritative topic cluster

---

#### Featured Image

**Requirements:**

- 1200x630px
- Specific to sub-topic
- Include screenshot/diagram if applicable
- Alt text with keyword

#### Problem Statement (100-150 words)

**Purpose:** Establish specific pain point this article solves

**Structure:**

```
[Specific problem reader faces]
  ↓
[Why this is frustrating/costly]
  ↓
[Promise of solution]
```

**Example:**

```
Die meisten Content Creators haben hunderte Artikel veröffentlicht – aber keine
Ahnung, welche davon eigentlich performen.

Das Problem? Ohne systematischen Content Audit verschwendest du Zeit mit Updates
an Artikeln die niemand liest, während deine Top-Performer unoptimiert bleiben.

In diesem Guide zeige ich dir ein 7-Schritte Framework für professionelle Content
Audits – mit Spreadsheet-Template, konkreten Beispielen und Checkliste.

Zeitaufwand: 4-6 Stunden für 100 Artikel
Ergebnis: Data-driven Content-Strategie
```

**Problem Statement Checklist:**

- [ ] Opens with specific, relatable problem
- [ ] Quantifies cost or impact of problem
- [ ] Promises concrete, actionable solution
- [ ] Sets clear expectations (time, outcome)
- [ ] Primary keyword mentioned naturally

---

### 4. Quick Navigation / Article Overview (Optional but recommended)

**For longer articles (1500+ words):**

```
## Was du in diesem Guide lernst

- ✅ [Benefit/Learning outcome 1]
- ✅ [Benefit/Learning outcome 2]
- ✅ [Benefit/Learning outcome 3]
- ✅ [Benefit/Learning outcome 4]
- ✅ [Benefit/Learning outcome 5]

**Geschätzte Lesezeit:** 12 Minuten
**Schwierigkeitsgrad:** Anfänger bis Fortgeschritten
**Was du brauchst:** [Tools/prerequisites]
```

---

### 5. Main Content Body

#### Recommended Structure

**Pattern 1: Step-by-Step Framework (Best for "How To" clusters)**

```
## Was ist ein [Topic]? (H2)
[Brief definition and context]

## Warum [Topic] wichtig ist (H2)
[Benefits and stakes]

## Das [X-Schritte] Framework (H2)
### Schritt 1: [Step name] (H3)
[Detailed instructions, examples, screenshots]

### Schritt 2: [Step name] (H3)
[Detailed instructions, examples, screenshots]

[...repeat for all steps]

## Häufige Fehler bei [Topic] (H2)
[Pitfalls and how to avoid them]

## Best Practices (H2)
[Pro tips and optimizations]

## Tools & Templates (H2)
[Resources and recommendations]

## Fazit & Nächste Schritte (H2)
[Summary and CTA]
```

**Pattern 2: Comprehensive Deep-Dive (Best for concept/strategy clusters)**

```
## [Topic] Definition & Grundlagen (H2)
## Die Wissenschaft hinter [Topic] (H2)
## [Topic] Strategien & Ansätze (H2)
  ### Strategie 1 (H3)
  ### Strategie 2 (H3)
  ### Strategie 3 (H3)
## Praxis-Beispiele & Case Studies (H2)
## Häufige Fehler (H2)
## Advanced Tactics (H2)
## Tools & Resources (H2)
## Zusammenfassung (H2)
```

**Pattern 3: Comparison/List (Best for "best of" clusters)**

```
## Die [X] besten [Tools/Methods/Approaches] (H2)
### Option 1: [Name] (H3)
[Description, pros/cons, use cases, pricing]

### Option 2: [Name] (H3)
[Description, pros/cons, use cases, pricing]

[...repeat]

## Vergleichstabelle (H2)
[Side-by-side comparison]

## Wie du die richtige Option wählst (H2)
[Decision framework]

## Fazit (H2)
```

---

#### Content Depth: Go Deep!

**Key Difference from SEO Article:**

```
SEO Article:     Broad but shallow (covers many aspects lightly)
Cluster Article: Narrow but deep (exhaustive on one aspect)
```

**Depth Indicators:**

- Multiple sub-sections (H3, H4) for each major point
- Concrete examples for every concept
- Screenshots or diagrams for every process
- Edge cases and troubleshooting covered
- Both basic and advanced tactics included
- Templates/checklists/frameworks provided

**Example Depth:**

❌ **Too Shallow (SEO Article level):**

```
## Schritt 2: Daten sammeln

Sammle Daten zu deinem Content in einem Spreadsheet. Wichtige Metriken
sind Traffic, Engagement und Conversions.
```

✅ **Proper Depth (Cluster Article level):**

````
## Schritt 2: Content-Daten systematisch sammeln

### 2.1 Datenquellen verbinden

Du brauchst Zugriff auf diese 3 Datenquellen:

**Google Analytics 4:**
- Pageviews (letzte 12 Monate)
- Average time on page
- Bounce rate
- Traffic sources

**Google Search Console:**
- Organic impressions
- Average position
- Click-through rate
- Query-level data

**CMS/Platform:**
- Publish date
- Last modified date
- Author
- Categories/tags

### 2.2 Das Content Audit Spreadsheet

Ich hab ein Template vorbereitet das du kopieren kannst:
→ [Link zum Google Sheet Template]

**Pflicht-Spalten:**
1. URL
2. Title
3. Publish Date
4. Pageviews (12mo)
5. Avg. Position
6. Status (Keep/Update/Merge/Delete)

**Optional aber empfohlen:**
7. Word Count
8. Backlinks
9. Internal Links
10. Conversion Goal

### 2.3 Daten exportieren (Schritt-für-Schritt)

**Google Analytics:**
1. Navigiere zu Reports > Engagement > Pages
2. Setze Zeitraum auf "Last 12 months"
3. Erhöhe Rows auf 5000
4. Export als CSV
5. [Screenshot showing export button]

**Google Search Console:**
1. Navigiere zu Performance > Pages
2. Date range: Last 12 months
3. Filter: nur /blog/* URLs
4. Export als CSV
5. [Screenshot]

### 2.4 Daten zusammenführen

Nutze VLOOKUP oder Python-Script:
```python
# Python script for merging data
[Code snippet]
````

### 2.5 Häufige Probleme beim Datensammeln

**Problem:** GA4 zeigt andere Zahlen als GSC
**Lösung:** Nutze GA4 für Behavior, GSC für Search Performance

**Problem:** Fehlende Daten für alte Artikel
**Lösung:** [Troubleshooting steps]

```

---

#### Visual Requirements

**Minimum Visuals:**
- 1 hero image
- 1 framework/process diagram
- 2-3 screenshots (if applicable)
- 1 summary infographic (optional)

**For Step-by-Step Content:**
- Screenshot for EVERY major step
- Annotate screenshots with arrows/highlights
- Include "before/after" comparisons
- Show expected results

**For Concept Content:**
- Visualize frameworks as diagrams
- Use comparison tables
- Create flowcharts for decision trees

---

#### Internal Linking Strategy

**Required Links:**

**1. Link to Parent Pillar (1 link - already placed after H1)**

**2. Links to Related Sibling Clusters (2-3 links)**

**Format:**
```

🔗 **Siehe auch:** [Brief context for why related]
→ [Descriptive anchor text to sibling cluster]

```

**Example:**
```

🔗 **Siehe auch:** Nachdem du deinen Content Audit abgeschlossen hast,
ist der nächste Schritt die Erstellung eines strukturierten Content-Kalenders:
→ [Content-Kalender erstellen: Template & Best Practices]

```

**Placement:**
- Mid-content (when naturally relevant)
- In "Next Steps" section at end
- In related resources section

**3. Link BACK to Pillar at Conclusion (1 link)**

**Format:**
```

Mehr zu [Pillar Topic] erfährst du in meinem umfassenden Guide:
→ [Pillar Title]

```

**Total Internal Links per Cluster:** 3-6 links
- 1-2 to pillar
- 2-3 to sibling clusters
- 0-1 to other relevant content

---

### 6. Actionable Resources Section (Required)

**Purpose:** Provide concrete takeaways reader can use

**Format:**
```

## Downloads & Templates

📥 **[Template Name]**
[Description of what it includes]
→ [Download link / Make a Copy]

📥 **[Checklist Name]**
[Description]
→ [Download link]

🔧 **Empfohlene Tools**

- [Tool 1]: [Use case] - [Link]
- [Tool 2]: [Use case] - [Link]
- [Tool 3]: [Use case] - [Link]

```

**Template Options:**
- Spreadsheet templates
- Checklists
- Swipe files
- Scripts/code snippets
- Email templates
- Notion templates

---

### 7. FAQ Section (Optional but recommended)

**Purpose:** Capture long-tail search intent

**Structure:**
```

## Häufige Fragen zu [Topic]

**Wie lange dauert ein [Topic]?**
[Concise answer in 2-3 sentences]

**Brauche ich [specific tool/skill] für [Topic]?**
[Concise answer]

**Was kostet [Topic]?**
[Concise answer]

[5-8 FAQs total]

```

**FAQ Sources:**
- Google "People Also Ask"
- AnswerThePublic
- Comments on related content
- Client questions from interviews

---

### 8. Conclusion & Next Steps (Required)

**Length:** 150-250 words

**Structure:**
```

## Zusammenfassung & nächste Schritte

[Quick recap of key points - 3-5 bullets]
↓
[Acknowledge effort required]
↓
[Clear next action]
↓
[Link back to pillar OR to next logical cluster]
↓
[Optional: CTA to resource/offer]

```

**Example:**
```

## Zusammenfassung: Dein Content Audit Action Plan

Du hast jetzt alles was du brauchst:

✅ 7-Schritte Framework für systematische Audits
✅ Spreadsheet-Template zum direkten Start
✅ Kriterien zur Bewertung deines Contents
✅ Decision-Framework für Keep/Update/Delete

Ein vollständiger Content Audit braucht Zeit (4-6 Stunden für 100 Artikel),
aber die Insights sind Gold wert. Du wirst genau wissen, wo du deine Energie
investieren solltest.

**Nächster Schritt:**

1. Kopiere das Template
2. Exportiere deine Daten (GA4 + GSC)
3. Starte mit deinen Top 20 Artikeln
4. Erweitere auf vollständigen Content-Bestand

**Danach:** Nutze die Audit-Ergebnisse um deinen Content-Kalender zu planen:
→ [Content-Kalender erstellen: Template & Strategie]

**Zurück zum Haupt-Guide:**
→ [Content Marketing Strategie: Der komplette Guide]

Viel Erfolg mit deinem Audit!

```

---

### 9. Related Articles Section (Optional)

**Format:**
```

## Ähnliche Artikel

📄 [Sibling Cluster Title]
[One sentence description]

📄 [Sibling Cluster Title]
[One sentence description]

📘 [Back to Pillar]
[One sentence description]

```

---

## Technical SEO for Cluster Articles

### Schema Markup

**Use schema-generator.xml task**

**Required:**
- Article schema
- BreadcrumbList schema (showing pillar relationship)

**Optional:**
- HowTo schema (if step-by-step)
- FAQPage schema (if FAQ section)

### Canonical & Hierarchy

**Ensure proper hierarchy:**
```

Pillar: example.com/content-marketing-strategie
├── Cluster: example.com/blog/content-audit-durchfuehren
├── Cluster: example.com/blog/content-kalender-erstellen
└── Cluster: example.com/blog/seo-content-optimieren

````

**Canonical tag:** Self-referencing (to cluster URL)

### Internal Link Architecture

**Links FROM cluster:**
- To parent pillar (1-2 links)
- To sibling clusters (2-3 links)
- To related resources (0-2 links)

**Links TO cluster:**
- From parent pillar (required!)
- From sibling clusters (when relevant)
- From other related content

---

## Success Metrics

**SEO Performance (3-6 months):**
- Organic impressions: >500/month
- Average position: Top 20 for primary keyword
- Traffic: >100 monthly visits
- Ranking for long-tail variations

**Cluster Ecosystem Health:**
- Pillar page ranks for broad keyword
- All clusters rank for specific long-tails
- Internal linking complete (all clusters ↔ pillar)
- Topic cluster dominates SERPs for topic

**Engagement:**
- Avg. time on page: >4 minutes
- Bounce rate: <65%
- Download rate (if templates): >5%
- Internal link CTR: >8%

---

## Cluster Article Checklist

**Planning:**
- [ ] Clear sub-topic focus (not overlapping with other clusters)
- [ ] Long-tail keyword identified (search volume 100-1K/month)
- [ ] Related to parent pillar
- [ ] Downloadable resource planned (template/checklist)

**Content:**
- [ ] 1,200-2,500 words
- [ ] Exhaustive coverage of sub-topic
- [ ] Step-by-step or comprehensive framework
- [ ] 3+ concrete examples or case studies
- [ ] 3+ visual elements (screenshots, diagrams)
- [ ] FAQ section (5-8 questions)
- [ ] Downloadable resource included
- [ ] Personal insights from interview/experience

**Linking:**
- [ ] Breadcrumb to pillar implemented
- [ ] Link to pillar after H1 title
- [ ] 2-3 links to sibling clusters (natural placement)
- [ ] Link back to pillar in conclusion
- [ ] Descriptive, benefit-driven anchor text

**SEO Technical:**
- [ ] Meta title optimized with long-tail keyword
- [ ] Meta description compelling
- [ ] H1 includes primary keyword
- [ ] Keyword in first 100 words
- [ ] Schema markup (Article + BreadcrumbList)
- [ ] All images have alt text
- [ ] Mobile-responsive verified

**Post-Launch:**
- [ ] Verify pillar page links TO this cluster
- [ ] Add to sitemap
- [ ] Submit to GSC
- [ ] Promote to email list
- [ ] Track rankings for primary keyword
- [ ] Monitor performance for quarterly updates

---

## Template Variables

```yaml
{cluster_topic}: Specific sub-topic
{primary_keyword}: Long-tail keyword
{pillar_title}: Parent pillar page title
{pillar_url}: Parent pillar page URL
{sibling_clusters}: Related cluster articles
{downloadable_resource}: Template/checklist URL
{user_name}: Author name
{date}: Publication date
````

---

## Notes for Content-Writer Agent

- Focus is DEPTH not BREADTH
- Assume reader wants exhaustive coverage of this ONE thing
- Link back to pillar prominently (readers may land here first)
- Include concrete, actionable takeaways (templates, checklists)
- Use more screenshots/visuals than regular SEO articles
- Keep sub-topic focused (don't drift into other cluster territory)
- This is where you can get technical and detailed
- Remember: clusters feed authority to pillar, pillar ranks for broad terms
- Update when pillar gets updated
