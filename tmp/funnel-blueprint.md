ChoirAccelerator - Master Implementation Blueprint
Version: 1.0
Datum: 03. Oktober 2025
Status: Ready for Implementation

📑 Inhaltsverzeichnis

Executive Summary
Finales Datenmodell
Business & Money Model
Tool-Setup & Konfiguration
Customer Journeys
Automation Workflows
Implementation Roadmap
Testing & Quality Assurance
Anhang: Technische Spezifikationen

Executive Summary
Projekt-Übersicht
ChoirAccelerator ist ein Funnel-System für Gesangscoaching mit Fokus auf Complete Vocal Technique (CVT) für Chorsänger:innen.
Technologie-Stack
ToolFunktionPlanBrevoEmail Marketing, CRM, SegmentierungPaid PlanThriveCartCheckout, Payment Processing, SubscriptionsPro+ ($295/Jahr)Circle.soCommunity, Course Hosting, Member ManagementStandard Plann8nAutomation OrchestratorSelf-HostedZapierCircle Integration BridgeStarter PlanWebflowWebsite, Landing Pages, Lead Capture-
Key Metrics (Aktuell)

Newsletter-Abonnenten: 300
Verkaufte Coaching-Programme: 13 à 1.500€
Ziel MRR (6 Monate): 5.000€

Finales Datenmodell
Brevo Contact Attributes Schema
Total: 23 Custom Attributes (11,5% von 200 Limit)
Phase 1: Core Funnel (Launch-kritisch)
yaml# === LEAD TRACKING ===
LEAD_SOURCE: text

# Werte: "cvt_webinar" | "arrangement_freebie" | "referral" | "instagram" | "google" | "direct"

# Nutzung: UTM-Tracking, Lead-Source-Reports

LEAD_DATE: date

# Format: YYYY-MM-DD

# Nutzung: Cohort-Analysis, Lead-Age-Berechnung

# === PRODUKT & SUBSCRIPTION ===

PRODUCT_TIER: text

# Werte: "trial" | "ve" | "progroup" | "coaching" | "mentorship" | null

# null = Lead ohne Kauf

# Nutzung: Haupt-Segmentierung

BILLING_CYCLE: text

# Werte: "monthly" | "annual" | "payment_plan" | null

# Nutzung: Upsell-Logic (Annual-Käufer = höheres Commitment)

BILLING_STATUS: text

# Werte: "active" | "paused" | "cancelled" | "completed" | null

# Nutzung: Access Control, Dunning Flows

# === TRIAL ===

TRIAL_ENDS_AT: date

# Format: YYYY-MM-DD

# Nutzung: Trial-Reminder Automations (Day -7, -3, -1, 0)

# === EXTERNAL IDs ===

TC_CUSTOMER_ID: text

# ThriveCart Customer ID

# Format: "cus_abc123xyz"

# Nutzung: ThriveCart API Calls, Subscription Management

TC_SUBSCRIPTION_ID: text

# ThriveCart Subscription ID

# Format: "sub_xyz789abc"

# Nutzung: Subscription Updates, Cancellations

CIRCLE_USER_ID: text

# Circle.so User ID

# Format: "12345678"

# Nutzung: Circle API Calls via Zapier

# === ENGAGEMENT ===

ENGAGEMENT_SCORE: number

# Range: 0-100

# Berechnung: (email_opens × 2) + (clicks × 5) + (circle_logins × 10) + (group_sessions × 20)

# Nutzung: Upsell-Trigger, Re-Engagement Flows

LAST_ACTIVITY_AT: date

# Format: YYYY-MM-DD

# Nutzung: Inaktivitäts-Detection, Churn-Prevention

Phase 2: Advanced Features
yaml# === PAYMENT PLANS ===
PAYMENT_PLAN_TOTAL: number

# Anzahl Raten (z.B. 4 bei 4x97€)

# Nur gefüllt wenn BILLING_CYCLE = "payment_plan"

PAYMENT_PLAN_PAID: number

# Anzahl bezahlter Raten (z.B. 2 nach 2 Monaten)

# Update bei jedem ThriveCart "installment succeeded" Webhook

PAYMENT_PLAN_NEXT_DUE: date

# Nächstes Fälligkeitsdatum

# Nutzung: Payment-Reminder Automations

# === REFERRAL ===

REF_COUNT: number

# Anzahl erfolgreicher Referrals (mit DOI)

# Increment bei jedem validierten Referral

REF_BONUS_UNLOCKED: boolean

# true wenn REF_COUNT >= 3

# Nutzung: Bonus-Freischaltung Trigger

REF_LINK: text

# Persönlicher Referral-Link

# Format: "https://adriangoldner.com/ref/abc123"

# Generiert bei Newsletter-Opt-in

# === COACHING ===

COACHING_SESSIONS_REMAINING: number

# Verbleibende Sessions im Paket

# Decrement bei jeder gebuchten Session

COACHING_PACKAGE_EXPIRES_AT: date

# Ablaufdatum des Coaching-Pakets

# Nutzung: Expiration-Reminder

# === STIMMANALYSE ===

STIMMANALYSE_COMPLETED: boolean

# true nach absolvierter kostenloser Stimmanalyse

# Nutzung: Cross-Sell Coaching-Pakete

STIMMANALYSE_DATE: date

# Datum der Stimmanalyse

# Nutzung: Follow-Up Sequenz Trigger

# === UPSELL TRACKING ===

LAST_UPSELL_OFFER_DATE: date

# Verhindert Spam (min. 30 Tage zwischen Upsells)

LAST_UPSELL_OFFER_TYPE: text

# Werte: "ve_to_progroup" | "progroup_to_coaching" | etc.

# Nutzung: A/B-Test Tracking

Brevo Lists (Segmentierung)
yaml# === HAUPT-LISTEN ===
Newsletter:

- Alle Abonnenten (inkl. Leads ohne Kauf)

Trial_Active:

- Filter: PRODUCT_TIER = "trial" AND BILLING_STATUS = "active"

VE_Members:

- Filter: PRODUCT_TIER = "ve" AND BILLING_STATUS = "active"

ProGroup_Members:

- Filter: PRODUCT_TIER = "progroup" AND BILLING_STATUS = "active"

Coaching_Clients:

- Filter: PRODUCT_TIER = "coaching" OR PRODUCT_TIER = "mentorship"

# === ENGAGEMENT SEGMENTE ===

Hot_Leads:

- Filter: ENGAGEMENT_SCORE >= 61 AND PRODUCT_TIER IN ["trial", "ve"]
- Nutzung: Upsell-Kampagnen

Cold_Leads:

- Filter: ENGAGEMENT_SCORE <= 30
- Nutzung: Re-Engagement Campaigns

Inactive_30_Days:

- Filter: LAST_ACTIVITY_AT < (TODAY - 30 days)
- Nutzung: Win-Back Flows

# === TRIAL SEGMENTE ===

Trial_Ending_Soon:

- Filter: TRIAL_ENDS_AT <= (TODAY + 7 days) AND BILLING_STATUS = "active"
- Nutzung: Conversion-Push Emails

Trial_Expired_No_Conversion:

- Filter: TRIAL_ENDS_AT < TODAY AND PRODUCT_TIER = "trial" AND BILLING_STATUS = "cancelled"
- Nutzung: Downsell Self-Study

# === PAYMENT PLAN SEGMENTE ===

Payment_Plan_At_Risk:

- Filter: BILLING_CYCLE = "payment_plan" AND (PAYMENT_PLAN_PAID / PAYMENT_PLAN_TOTAL) < 0.5
- Nutzung: Retention Monitoring

# === REFERRAL SEGMENTE ===

Referral_Close_To_Bonus:

- Filter: REF_COUNT = 2 AND REF_BONUS_UNLOCKED = false
- Nutzung: "Noch 1 Referral bis Bonus!" Email

Referral_Bonus_Unlocked:

- Filter: REF_BONUS_UNLOCKED = true
- Nutzung: Bonus-Delivery Automation

Business & Money Model
Value Ladder
┌────────────────────────────────────────────────────┐
│ MENTORSHIP (3.500€/Jahr) │
│ ↑ 24 Sessions, Unlimited Support, VIP Status │
├────────────────────────────────────────────────────┤
│ COACHING PROGRAMM (1.500€) │
│ ↑ 8 Sessions, 6 Monate ProGroup inkl. │
├────────────────────────────────────────────────────┤
│ PROGROUP MEMBERSHIP (85€/M oder 697€/J) │
│ ↑ Gruppencoaching + VE Content │
├────────────────────────────────────────────────────┤
│ VOCAL ESSENTIALS (47€/M oder 347€/J) │
│ ↑ Self-Study Masterclasses, Community │
├────────────────────────────────────────────────────┤
│ TRIAL (7€ für 30 Tage) │
│ ↑ Inkl. kostenlose Stimmanalyse │
├────────────────────────────────────────────────────┤
│ LEAD MAGNET (CVT Mini-Kurs) │
│ → Newsletter Opt-in │
└────────────────────────────────────────────────────┘
Produkt-Matrix
Core Products
ProduktMonatlichJährlichPayment PlanLTV (Ø)Trial7€ (einmalig)--7€VocalEssentials47€347€ (spare 217€)4x 97€ (388€)564€ProGroup85€697€ (spare 467€)3x 247€ (741€)1.020€Coaching-1.500€ (einmalig)-1.500€Mentorship-3.500€/Jahr-3.500€
Order Bumps (Cross-Sells)
BumpPreisCheckout-FlowAcceptance Rate (Ziel)Warm-Up Bundle17€Trial, VE, ProGroup25%Stimmnotfallplan19€Trial, VE20%CVT Cheat Sheet17€VE, ProGroup15%30-Tage Übungsplan27€ProGroup, Coaching30%Mini-Feedback Service47€VE, ProGroup10%Blending Practice Paket19€ProGroup, Coaching20%
Downsells
VonZuPreisConversion Rate (Ziel)VE AnnualVE Payment Plan4x 97€30%VESelf-Study27€/M40%ProGroup AnnualProGroup Monthly85€/M50%ProGroupVE47€/M25%CoachingCoaching Light997€20%
Revenue Projections (6 Monate)
Annahmen:

Newsletter-Wachstum: +100/Monat (via Referral + Organic)
Trial Conversion Rate: 15%
VE Retention: 70% nach 6 Monaten
Upsell VE→ProGroup: 20% nach 60 Tagen

MonatNewsletterTrialVEProGroupCoachingMRRM140010500305€M2500151210729€M36002020311.395€M47002528612.046€M580030351022.795€M690035421523.749€
Break-Even: Monat 4 (2.000€ MRR)
Target MRR: Monat 6 (3.749€)

Tool-Setup & Konfiguration

1. ThriveCart Setup
   Produkt-Konfiguration
   Product 1: Trial (7€)
   yamlProduct Name: "VocalEssentials Trial - 30 Tage Zugang"
   Product Type: Subscription (Limited)
   Price: 7€
   Billing: One-time (kein Rebill)
   Trial Length: 30 Tage

Checkout Page URL: /trial

Payment Processors:

- Stripe Connect+ (Primary)
- PayPal (Backup)

Order Bumps:

- Warm-Up Bundle (17€)
- Stimmnotfallplan (19€)

Upsell Funnel:

- Upsell 1: VocalEssentials Monthly (47€/M)
- Upsell 2: VocalEssentials Annual (347€)
- Downsell: Self-Study (27€/M)

Webhooks:

- subscription.charge.succeeded → n8n Webhook URL
- subscription.cancelled → n8n Webhook URL

Settings:

- Enable Subscription Saver (Dunning): Yes
- Customer Self-Cancel: Enabled (EU compliance)
- Send Receipt: Automated
  Product 2: VocalEssentials Monthly
  yamlProduct Name: "VocalEssentials Membership - Monatlich"
  Product Type: Subscription (Ongoing)
  Price: 47€/Monat
  Billing: Monthly (recurring)
  Trial: None

Checkout Page URL: /vocal-essentials

Payment Processors:

- Stripe Connect+ (Primary)

Order Bumps:

- Warm-Up Bundle (17€)
- CVT Cheat Sheet (17€)
- Mini-Feedback Service (47€)

Upsell Funnel:

- Upsell 1: VocalEssentials Annual (347€) ← Pay Now Special
- Upsell 2: ProGroup Monthly (85€/M)

Settings:

- Enable Prorating: Yes (Pro+ Feature)
- Upgrade Path: → ProGroup (automatisches Prorating)
- Downgrade Path: → Self-Study (läuft bis Monatsende)
- Customer Self-Cancel: Enabled
  Product 3: VocalEssentials Annual
  yamlProduct Name: "VocalEssentials Membership - Jährlich"
  Product Type: Subscription (Limited to 1 year)
  Price: 347€
  Billing: Annual (1 rebill nach 12 Monaten)

Bonuses:

- "CVT Advanced Techniques" Kurs
- "Perfect Blending Masterclass"
- "Stimmnotfall Premium Kit"
- 1x kostenloses Coaching-Call (197€ Wert)

Upsell Funnel:

- Upsell 1: ProGroup Annual (697€) - nur weitere 300€ mehr

Settings:

- Enable Prorating: Yes
- Upgrade Path: → ProGroup Annual
  Product 4: VocalEssentials Payment Plan
  yamlProduct Name: "VocalEssentials - 4 Raten"
  Product Type: Split-Pay (Payment Plan)
  Price: 4x 97€ (Total: 388€)
  Billing: Monthly (4 payments)

Settings:

- Customer Self-Cancel: Disabled (Pro+ Setting)
- Failed Payment Grace: 7 Tage
- After Completion: Auto-convert to VE Monthly (47€/M)

Webhooks:

- subscription.charge.succeeded (per installment)
- subscription.completed (after final payment)
  Product 5: ProGroup Monthly
  yamlProduct Name: "ProGroup Membership - Monatlich"
  Product Type: Subscription (Ongoing)
  Price: 85€/Monat

Checkout Page URL: /pro-group

Order Bumps:

- 30-Tage Übungsplan (27€)
- Blending Practice Paket (19€)
- Mini-Feedback Service (47€)

Upsell Funnel:

- Upsell 1: ProGroup Annual (697€)
- Upsell 2: Coaching Programm (1.500€)

Settings:

- Enable Prorating: Yes
- Upgrade Path: → Coaching (Credit-Anrechnung via n8n)
- Downgrade Path: → VocalEssentials
  Product 6: ProGroup Annual
  yamlProduct Name: "ProGroup Membership - Jährlich"
  Product Type: Subscription (Limited to 1 year)
  Price: 697€

Bonuses:

- 1x Einzelcoaching-Session (197€)
- Priority Support
- Früher Zugang zu neuen Inhalten

Settings:

- Enable Prorating: Yes
  Product 7: Coaching Programm
  yamlProduct Name: "ChoirAccelerator Coaching Programm"
  Product Type: One-Time Purchase
  Price: 1.500€

Includes:

- 8x Einzelcoaching Sessions
- 6 Monate ProGroup Membership (Wert: 510€)
- WhatsApp-Support während Programm

Checkout Page URL: /choir-accelerator

Order Bumps:

- Extra Coaching Session (97€)
- Blending Practice Paket (19€)

Upsell Funnel:

- Upsell 1: Mentorship (3.500€/Jahr)
- Downsell: Coaching Light (997€ - ohne ProGroup)

Settings:

- After Purchase: n8n → erstelle ProGroup Subscription (85€/M) + pause first 6 months
  Product 8: Self-Study (Downsell)
  yamlProduct Name: "VocalEssentials Self-Study"
  Product Type: Subscription (Ongoing)
  Price: 27€/Monat

Includes:

- 7 Masterclasses (kein Community-Zugang)

Settings:

- Upgrade Path: → VocalEssentials Full (47€/M)
  Webhook-Konfiguration (Global)
  yamlWebhook Endpoint: https://your-n8n-instance.com/webhook/thrivecart

Events to Subscribe:

- subscription.charge.succeeded
- subscription.charge.failed
- subscription.cancelled
- subscription.paused
- subscription.completed
- subscription.upgraded
- subscription.downgraded
- refund.issued
- order.success

Webhook Format: JSON
Retry on Failure: Yes (3x with backoff)

2. Brevo Setup
   Automation Workflows
   Welcome Sequence (Newsletter Opt-in)
   yamlName: "Newsletter Welcome Sequence"
   Trigger: Contact added to List "Newsletter"

Emails:
Day 0 (sofort):
Subject: "Willkommen! Hier ist dein CVT Mini-Kurs 🎵"
Content: - Persönliche Begrüßung - Link zum CVT Mini-Kurs - Referral-Link: "Teile mit 3 Freunden → Gratis 'Perfektes Blending' Kurs" - CTA: Trial für 7€ testen

Day 2:
Subject: "Die #1 Fehler beim CVT Blending"
Content: - Educational Content - Social Proof (Testimonial) - CTA: Trial für 7€

Day 5:
Subject: "Warum die meisten Chorsänger falsch trainieren"
Content: - Problem Awareness - Lösung: VocalEssentials - Limited Time: 7€ Trial

Day 7:
Subject: "Letzte Chance: 7€ Trial endet bald"
Content: - Urgency (nicht für alle, nur für die, die noch nicht konvertiert haben) - Objection Handling - Garantie

Conditions:

- Stop sequence wenn PRODUCT_TIER != null (User hat gekauft)
  Trial Reminder Sequence
  yamlName: "Trial Conversion Sequence"
  Trigger: PRODUCT_TIER = "trial" AND BILLING_STATUS = "active"

Emails:
Day 1 (nach Trial-Start):
Subject: "Willkommen bei VocalEssentials! 🎉"
Content: - Onboarding Guide - Circle-Zugang Anleitung - Bonus: Stimmanalyse buchen (Cal.com Link)

Day 7 (23 Tage vor Ende):
Subject: "Noch 23 Tage: Deine ersten CVT-Fortschritte?"
Content: - Check-in Email - Feature Highlight - CTA: Jetzt upgraden (spare 217€ mit Annual)

Day 23 (7 Tage vor Ende):
Subject: "Dein Trial endet in 7 Tagen"
Content: - Reminder - Special Offer: Annual 347€ (save 217€) - Payment Plan Option: 4x 97€

Day 27 (3 Tage vor Ende):
Subject: "Nur noch 3 Tage: Behalte deinen CVT-Fortschritt"
Content: - Urgency - Social Proof - FAQ zu Payment Options

Day 29 (1 Tag vor Ende):
Subject: "LETZTE CHANCE: Dein Trial endet morgen"
Content: - Final Push - Guarantee: 60 Tage Geld-zurück - Objection Handling

Day 30 (Trial abgelaufen):
IF BILLING_STATUS = "cancelled":
Subject: "Schade, dass du gehst... hier ist ein Special"
Content: - Downsell: Self-Study für 27€/M - Testimonials - Last Chance Offer

Conditions:

- Stop wenn User zu VE upgraded
- Weiter zu Downsell-Flow wenn Trial gecancelt
  Upsell VE → ProGroup
  yamlName: "ProGroup Upsell Sequence"
  Trigger:
- PRODUCT_TIER = "ve"
- BILLING_STATUS = "active"
- Days since VE purchase >= 45
- ENGAGEMENT_SCORE >= 60

Emails:
Day 45:
Subject: "Du rockst VocalEssentials! Ready für den nächsten Level?"
Content: - Congratulate Progress - Introduce ProGroup (Gruppencoaching) - Social Proof von ProGroup Members - CTA: Jetzt upgraden

Day 48:
Subject: "Die Wahrheit über Self-Study vs. Live-Coaching"
Content: - Education: Benefits of Live Feedback - ProGroup Features - Special: Erste Session kostenlos testen

Day 52:
Subject: "Angebot läuft aus: ProGroup für nur 38€ mehr"
Content: - Urgency (falscher Scarcity vermeiden!) - ROI-Berechnung: 38€ mehr = X Stunden Live-Coaching - Payment Options: 85€/M oder 697€/J

Conditions:

- Stop wenn User zu ProGroup upgraded
- Max. 1 Upsell-Sequenz alle 60 Tage (verhindert Spam)
  Re-Engagement (Inactive Users)
  yamlName: "Win-Back Inactive Users"
  Trigger: LAST_ACTIVITY_AT < (TODAY - 30 days) AND BILLING_STATUS = "active"

Emails:
Day 30:
Subject: "Wir vermissen dich! Ist alles ok?"
Content: - Personal Touch - "Was hält dich zurück?" (Survey Link) - Offer Help: Kostenloses Check-In Call

Day 37:
Subject: "Exklusiv für dich: Neue CVT-Masterclass"
Content: - Value Delivery (neue Inhalte) - Zeige was sie verpassen - CTA: Komm zurück in die Community

Day 44:
Subject: "Behalte deinen Membership oder pausieren?"
Content: - Pause-Option (nicht sofort kündigen) - Alternative: Downgrade zu Self-Study - Last Chance: Persönliches Gespräch

Conditions:

- Stop wenn User wieder aktiv wird
- Wenn keine Reaktion nach 60 Tagen: Flag für manuelles Follow-Up
  Referral Bonus Unlock
  yamlName: "Referral Bonus Delivery"
  Trigger: REF_COUNT >= 3 AND REF_BONUS_UNLOCKED = false

Email:
Subject: "🎉 Du hast es geschafft! Dein Bonus ist freigeschaltet"
Content: - Congratulations - Bonus: "Perfektes Blending" Masterclass - Circle-Freischaltung via Zapier - CTA: Weiter empfehlen für zusätzliche Perks

Actions (via n8n):

1. Set REF_BONUS_UNLOCKED = true
2. Trigger Zapier → Circle unlock Bonus Content
3. Send Email

4. Circle.so Setup
   Spaces-Struktur
   yaml# === PUBLIC SPACES ===
   Willkommens-Space:
   Visibility: All Members
   Content: - Willkommens-Video - Community Guidelines - Erste Schritte Guide - FAQ

# === VOCAL ESSENTIALS SPACES ===

VE_Masterclass_Hub:
Access: PRODUCT_TIER IN ["trial", "ve", "progroup", "coaching", "mentorship"]
Content: - 7 Masterclass Recordings - Workbooks (PDF Downloads) - Progress Tracker

VE_Ressourcen:
Access: PRODUCT_TIER IN ["trial", "ve", "progroup", "coaching", "mentorship"]
Content: - Stimmnotfallplan - CVT Schnellreferenz - Selbstanalyse Protokoll - Perfekte-Übeeinheit-Vorlage

VE_Community:
Access: PRODUCT_TIER IN ["ve", "progroup", "coaching", "mentorship"]
Note: Trial hat nur Read-Access
Content: - Discussion Forum - Voice Note Feedback Threads - Success Stories

VE_Übungsbibliothek:
Access: PRODUCT_TIER IN ["ve", "progroup", "coaching", "mentorship"]
Content: - Gesangsübungen nach Masterclass-Thema - Warm-Up Bibliothek

# === PROGROUP SPACES ===

ProGroup_Gruppencoaching:
Access: PRODUCT_TIER IN ["progroup", "coaching", "mentorship"]
Content: - Live-Session Kalender - Recording-Archiv - Homework Assignments

ProGroup_Private_Lounge:
Access: PRODUCT_TIER IN ["progroup", "coaching", "mentorship"]
Content: - Exclusive Tips - Direct Q&A mit Adrian - Advanced Techniques

# === COACHING SPACES ===

Coaching_1on1_Space:
Access: PRODUCT_TIER IN ["coaching", "mentorship"]
Content: - Buchungskalender - Session Notes - Personalized Resources

# === BONUS CONTENT (REFERRAL) ===

Bonus_Perfect_Blending:
Access: REF_BONUS_UNLOCKED = true
Content: - "Perfektes Blending" Masterclass - A-Cappella Backing Tracks - Blending Practice Guide
Member Roles
yamlTrial:
Assigned when: PRODUCT_TIER = "trial"
Permissions: - View VE Masterclasses - View Resources - Read-Only Community Access
Badge: "🔍 Trial Member"

VocalEssentials:
Assigned when: PRODUCT_TIER = "ve"
Permissions: - All Trial Permissions - Post in Community - Download Resources
Badge: "🎵 VE Member"

ProGroup:
Assigned when: PRODUCT_TIER = "progroup"
Permissions: - All VE Permissions - Access ProGroup Spaces - Book Group Sessions
Badge: "⭐ ProGroup Member"

Coaching:
Assigned when: PRODUCT_TIER IN ["coaching", "mentorship"]
Permissions: - All ProGroup Permissions - Access Coaching Spaces - Priority Support
Badge: "💎 Coaching Client"

Referral_Bonus:
Assigned when: REF_BONUS_UNLOCKED = true
Additional Permissions: - Access Bonus Content
Badge: "🎁 Referral Champion"

4. n8n Workflows
   Workflow 1: ThriveCart Purchase Handler
   yamlWorkflow Name: "TC_Purchase_Handler"
   Trigger: Webhook (ThriveCart subscription.charge.succeeded)

Nodes:

1.  [Webhook] Receive ThriveCart Event
    ↓
2.  [Function] Parse Webhook Data
    Extract:
    - customer.email
    - customer.id
    - product.name
    - subscription.id
    - subscription.status
    - subscription.billing_cycle
    - installment.current (für Payment Plans)
    - installment.total (für Payment Plans)
      ↓
3.  [Switch] Check Event Type

    CASE: First Purchase (installment = 1 or null)
    ↓
    4a. [HTTP Request] Brevo: Update/Create Contact
    Attributes: - TC_CUSTOMER_ID: customer.id - TC_SUBSCRIPTION_ID: subscription.id - PRODUCT_TIER: Mapped from product.name - BILLING_CYCLE: subscription.billing_cycle - BILLING_STATUS: "active" - LAST_ACTIVITY_AT: NOW()

        IF product = "Trial":
        - TRIAL_ENDS_AT: NOW() + 30 days

        IF billing_cycle = "payment_plan":
        - PAYMENT_PLAN_TOTAL: installment.total
        - PAYMENT_PLAN_PAID: 1
        - PAYMENT_PLAN_NEXT_DUE: NOW() + 30 days

    ↓
    5a. [HTTP Request] Zapier Webhook: Create Circle User
    Payload: - email: customer.email - product_tier: mapped_tier - action: "create_or_update_role"
    ↓
    6a. [HTTP Request] Brevo: Start Welcome Sequence
    Add to List based on PRODUCT_TIER

    CASE: Payment Plan Installment (installment > 1)
    ↓
    4b. [HTTP Request] Brevo: Update Contact
    Attributes: - PAYMENT_PLAN_PAID: installment.current - PAYMENT_PLAN_NEXT_DUE: NOW() + 30 days - LAST_ACTIVITY_AT: NOW()
    ↓
    5b. [Function] Check if Final Installment
    IF installment.current == installment.total:
    ↓
    6b. [HTTP Request] Brevo: Update
    Attributes: - BILLING_STATUS: "completed" - BILLING_CYCLE: "monthly" (auto-convert)
    ↓
    7b. [HTTP Request] ThriveCart API: Convert to Monthly Subscription

    CASE: Annual Renewal
    ↓
    4c. [HTTP Request] Brevo: Update
    Attributes: - LAST_ACTIVITY_AT: NOW() - (Renewal erfolgt automatisch in TC)
    ↓
    5c. [Email] Renewal Success Notification

4.  [End]
    Workflow 2: Failed Payment Handler
    yamlWorkflow Name: "TC_Failed_Payment_Handler"
    Trigger: Webhook (ThriveCart subscription.charge.failed)

Nodes:

1. [Webhook] Receive Failed Payment Event
   ↓
2. [HTTP Request] Brevo: Get Contact by TC_CUSTOMER_ID
   ↓
3. [HTTP Request] Brevo: Update Contact
   Attributes:
   - BILLING_STATUS: "paused"
   - LAST_ACTIVITY_AT: NOW()
     ↓
4. [Function] Calculate Grace Period End
   grace_end = NOW() + 7 days
   ↓
5. [HTTP Request] Brevo: Start Dunning Email Sequence
   Day 0: "Zahlungsfehler - bitte aktualisiere Zahlungsmethode"
   Day 3: "Reminder: Update deine Zahlung"
   Day 7: "Letzter Tag: Dein Zugang läuft heute ab"
   ↓
6. [Delay] Wait 7 days
   ↓
7. [HTTP Request] Brevo: Check BILLING_STATUS

   IF still "paused":
   ↓
   8a. [HTTP Request] Zapier: Downgrade Circle Role
   Action: "downgrade_to_readonly"
   ↓
   9a. [Delay] Wait 7 more days
   ↓
   10a. [HTTP Request] Brevo: Check again
   IF still "paused":
   ↓
   11a. [HTTP Request] Zapier: Remove Circle Access
   ↓
   12a. [HTTP Request] Brevo: Remove from Active Lists

   ELSE (Payment succeeded in meantime):
   ↓
   8b. [End] ThriveCart Subscription Saver handled it

8. [End]
   Workflow 3: Subscription Upgrade Handler (ThriveCart Prorating)
   yamlWorkflow Name: "TC_Subscription_Upgrade"
   Trigger: Webhook (ThriveCart subscription.upgraded)

Nodes:

1. [Webhook] Receive Upgrade Event
   Payload:
   - old_product_id
   - new_product_id
   - prorated_amount (automatisch von TC berechnet)
   - customer_id
     ↓
2. [HTTP Request] Brevo: Get Contact by TC_CUSTOMER_ID
   ↓
3. [Function] Map Product IDs to Tiers
   old_tier = map_product(old_product_id)
   new_tier = map_product(new_product_id)
   ↓
4. [HTTP Request] Brevo: Update Contact
   Attributes:
   - PRODUCT_TIER: new_tier
   - BILLING_STATUS: "active"
   - LAST_ACTIVITY_AT: NOW()
   - LAST_UPSELL_OFFER_DATE: null (reset)
     ↓
5. [HTTP Request] Zapier: Update Circle Role
   Payload:
   - user_email: contact.email
   - new_role: new_tier
   - action: "upgrade_role"
     ↓
6. [HTTP Request] Brevo: Send Upgrade Success Email
   Template: "Willkommen im [new_tier]!"
   ↓
7. [Function] Calculate Engagement Score Bonus
   engagement_score += 20 (Upgrade = starkes Signal)
   ↓
8. [HTTP Request] Brevo: Update ENGAGEMENT_SCORE

9. [End]

WICHTIG: Kein manuelles Prorating nötig!
ThriveCart Pro+ macht das automatisch.
Workflow 4: Engagement Score Calculator
yamlWorkflow Name: "Engagement_Score_Calculator"
Trigger: Schedule (täglich 02:00 Uhr)

Nodes:

1. [Schedule Trigger]
   ↓
2. [HTTP Request] Brevo: Get All Active Members
   Filter: BILLING_STATUS = "active"
   ↓
3. [Loop] For Each Contact:
   ↓ 4. [HTTP Request] Brevo: Get Email Stats (letzte 30 Tage)
   - email_opens
   - email_clicks
     ↓
   5. [HTTP Request] Circle API (via Zapier): Get Activity
      - community_logins
      - posts_created
      - sessions_attended (für ProGroup)
        ↓
   6. [Function] Calculate Engagement Score
      score = (
      (email_opens × 2) +
      (email_clicks × 5) +
      (community_logins × 10) +
      (posts_created × 15) +
      (sessions_attended × 20)
      )
      # Cap bei 100
      score = MIN(score, 100)
      ↓
   7. [HTTP Request] Brevo: Update Contact
      Attributes:
      - ENGAGEMENT_SCORE: score
      - LAST_ACTIVITY_AT: NOW()
        ↓
   8. [Switch] Check Score Thresholds

      IF score >= 61 AND PRODUCT_TIER = "ve" AND days_since_purchase >= 45:
      ↓
      9a. [HTTP Request] Brevo: Add to List "Hot_Leads"
      → Trigger Upsell VE → ProGroup

      IF score <= 30 AND days_since_activity >= 30:
      ↓
      9b. [HTTP Request] Brevo: Add to List "Cold_Leads"
      → Trigger Re-Engagement Flow

      ELSE:
      ↓
      9c. Continue Loop

4. [End]
   Workflow 5: Referral Handler
   yamlWorkflow Name: "Referral_Handler"
   Trigger: Webhook (Referral Tool - nach DOI validiert)

Nodes:

1. [Webhook] Receive Referral Event
   Payload:
   - referrer_email
   - referred_email
   - referral_id
     ↓
2. [HTTP Request] Brevo: Get Referrer Contact
   Filter: email = referrer_email
   ↓
3. [Function] Increment REF_COUNT
   current_count = contact.REF_COUNT
   new_count = current_count + 1
   ↓
4. [HTTP Request] Brevo: Update Referrer
   Attributes:
   - REF_COUNT: new_count
   - LAST_ACTIVITY_AT: NOW()
     ↓
5. [Switch] Check if Bonus Unlocked

   IF new_count >= 3 AND REF_BONUS_UNLOCKED = false:
   ↓
   6a. [HTTP Request] Brevo: Update Referrer
   Attributes: - REF_BONUS_UNLOCKED: true
   ↓
   7a. [HTTP Request] Brevo: Send Bonus Email
   Template: "🎉 Du hast 3 Referrals! Bonus freigeschaltet"
   ↓
   8a. [HTTP Request] Zapier: Circle Unlock Bonus Content
   Payload: - user_email: referrer_email - space: "Bonus_Perfect_Blending" - action: "grant_access"

   ELSE IF new_count = 2:
   ↓
   6b. [HTTP Request] Brevo: Send Encouragement Email
   Template: "Fast geschafft! Noch 1 Referral bis Bonus"

   ELSE:
   ↓
   6c. [HTTP Request] Brevo: Send Thank You Email
   Template: "Danke für deine Empfehlung!"

6. [End]

7. Zapier Setup (Circle Integration Bridge)
   Zap 1: Create Circle User on Purchase
   yamlZap Name: "ThriveCart → Circle User Creation"
   Trigger: Webhook by Zapier
   Webhook URL: [Provided by Zapier] → Use in n8n

Actions:

1. [Webhook] Receive from n8n
   Sample Payload:
   {
   "email": "user@example.com",
   "product_tier": "ve",
   "first_name": "John",
   "action": "create_or_update_role"
   }
   ↓
2. [Filter] Only Continue if action = "create_or_update_role"
   ↓
3. [Circle] Find Member by Email
   Email: {{email}}

   IF not found:
   ↓
   4a. [Circle] Create Member
   Email: {{email}}
   Name: {{first_name}}
   Send Invite: Yes

   ELSE:
   ↓
   4b. Continue to role update
   ↓

4. [Circle] Update Member Role
   Map product_tier to Circle Role:
   - "trial" → "Trial"
   - "ve" → "VocalEssentials"
   - "progroup" → "ProGroup"
   - "coaching" → "Coaching"
   - "mentorship" → "Coaching"
     ↓
5. [Circle] Grant Space Access based on Role
   IF role = "ProGroup" OR "Coaching":
   - Add to "ProGroup_Gruppencoaching"
   - Add to "ProGroup_Private_Lounge"

   IF role = "Coaching":
   - Add to "Coaching_1on1_Space"

6. [End]
   Zap 2: Circle Activity → Brevo Engagement
   yamlZap Name: "Circle Activity → Brevo Update"
   Trigger: Circle - New Post Created OR New Comment

Actions:

1. [Circle] Detect Activity
   Member Email: {{member_email}}
   Activity Type: {{activity_type}}
   ↓
2. [Brevo] Find Contact
   Email: {{member_email}}
   ↓
3. [Brevo] Update Contact
   Attributes:
   - LAST_ACTIVITY_AT: NOW()

   (Engagement Score wird täglich via n8n neu berechnet)

4. [End]

Note: Dieser Zap läuft auf jedem Circle-Event.
Rate Limit: Zapier Starter erlaubt 750 Tasks/Monat.
Bei 300 Usern × 10 Posts/Monat = 3.000 Tasks → Upgrade zu Professional nötig ($20/M).
Zap 3: Failed Payment → Circle Downgrade
yamlZap Name: "Brevo → Circle Downgrade on Failed Payment"
Trigger: Webhook by Zapier (from n8n after 7-day grace)

Actions:

1. [Webhook] Receive from n8n
   Payload:
   {
   "email": "user@example.com",
   "action": "downgrade_to_readonly"
   }
   ↓
2. [Circle] Find Member
   Email: {{email}}
   ↓
3. [Circle] Update Member Role
   New Role: "Read-Only"
   ↓
4. [Circle] Remove from Private Spaces
   Spaces to remove:
   - ProGroup_Gruppencoaching
   - ProGroup_Private_Lounge
   - Coaching_1on1_Space

   Keep access to:
   - VE_Masterclass_Hub (view-only)
   - VE_Community (read-only)

5. [End]
   Zap 4: Referral Bonus → Circle Unlock
   yamlZap Name: "Referral Bonus → Circle Space Unlock"
   Trigger: Webhook by Zapier (from n8n)

Actions:

1. [Webhook] Receive from n8n
   Payload:
   {
   "email": "user@example.com",
   "space": "Bonus_Perfect_Blending",
   "action": "grant_access"
   }
   ↓
2. [Circle] Find Member
   Email: {{email}}
   ↓
3. [Circle] Grant Space Access
   Space: "Bonus_Perfect_Blending"
   Access Level: Full Access
   ↓
4. [Circle] Add Member to Space
   Send Notification: Yes (Circle sendet automatische Email)

5. [End]

Customer Journeys
Journey 1: Lead → Trial → VocalEssentials (Monthly)
┌─────────────────────────────────────────────────────────┐
│ STAGE 1: LEAD ACQUISITION │
└─────────────────────────────────────────────────────────┘

User landet auf Webflow Landing Page: /cvt-mini-kurs
↓
[Webflow Form] Newsletter Opt-in

- Email
- Vorname
- (Optional) Wie hast du von uns gehört?
  ↓
  [Webflow → n8n Webhook]
  ↓
  [n8n] Create/Update Contact in Brevo
  Attributes:
- LEAD_SOURCE: Parsed from UTM or Form Field
- LEAD_DATE: NOW()
- REF_LINK: Generate unique link
  ↓
  [Brevo] Welcome Email (sofort)
  Subject: "Willkommen! Hier ist dein CVT Mini-Kurs 🎵"
  Content:
- CVT Mini-Kurs Link
- Referral-Link: "Teile mit 3 Freunden → Bonus"
- CTA: "Jetzt 7€ Trial starten"

┌─────────────────────────────────────────────────────────┐
│ STAGE 2: TRIAL CONVERSION │
└─────────────────────────────────────────────────────────┘

User klickt auf Trial-CTA in Email oder Website
↓
[ThriveCart Checkout] /trial

- Preis: 7€
- Order Bumps:
  ✓ Warm-Up Bundle (17€) - 25% nehmen es
  ✓ Stimmnotfallplan (19€) - 20% nehmen es
  ↓
  User completed checkout
  ↓
  [ThriveCart → n8n Webhook] subscription.charge.succeeded
  ↓
  [n8n] Update Brevo Contact
  Attributes:
- PRODUCT_TIER: "trial"
- BILLING_STATUS: "active"
- TRIAL_ENDS_AT: NOW() + 30 days
- TC_CUSTOMER_ID: "cus_xxx"
- TC_SUBSCRIPTION_ID: "sub_xxx"
  ↓
  [n8n → Zapier] Create Circle User
  Role: "Trial"
  Spaces: VE_Masterclass_Hub, VE_Ressourcen (view-only)
  ↓
  [Brevo] Trial Welcome Email (sofort nach Kauf)
  Subject: "Willkommen bei VocalEssentials! 🎉"
  Content:
- Circle Login-Daten
- Erste Schritte Guide
- Bonus: Kostenlose Stimmanalyse buchen (Cal.com)

┌─────────────────────────────────────────────────────────┐
│ STAGE 3: TRIAL NURTURE (30 Tage) │
└─────────────────────────────────────────────────────────┘

Day 1-22: User nutzt Trial

- Circle-Zugang
- Masterclasses anschauen
- (Optional) Stimmanalyse buchen → Cross-Sell Coaching

Day 7: Check-In Email
Subject: "Noch 23 Tage: Deine ersten CVT-Fortschritte?"

Day 23: First Conversion Push
Subject: "Dein Trial endet in 7 Tagen"
Content:

- Special Offer: Annual 347€ (save 217€)
- Payment Plan: 4x 97€
- Monthly: 47€/M

Day 27: Second Push
Subject: "Nur noch 3 Tage"

Day 29: Final Push
Subject: "LETZTE CHANCE"

┌─────────────────────────────────────────────────────────┐
│ STAGE 4A: CONVERSION SUCCESS (VE Monthly) │
└─────────────────────────────────────────────────────────┘

User klickt auf "47€/M Monthly" CTA
↓
[ThriveCart Checkout] Subscription Upgrade
ThriveCart Prorating:

- Trial läuft noch 5 Tage
- Credit: (5/30) × 7€ = 1,17€
- Erste VE-Zahlung: 47€ - 1,17€ = 45,83€
  ↓
  [ThriveCart → n8n Webhook] subscription.upgraded
  ↓
  [n8n] Update Brevo
  Attributes:
- PRODUCT_TIER: "ve"
- BILLING_CYCLE: "monthly"
- BILLING_STATUS: "active"
- TRIAL_ENDS_AT: null
  ↓
  [n8n → Zapier] Upgrade Circle Role
  Role: "VocalEssentials"
  New Access: VE_Community (full posting rights)
  ↓
  [Brevo] VE Welcome Email
  Subject: "Willkommen bei VocalEssentials - Dein Full Access ist live!"

User Journey continues → siehe Journey 2 (VE → ProGroup Upsell)

┌─────────────────────────────────────────────────────────┐
│ STAGE 4B: TRIAL EXPIRED - DOWNSELL │
└─────────────────────────────────────────────────────────┘

Day 30: Trial abgelaufen, keine Zahlung
↓
[ThriveCart] Auto-Cancel Subscription
↓
[ThriveCart → n8n Webhook] subscription.cancelled
↓
[n8n] Update Brevo
Attributes:

- BILLING_STATUS: "cancelled"
  ↓
  [n8n → Zapier] Circle Role Downgrade
  Role: "Inactive" (oder komplett entfernen)
  ↓
  [Brevo] Downsell Email (sofort nach Cancel)
  Subject: "Schade, dass du gehst... hier ist ein Special"
  Content:
- Downsell: Self-Study für 27€/M
  (Masterclasses ohne Community)
- Testimonials
- 60-Tage Geld-zurück-Garantie

IF User kauft Self-Study:
→ PRODUCT_TIER: "ve_self_study"
→ Circle: View-only access

IF User kauft nicht:
→ Bleibt in Newsletter
→ Re-Engagement Campaigns später

Journey 2: VocalEssentials → ProGroup Upsell
┌─────────────────────────────────────────────────────────┐
│ STARTING POINT: Active VE Member (Day 1) │
└─────────────────────────────────────────────────────────┘

User ist VE Member (47€/M)

- Nutzt Masterclasses
- Postet in Community
- Öffnet Emails

┌─────────────────────────────────────────────────────────┐
│ STAGE 1: ENGAGEMENT TRACKING (Day 1-45) │
└─────────────────────────────────────────────────────────┘

[n8n Daily Workflow] Engagement Score Calculator
↓
Berechnet ENGAGEMENT_SCORE täglich:

- Email Opens × 2
- Clicks × 5
- Circle Logins × 10
- Posts × 15
  ↓
  Score wird in Brevo gespeichert

┌─────────────────────────────────────────────────────────┐
│ STAGE 2: UPSELL QUALIFICATION (Day 45) │
└─────────────────────────────────────────────────────────┘

Day 45: n8n prüft Upsell-Berechtigung
Conditions:
✓ PRODUCT_TIER = "ve"
✓ BILLING_STATUS = "active"
✓ Days since VE purchase >= 45
✓ ENGAGEMENT_SCORE >= 60

IF alle Conditions erfüllt:
↓
[Brevo] Start Upsell Sequence
Add to List: "VE_Upsell_Eligible"

┌─────────────────────────────────────────────────────────┐
│ STAGE 3: UPSELL SEQUENCE (Day 45-52) │
└─────────────────────────────────────────────────────────┘

Day 45: Email 1
Subject: "Du rockst VocalEssentials! Ready für den nächsten Level?"
Content:

- Congratulations on Progress
- Introduce: ProGroup Membership
  → Live Gruppencoaching (2x/Monat)
  → Advanced Masterclasses
  → Direct Q&A mit Adrian
- Social Proof (ProGroup Testimonials)
- CTA: "Mehr erfahren"

Day 48: Email 2
Subject: "Die Wahrheit über Self-Study vs. Live-Coaching"
Content:

- Education: Benefits of Live Feedback
- Real Results: ProGroup Member Case Studies
- ProGroup Features Breakdown
- Special: Erste Gruppen-Session kostenlos testen
- CTA: "Jetzt upgraden"

Day 52: Email 3
Subject: "Nur 38€ mehr für Live-Coaching"
Content:

- ROI Calculation:
  47€ (VE) + 38€ = 85€ (ProGroup)
  = 2x Gruppensessions/Monat
  = 24 Sessions/Jahr
  = 3,54€ pro Session
- Payment Options:
  → 85€/M Monthly
  → 697€/J Annual (spare 467€!)
- Guarantee: 60 Tage Geld-zurück
- CTA: "Jetzt upgraden"

┌─────────────────────────────────────────────────────────┐
│ STAGE 4A: UPGRADE SUCCESS (ProGroup) │
└─────────────────────────────────────────────────────────┘

User klickt "Jetzt upgraden" → landet auf /pro-group Checkout

[ThriveCart Checkout]
Preisoptionen:
○ 85€/Monat
○ 697€/Jahr (SAVE 467€) ← Empfohlen

Order Bumps:
□ 30-Tage Übungsplan Chor (27€)
□ Blending Practice Paket (19€)

User wählt: 85€/Monat (im Beispiel)
↓
[ThriveCart] Subscription Upgrade mit Prorating

- VE läuft noch 15 Tage (von 30)
- Credit: (15/30) × 47€ = 23,50€
- Erste ProGroup Zahlung: 85€ - 23,50€ = 61,50€
- Ab nächstem Monat: 85€ normal
  ↓
  [ThriveCart → n8n Webhook] subscription.upgraded
  Payload:
- old_product: "VocalEssentials Monthly"
- new_product: "ProGroup Monthly"
- prorated_amount: 61,50€
- customer_id: "cus_xxx"
  ↓
  [n8n] Update Brevo Contact
  Attributes:
- PRODUCT_TIER: "progroup"
- BILLING_CYCLE: "monthly"
- LAST_UPSELL_OFFER_DATE: null (reset)
- ENGAGEMENT_SCORE: +20 Bonus
  ↓
  [n8n → Zapier] Upgrade Circle Role
  Old Role: "VocalEssentials"
  New Role: "ProGroup"

New Access:

- ProGroup_Gruppencoaching
- ProGroup_Private_Lounge

Action in Circle:

1. Update Member Role
2. Grant Space Access
3. Send Welcome DM
   ↓
   [Brevo] ProGroup Welcome Email
   Subject: "🎉 Willkommen bei ProGroup!"
   Content:

- Dein Upgrade ist aktiv
- Nächste Gruppensession: [Datum]
- Zugang zu Private Lounge
- Erste Schritte Guide
- CTA: "Erste Session buchen"

┌─────────────────────────────────────────────────────────┐
│ STAGE 4B: UPSELL DECLINED │
└─────────────────────────────────────────────────────────┘

User öffnet Emails nicht / klickt nicht auf CTA

Day 60: Sequenz endet
↓
[Brevo] Update Contact
Attributes:

- LAST_UPSELL_OFFER_DATE: NOW()
- LAST_UPSELL_OFFER_TYPE: "ve_to_progroup"

User bleibt VE Member
→ Nächster Upsell-Versuch frühestens in 60 Tagen

IF ENGAGEMENT_SCORE sinkt < 30:
→ Re-Engagement Flow startet

Journey 3: ProGroup → Coaching Programm Upsell
┌─────────────────────────────────────────────────────────┐
│ STARTING POINT: Active ProGroup Member (Day 1) │
└─────────────────────────────────────────────────────────┘

User ist ProGroup Member (85€/M)

- Besucht Gruppensessions regelmäßig
- Aktiv in Private Lounge
- Hoher Engagement Score

┌─────────────────────────────────────────────────────────┐
│ STAGE 1: QUALIFICATION TRACKING (Day 1-90) │
└─────────────────────────────────────────────────────────┘

[n8n Daily Workflow] Tracks:

- GROUP_SESSIONS_ATTENDED (via Circle/Zapier)
- ENGAGEMENT_SCORE
- Days since ProGroup purchase

┌─────────────────────────────────────────────────────────┐
│ STAGE 2: COACHING UPSELL QUALIFICATION (Day 90) │
└─────────────────────────────────────────────────────────┘

Day 90: n8n prüft Conditions
✓ PRODUCT_TIER = "progroup"
✓ BILLING_STATUS = "active"
✓ Days since ProGroup purchase >= 90
✓ GROUP_SESSIONS_ATTENDED >= 3
✓ ENGAGEMENT_SCORE >= 70

IF alle Conditions erfüllt:
↓
[n8n] Trigger "High-Intent Lead" Flag
↓
[Brevo] Start Coaching Upsell Sequence

┌─────────────────────────────────────────────────────────┐
│ STAGE 3: COACHING UPSELL SEQUENCE (Day 90-100) │
└─────────────────────────────────────────────────────────┘

Day 90: Email 1 (Anchor Upsell)
Subject: "Bereit für 1:1 Mastery?"
Content:

- Acknowledge Progress
- The Gap: Gruppencoaching vs. Personal Coaching
- Present 2 Options (Anchor Technique):

  Option A: CVT MENTORSHIP YEAR (4.997€)
  - 24 Sessions / 12 Monate
  - Unlimited WhatsApp Support
  - Quarterly Live-Events
  - Guarantee: Professional Level

  Option B: COACHING PROGRAMM (1.500€)
  - 8 Sessions / 4 Monate
  - Strukturiertes CVT-Programm
  - Inkl. 6 Monate ProGroup (Wert 510€)
  - WhatsApp Support während Programm

- CTA: "15-Min Discovery Call buchen"

Day 94: Email 2 (Rollover Credit)
Subject: "Du hast bereits 270€ Credit für Coaching"
Content:

- Rollover-Credit Erklärung:
  "Du bist seit 90 Tagen ProGroup Member
  = 3 × 85€ = 255€ bezahlt

  Bei Coaching-Upgrade rechnen wir dir
  diese 255€ voll an!

  Coaching Programm (1.500€)
  - 255€ Credit
    = 1.245€ für dich"

- Social Proof: Coaching Success Stories
- CTA: "Jetzt upgraden mit Credit"

Day 98: Email 3 (Final Push)
Subject: "Letzter Tag: Credit-Angebot endet"
Content:

- Urgency (echte Deadline setzen!)
- FAQ zu Coaching
- Guarantee: Geld-zurück bei Unzufriedenheit
- CTA: "Jetzt buchen"

┌─────────────────────────────────────────────────────────┐
│ STAGE 4A: COACHING PURCHASE SUCCESS │
└─────────────────────────────────────────────────────────┘

User klickt CTA → landet auf /choir-accelerator

[ThriveCart Checkout]
Preis: 1.500€ einmalig

ABER: n8n berechnet Rollover Credit

- ProGroup seit 90 Tagen
- 3 × 85€ = 255€ bezahlt
- Custom Discount Code in TC: "-255€"
- Final Price: 1.245€

Order Bumps:
□ Extra Coaching Session (97€)
□ Blending Practice Paket (19€)

User completed checkout
↓
[ThriveCart → n8n Webhook] order.success
↓
[n8n Complex Workflow]

1. Update Brevo Contact
   Attributes:
   - PRODUCT_TIER: "coaching"
   - BILLING_STATUS: "active"
   - COACHING_SESSIONS_REMAINING: 8
   - COACHING_PACKAGE_EXPIRES_AT: NOW() + 6 months

2. ThriveCart API Call: Create ProGroup Subscription
   - Product: ProGroup Monthly (85€/M)
   - First 6 payments: Paused (inkludiert in Coaching)
   - Start billing after 6 months

3. Brevo: Cancel old ProGroup Subscription
   (wird ersetzt durch neue Subscription aus Schritt 2)

4. Zapier: Update Circle Role
   - Role: "Coaching"
   - New Access: Coaching_1on1_Space
   - Keep: Alle ProGroup Spaces

5. Brevo: Send Coaching Welcome Email
   Subject: "Willkommen im Coaching Programm! 🎯"
   Content:
   - Erste Session buchen (Cal.com Link)
   - Zugang zu Coaching Space
   - WhatsApp-Gruppe Einladung
   - Onboarding Workbook

┌─────────────────────────────────────────────────────────┐
│ STAGE 4B: COACHING DECLINED - DOWNSELL │
└─────────────────────────────────────────────────────────┘

User öffnet Emails nicht / lehnt ab

Day 105: Downsell Email
Subject: "Kein Problem - hier ist eine Alternative"
Content:

- Downsell: Coaching Light (997€)
  → 8 Sessions
  → Kein ProGroup inkludiert
  → Basic Support (Email only)
- Oder: Einzelcoaching Session (97€)
  → Teste 1 Session
  → Kein Commitment

IF weiterhin keine Conversion:
→ User bleibt ProGroup Member
→ Nächster Coaching-Upsell in 6 Monaten

Journey 4: Payment Plan User Journey
┌─────────────────────────────────────────────────────────┐
│ SCENARIO: VE Annual abgelehnt → Payment Plan Downsell │
└─────────────────────────────────────────────────────────┘

User im Trial, will zu VE upgraden
↓
[ThriveCart Checkout] /vocal-essentials

Primary Offer: 347€ Jährlich (SAVE 217€)
↓
User klickt "Zurück" (zu teuer)
↓
[ThriveCart] Downsell-Page
Headline: "Kein Problem! Zahle in Raten"

Optionen:
○ 4x 97€ (= 388€ total, 41€ mehr als Annual)
○ Zurück zu 47€/Monat

User wählt: 4x 97€
↓
[ThriveCart] Subscription mit Split-Pay
Product: "VocalEssentials Payment Plan 4x"
↓
Checkout Success
↓
[ThriveCart → n8n Webhook] subscription.charge.succeeded
Payload:

- installment.current: 1
- installment.total: 4
- amount: 97€

┌─────────────────────────────────────────────────────────┐
│ STAGE 1: FIRST PAYMENT │
└─────────────────────────────────────────────────────────┘

[n8n Workflow] TC_Purchase_Handler
↓
Detect: installment = 1 (First Payment)
↓
[n8n] Create Brevo Contact
Attributes:

- PRODUCT_TIER: "ve"
- BILLING_CYCLE: "payment_plan"
- BILLING_STATUS: "active"
- PAYMENT_PLAN_TOTAL: 4
- PAYMENT_PLAN_PAID: 1
- PAYMENT_PLAN_NEXT_DUE: NOW() + 30 days
- TC_CUSTOMER_ID: "cus_xxx"
- TC_SUBSCRIPTION_ID: "sub_xxx"
  ↓
  [n8n → Zapier] Create Circle User
  Role: "VocalEssentials"
  ↓
  [Brevo] VE Welcome Email
  Subject: "Willkommen bei VocalEssentials!"
  Content:
- Full Access aktiviert
- Dein Payment Plan: 3 weitere Raten à 97€
- Nächste Zahlung: [Datum]

┌─────────────────────────────────────────────────────────┐
│ STAGE 2: INSTALLMENT 2 (30 Tage später) │
└─────────────────────────────────────────────────────────┘

Day 30: ThriveCart Auto-Rebill
↓
[ThriveCart → n8n Webhook] subscription.charge.succeeded
Payload:

- installment.current: 2
- installment.total: 4
- amount: 97€
  ↓
  [n8n Workflow] TC_Purchase_Handler
  ↓
  Detect: installment = 2 (NOT first payment)
  ↓
  [n8n] Update Brevo Contact
  Attributes:
- PAYMENT_PLAN_PAID: 2
- PAYMENT_PLAN_NEXT_DUE: NOW() + 30 days
- LAST_ACTIVITY_AT: NOW()
  ↓
  [Brevo] Payment Success Email (Optional)
  Subject: "Zahlung erfolgreich - 2 von 4 Raten bezahlt"

┌─────────────────────────────────────────────────────────┐
│ STAGE 3: FAILED PAYMENT (Beispiel in Monat 3) │
└─────────────────────────────────────────────────────────┘

Day 60: ThriveCart versucht Rebill
↓
Payment FAILED (z.B. Karte abgelaufen)
↓
[ThriveCart → n8n Webhook] subscription.charge.failed
Payload:

- installment.current: 3
- installment.total: 4
- reason: "card_expired"
  ↓
  [n8n Workflow] TC_Failed_Payment_Handler
  ↓
  [n8n] Update Brevo
  Attributes:
- BILLING_STATUS: "paused"
  ↓
  [ThriveCart] Subscription Saver (automatisch)
- Auto-Retry nach 3, 5, 7 Tagen
- Emails an User: "Update deine Zahlungsmethode"
  ↓
  [n8n] Start Grace Period (7 Tage)
  ↓
  Day 0: Brevo Email
  Subject: "Zahlung fehlgeschlagen - bitte aktualisieren"

Day 3: Brevo Email
Subject: "Reminder: Update deine Zahlung"

Day 7: Brevo Email
Subject: "Letzter Tag: Dein Zugang läuft heute ab"

↓
IF Payment noch nicht gefixt nach 7 Tagen:
↓
[n8n → Zapier] Downgrade Circle Role
Action: "downgrade_to_readonly"
User kann Content sehen, aber nicht nutzen
↓
Day 14: Kompletter Entzug
[n8n → Zapier] Remove Circle Access

┌─────────────────────────────────────────────────────────┐
│ STAGE 4A: PAYMENT FIXED (within Grace Period) │
└─────────────────────────────────────────────────────────┘

Day 5: User updated Zahlungsmethode in ThriveCart
↓
[ThriveCart] Retry Payment → SUCCESS
↓
[ThriveCart → n8n Webhook] subscription.charge.succeeded
Payload:

- installment.current: 3
- installment.total: 4
- amount: 97€
  ↓
  [n8n] Update Brevo
  Attributes:
- BILLING_STATUS: "active"
- PAYMENT_PLAN_PAID: 3
  ↓
  [Brevo] Success Email
  Subject: "Zahlung erfolgreich - Zugang wiederhergestellt"

┌─────────────────────────────────────────────────────────┐
│ STAGE 4B: FINAL INSTALLMENT │
└─────────────────────────────────────────────────────────┘

Day 90: ThriveCart Rebill Installment 4
↓
[ThriveCart → n8n Webhook] subscription.charge.succeeded
Payload:

- installment.current: 4
- installment.total: 4
- amount: 97€
  ↓
  PLUS
  [ThriveCart → n8n Webhook] subscription.completed
  ↓
  [n8n Workflow] Payment Plan Completion Handler
  ↓

1. Update Brevo
   Attributes:
   - PAYMENT_PLAN_PAID: 4
   - BILLING_STATUS: "completed"

2. ThriveCart API: Convert to Monthly Subscription
   Action: Create new subscription
   Product: VocalEssentials Monthly (47€/M)
   First billing: NOW() + 30 days

3. Update Brevo
   Attributes:
   - BILLING_CYCLE: "monthly"
   - BILLING_STATUS: "active"
   - TC_SUBSCRIPTION_ID: [new_sub_id]
   - PAYMENT_PLAN_TOTAL: null (clear)
   - PAYMENT_PLAN_PAID: null (clear)

4. Brevo Email
   Subject: "Glückwunsch! Payment Plan abgeschlossen"
   Content:
   - Du hast alle 4 Raten bezahlt
   - Ab jetzt: 47€/Monat automatisch
   - Jederzeit kündbar
   - Danke für dein Vertrauen

User ist jetzt regulärer VE Monthly Member
→ Upsell zu ProGroup möglich ab Day 45

Automation Workflows
Critical Path Automations (Phase 1 - Launch-kritisch)

1. Newsletter Opt-in Flow
   Trigger: Webflow Form Submit (/cvt-mini-kurs)
   Frequency: ~100x/Monat (Ziel)

Flow:

1. Webflow → n8n Webhook
2. Parse Form Data (email, name, utm_source)
3. Brevo API: Create or Update Contact
   - LEAD_SOURCE
   - LEAD_DATE
   - REF_LINK (generate)
4. Brevo API: Add to List "Newsletter"
5. Trigger Welcome Sequence (automatisch in Brevo)

Error Handling:

- IF Brevo API fails: Retry 3x
- Log error to n8n Table "errors"
- Alert via Email nach 3 Failed Attempts

SLA: < 5 Minuten 2. Trial Purchase Flow
Trigger: ThriveCart Webhook (subscription.charge.succeeded)
Frequency: ~10x/Monat (Monat 1), später mehr

Flow:

1. n8n Webhook receives ThriveCart Event
2. Validate Webhook Signature (Security)
3. Parse Event Data
4. Check: First Payment or Installment?

   IF First Payment:
   5a. Brevo API: Update Contact - PRODUCT_TIER: "trial" - BILLING_STATUS: "active" - TRIAL_ENDS_AT: NOW() + 30 days - TC_CUSTOMER_ID - TC_SUBSCRIPTION_ID
   6a. Zapier Webhook: Create Circle User - Role: "Trial"
   7a. Brevo API: Send Trial Welcome Email

   ELSE (Installment):
   5b. Brevo API: Update PAYMENT_PLAN_PAID
   6b. (Skip Circle creation)
   7b. (Skip Welcome Email)

5. Log Event to n8n Table "events_log"

Error Handling:

- Idempotency Check (event_log)
- Retry failed Brevo/Zapier calls 3x
- Alert if subscription data incomplete

SLA: < 2 Minuten 3. Trial Reminder Automation
Trigger: Brevo Automation (attribute-based)
Condition: TRIAL_ENDS_AT = [specific date]

Setup in Brevo:

- Workflow 1: TRIAL_ENDS_AT = TODAY + 7 days
  → Send Email "Dein Trial endet in 7 Tagen"
- Workflow 2: TRIAL_ENDS_AT = TODAY + 3 days
  → Send Email "Nur noch 3 Tage"
- Workflow 3: TRIAL_ENDS_AT = TODAY + 1 day
  → Send Email "LETZTE CHANCE"
- Workflow 4: TRIAL_ENDS_AT = TODAY AND BILLING_STATUS = "cancelled"
  → Send Downsell Email "Self-Study für 27€/M"

Keine n8n Workflows nötig - Brevo macht das nativ!

SLA: Emails senden um 10:00 Uhr (optimale Open Rate) 4. Subscription Upgrade (VE → ProGroup)
Trigger: ThriveCart Webhook (subscription.upgraded)
Frequency: ~2-3x/Monat (20% von VE Members)

Flow:

1. n8n Webhook receives Upgrade Event
2. Extract:
   - old_product_id
   - new_product_id
   - customer_id
   - prorated_amount (from ThriveCart)
3. Map Product IDs to Tiers
4. Brevo API: Update Contact
   - PRODUCT_TIER: "progroup"
   - ENGAGEMENT_SCORE: += 20
   - LAST_UPSELL_OFFER_DATE: null
5. Zapier Webhook: Update Circle Role
   - New Role: "ProGroup"
   - Grant Spaces: ProGroup_Gruppencoaching, ProGroup_Private_Lounge
6. Brevo API: Send ProGroup Welcome Email

Error Handling:

- IF Zapier fails: Queue for manual review
- IF Brevo fails: Retry, then alert

SLA: < 5 Minuten

WICHTIG: Kein Prorating in n8n nötig!
ThriveCart Pro+ macht das automatisch. 5. Failed Payment Handler
Trigger: ThriveCart Webhook (subscription.charge.failed)
Frequency: ~5-10% aller Rebills (Industry Standard)

Flow:

1. n8n Webhook receives Failed Payment
2. Brevo API: Update Contact
   - BILLING_STATUS: "paused"
3. Brevo API: Start Dunning Email Sequence
   (läuft parallel zu ThriveCart Subscription Saver)
4. n8n Delay Node: 7 Tage
5. Brevo API: Check BILLING_STATUS

   IF still "paused":
   6a. Zapier: Downgrade Circle to Read-Only
   7a. n8n Delay: 7 weitere Tage
   8a. IF still "paused": - Zapier: Remove Circle Access - Brevo: Remove from Active Lists

   ELSE (Payment fixed):
   6b. End (ThriveCart handled retry)

Error Handling:

- Log all Failed Payments für Monitoring
- Alert bei > 10% Failed Payment Rate

SLA: Grace Period = 7 Tage (nicht ändern!)

Advanced Automations (Phase 2) 6. Engagement Score Calculator
Trigger: n8n Schedule (täglich 02:00 Uhr)
Frequency: 1x/Tag

Flow:

1. Brevo API: Get All Contacts with BILLING_STATUS = "active"
2. FOR EACH Contact: 3. Brevo API: Get Email Stats (letzte 30 Tage)
   - email_opens
   - email_clicks
   4. Zapier → Circle API: Get User Activity
      - community_logins
      - posts_created
      - sessions_attended (via Calendar Events)
   5. Calculate Engagement Score
      score = (email_opens × 2) +
      (email_clicks × 5) +
      (community_logins × 10) +
      (posts_created × 15) +
      (sessions_attended × 20)
      score = MIN(score, 100)
   6. Brevo API: Update Contact
      - ENGAGEMENT_SCORE: score
      - LAST_ACTIVITY_AT: NOW()
   7. Check Thresholds:

      IF score >= 61 AND PRODUCT_TIER = "ve" AND days_since >= 45:
      8a. Brevo API: Add to List "Hot_Leads"
      → Trigger Upsell Sequence

      IF score <= 30 AND days_since_activity >= 30:
      8b. Brevo API: Add to List "Cold_Leads"
      → Trigger Re-Engagement

      ELSE:
      8c. Continue Loop

3. END

Performance:

- 300 Contacts × 5 API Calls = 1.500 Calls/Tag
- Runtime: ~15 Minuten
- Zapier Tasks: 300/Tag = 9.000/Monat (OK mit Professional Plan)

Error Handling:

- Skip contacts with API errors (don't break loop)
- Log errors for manual review
- Alert wenn > 10% Contacts skipped

7. Referral Handler
   Trigger: Referral Tool Webhook (nach DOI validiert)
   Frequency: ~10-15x/Monat (mit Referral-Programm Growth)

Flow:

1. n8n Webhook receives Referral Event
   Payload:
   - referrer_email
   - referred_email
   - referral_id

2. Brevo API: Get Referrer Contact by email

3. Function Node: Increment REF_COUNT
   current = contact.REF_COUNT
   new = current + 1

4. Brevo API: Update Referrer
   - REF_COUNT: new
   - LAST_ACTIVITY_AT: NOW()

5. Switch: Check Bonus Unlock

   IF new >= 3 AND REF_BONUS_UNLOCKED = false:
   6a. Brevo API: Update Referrer - REF_BONUS_UNLOCKED: true
   7a. Brevo API: Send Bonus Email
   Subject: "🎉 Du hast 3 Referrals! Bonus freigeschaltet"
   8a. Zapier Webhook: Circle Unlock Bonus - Space: "Bonus_Perfect_Blending" - User: referrer_email

   ELSE IF new = 2:
   6b. Brevo API: Send Encouragement
   Subject: "Fast geschafft! Noch 1 Referral"

   ELSE:
   6c. Brevo API: Send Thank You
   Subject: "Danke für deine Empfehlung!"

6. Log to events_log (idempotency)

Error Handling:

- Validate referrer exists in Brevo
- IF not found: Create Lead first
- Retry Zapier call 3x

SLA: < 5 Minuten 8. Coaching Session Booking Handler
Trigger: Cal.com Webhook (booking.created)
Frequency: ~5-10x/Monat (für Coaching Clients)

Flow:

1. n8n Webhook receives Booking Event
   Payload:
   - attendee_email
   - session_type (1on1 / group)
   - scheduled_date

2. Brevo API: Get Contact by email

3. Function: Decrement COACHING_SESSIONS_REMAINING
   remaining = contact.COACHING_SESSIONS_REMAINING - 1

4. Brevo API: Update Contact
   - COACHING_SESSIONS_REMAINING: remaining
   - LAST_ACTIVITY_AT: NOW()

5. IF remaining = 0:
   6a. Brevo API: Trigger "Package Expiring" Email
   Subject: "Dein Coaching-Paket ist aufgebraucht"
   Content: - Extend Package? (Buy more sessions) - Upgrade to Mentorship?

   ELSE IF remaining <= 2:
   6b. Brevo API: Send Reminder
   Subject: "Nur noch [X] Sessions übrig"

6. Circle API (via Zapier): Post to Coaching Space
   Message: "[Name] hat Session gebucht für [Date]"

Error Handling:

- Validate Contact has Coaching Package
- IF no package: Alert für manual review

SLA: < 2 Minuten

Implementation Roadmap
Phase 1: Core Funnel (Wochen 1-4)
Ziel: Launch-fähiges MVP mit Trial → VE Flow
Woche 1: Setup & Foundations
Tag 1-2: Tool Accounts & Basis-Setup

ThriveCart Pro+ Account verifizieren
Brevo Contact Attributes erstellen (Phase 1 Schema)
n8n Self-Hosted Instance bereitstellen
Zapier Account verbinden mit Circle

Tag 3-4: ThriveCart Produkte

Produkt 1: Trial (7€) erstellen
Produkt 2: VE Monthly (47€) erstellen
Produkt 3: VE Annual (347€) erstellen
Produkt 4: Self-Study (27€) Downsell erstellen
Webhooks konfigurieren → n8n Endpoint

Tag 5-7: Circle Spaces Setup

Willkommens-Space erstellen
VE_Masterclass_Hub erstellen (7 Masterclasses hochladen)
VE_Ressourcen Space (PDFs hochladen)
VE_Community Space
Member Roles definieren (Trial, VE)

Woche 2: Automationen Core
Tag 8-10: n8n Workflows bauen

Workflow 1: Newsletter Opt-in (Webflow → Brevo)
Workflow 2: TC Purchase Handler (ThriveCart → Brevo + Circle)
Workflow 3: Failed Payment Handler (mit 7-Tage Grace)
Workflow 4: Subscription Upgrade Handler (VE Prorating)

Tag 11-12: Zapier Zaps erstellen

Zap 1: Create Circle User on Purchase
Zap 2: Circle Activity → Brevo Update
Zap 3: Failed Payment → Circle Downgrade

Tag 13-14: Testing

Test Full Flow: Webflow → Newsletter
Test Trial Purchase → Circle Creation
Test VE Upgrade → Prorating
Test Failed Payment → Grace Period

Woche 3: Email Sequences in Brevo
Tag 15-17: Welcome Sequences

Newsletter Welcome (7 Emails, Day 0-7)
Trial Welcome (1 Email, sofort nach Kauf)
VE Welcome (1 Email, nach Upgrade)

Tag 18-19: Trial Conversion Sequence

Day 7 Email: Check-In
Day 23 Email: First Push (7 Tage vor Ende)
Day 27 Email: Second Push
Day 29 Email: Final Push
Day 30 Email: Downsell (wenn cancelled)

Tag 20-21: Testing & Refinement

Test alle Email-Sequenzen (Preview)
Test Trigger Conditions in Brevo
A/B Test Subject Lines vorbereiten

Woche 4: Landing Pages & Launch Prep
Tag 22-24: Webflow Landing Pages

/cvt-mini-kurs (Lead Magnet Page)
/trial (Trial Checkout Upsell Landing)
/vocal-essentials (VE Landing Page)

Tag 25-26: Order Bumps

Warm-Up Bundle (17€) in ThriveCart
Stimmnotfallplan (19€) in ThriveCart
PDFs erstellen & Upload zu Circle

Tag 27-28: Final Testing

End-to-End Test: Lead → Trial → VE → Circle
Test Payment Plan Flow
Test Failed Payment Scenarios
Test Downsells

Tag 29: Soft Launch

Launch für Beta-Gruppe (10-20 Leads)
Monitor Workflows live
Fix Bugs in Echtzeit

Tag 30: Public Launch

Newsletter an 300 Abonnenten
Social Media Ankündigung
Monitor Analytics

Phase 2: Upsell Layer (Wochen 5-8)
Ziel: ProGroup Membership einführen + Engagement Scoring
Woche 5: ProGroup Setup
Tag 31-33: ThriveCart Produkte

Produkt 5: ProGroup Monthly (85€)
Produkt 6: ProGroup Annual (697€)
Produkt 7: ProGroup Payment Plan (3x 247€)
Order Bumps (30-Tage Übungsplan, Blending Paket)

Tag 34-36: Circle ProGroup Spaces

ProGroup_Gruppencoaching Space
ProGroup_Private_Lounge
Member Role "ProGroup" erstellen
Kalendersystem für Gruppensessions (Cal.com Integration)

Tag 37: Upgrade Flow Testing

Test VE → ProGroup Upgrade mit Prorating
Test Circle Role Upgrade
Test Payment Plan ProGroup

Woche 6: Engagement Scoring
Tag 38-40: n8n Engagement Calculator

Workflow 5: Engagement Score Calculator (täglich)
Integration: Brevo Email Stats API
Integration: Circle Activity via Zapier
Scoring-Formel implementieren

Tag 41-42: Brevo Segmente

Segment: Hot_Leads (Score >= 61)
Segment: Cold_Leads (Score <= 30)
Segment: VE_Upsell_Eligible

Tag 43-44: Testing

Test Score-Berechnung mit Test-Daten
Verify Segment-Updates
Test Upsell-Trigger Logic

Woche 7: Upsell Email Sequences
Tag 45-47: VE → ProGroup Upsell Sequence

Email 1: "Ready für den nächsten Level?" (Day 45)
Email 2: "Self-Study vs. Live-Coaching" (Day 48)
Email 3: "Nur 38€ mehr" (Day 52)

Tag 48-49: Re-Engagement Sequence

Email 1: "Wir vermissen dich" (Day 30 inactive)
Email 2: "Neue Masterclass" (Day 37)
Email 3: "Pausieren oder Downgrade?" (Day 44)

Tag 50-51: Testing

Test Upsell Trigger (45 Tage nach VE)
Test Engagement Score Conditions
A/B Test Subject Lines

Woche 8: Launch ProGroup
Tag 52-54: Soft Launch

Manuell erste 5 VE Members zu ProGroup einladen
Erste Gruppensession durchführen
Feedback sammeln

Tag 55-56: Automation Launch

Automatische Upsell-Emails aktivieren
Monitor Conversion Rates
Optimize Email Copy basierend auf Opens/Clicks

Tag 57: Review & Iterate

KPIs analysieren:

VE → ProGroup Conversion Rate (Ziel: 20%)
Email Open Rates (Ziel: 30%+)
Click Rates (Ziel: 5%+)

Anpassungen vornehmen

Phase 3: Advanced Features (Wochen 9-12)
Ziel: Coaching Programm, Referral, Payment Plans erweitern
Woche 9: Coaching Setup
Tag 58-60: ThriveCart Coaching Produkte

Produkt 7: Coaching Programm (1.500€)
Produkt 8: Coaching Light Downsell (997€)
Produkt 9: Einzelcoaching Session (97€)
n8n: Rollover Credit Calculator für ProGroup → Coaching

Tag 61-63: Circle Coaching Space

Coaching_1on1_Space erstellen
Cal.com Integration für Session-Buchung
Member Role "Coaching" erstellen

Tag 64: Testing

Test Coaching Purchase Flow
Test Rollover Credit Berechnung
Test ProGroup Subscription Pause (6 Monate)

Woche 10: Referral System finalisieren
Tag 65-67: Referral Logic

n8n Workflow 6: Referral Handler (80% fertig → 100%)
Referral-Link Generation beim Opt-in
Bonus-Freischaltung bei 3 Referrals

Tag 68-69: Bonus Content

"Perfektes Blending" Masterclass erstellen
Circle Bonus Space erstellen
Zapier: Auto-Unlock bei REF_BONUS_UNLOCKED = true

Tag 70-71: Testing

Test Referral-Link Tracking
Test Bonus-Freischaltung Automation
Test Referral Emails

Woche 11: Payment Plans erweitern
Tag 72-74: Zusätzliche Payment Plans

VE 6x 67€ (optional, nur wenn Nachfrage)
ProGroup 6x 127€ (optional)
n8n: Payment Plan Completion Handler

Tag 75-76: Failed Payment Optimization

Verbesserte Dunning Emails (A/B Testing)
Retry-Strategie verfeinern
Circle Grace Period Policy dokumentieren

Tag 77-78: Testing

Test alle Payment Plan Varianten
Test Final Installment → Monthly Conversion
Test Failed Payment → Recovery

Woche 12: Analytics & Reporting
Tag 79-81: Reporting Setup

n8n → Google Sheets Daily Snapshot

Neue Leads (nach Source)
Trial Starts
VE Conversions
ProGroup Upgrades
MRR
Churn Rate

Looker Studio Dashboard erstellen

Tag 82-84: Optimization

Analyze Conversion Funnels
Identify Drop-Off Points
Optimize Low-Performing Emails

Tag 85: Phase 3 Review

KPIs Review:

Trial → VE Conversion (Ziel: 15%)
VE → ProGroup (Ziel: 20%)
Referral Rate (Ziel: 10%)
Churn Rate (Ziel: < 10%/Monat)

Plan Phase 4 (Mentorship, Advanced Automation)

Testing & Quality Assurance
Test Plan

1. Unit Tests (pro Workflow)
   Newsletter Opt-in Flow
   Test Cases:
   ✓ Valid Email → Brevo Contact erstellt
   ✓ Duplicate Email → Brevo Contact updated (kein Error)
   ✓ Invalid Email → Error logged, kein Brevo Call
   ✓ UTM Parameters → Korrekt in LEAD_SOURCE gespeichert
   ✓ Referral Link → Generiert und in REF_LINK gespeichert
   ✓ Welcome Email → Triggered innerhalb 5 Min

Error Cases:
✗ Brevo API down → Retry 3x, dann Email Alert
✗ Webhook Timeout → Queue für späteren Retry
Trial Purchase Flow
Test Cases:
✓ First Payment → Brevo + Circle erstellt
✓ Order Bump Selected → Zusätzlicher Revenue tracked
✓ TRIAL_ENDS_AT → Korrekt 30 Tage in Zukunft
✓ Circle Role → "Trial" assigned
✓ Welcome Email → Gesendet mit korrektem Circle-Link

Edge Cases:
✓ User kauft Trial 2x (Duplicate) → Idempotency Check
✓ ThriveCart sendet Duplicate Webhook → Nur 1x verarbeitet
✓ Payment succeeded aber Webhook delayed → Retry-Logic
Subscription Upgrade (VE → ProGroup)
Test Cases:
✓ Upgrade Webhook → Brevo PRODUCT_TIER updated
✓ ThriveCart Prorating → Korrekt berechnet (keine n8n-Logic nötig)
✓ Circle Role Upgrade → "ProGroup" assigned
✓ ProGroup Spaces → Access granted
✓ Welcome Email → Gesendet

Financial Tests:
✓ VE läuft 10 Tage → Upgrade → Prorated korrekt
✓ VE läuft 25 Tage → Upgrade → Prorated korrekt
✓ Annual zu Annual Upgrade → Prorated korrekt
Failed Payment Handler
Test Cases:
✓ Payment fails → BILLING_STATUS "paused"
✓ Dunning Emails → Senden Day 0, 3, 7
✓ Grace Period 7 Tage → Circle noch aktiv
✓ Day 7 ohne Payment → Circle Downgrade zu Read-Only
✓ Day 14 ohne Payment → Circle Access entfernt

Recovery Tests:
✓ Payment fixed Day 3 → Dunning stoppt, Circle bleibt aktiv
✓ Payment fixed Day 10 → Circle Re-Aktivierung 2. Integration Tests (End-to-End)
Full Funnel Test: Lead → Coaching
Scenario: Neuer Lead wird Coaching Client

Steps:

1. Webflow Form Submit
   ✓ Email in Brevo
   ✓ Welcome Email empfangen
   ✓ Referral Link generiert

2. Trial Purchase (7€)
   ✓ Circle Account erstellt
   ✓ Trial Welcome Email
   ✓ Masterclasses zugänglich

3. Wait 25 Tage (simuliert via TRIAL_ENDS_AT manipulation)
   ✓ Trial Reminder Emails
   ✓ Day 27, 29 Emails

4. Upgrade zu VE Annual (347€)
   ✓ Prorating korrekt
   ✓ Circle Role "VocalEssentials"
   ✓ Community-Zugang aktiv

5. Wait 45 Tage (simuliert)
   ✓ ENGAGEMENT_SCORE >= 60
   ✓ Upsell Email VE → ProGroup

6. Upgrade zu ProGroup (85€/M)
   ✓ Prorating korrekt
   ✓ Circle ProGroup Spaces
   ✓ ProGroup Welcome

7. Wait 90 Tage
   ✓ Coaching Upsell Email
   ✓ Rollover Credit berechnet

8. Purchase Coaching (1.500€)
   ✓ ProGroup Subscription pausiert 6 Monate
   ✓ Circle Coaching Role
   ✓ Coaching Space Access

Expected Total Time: ~3 Stunden (mit Simulation)
Expected Revenue: 7€ + 347€ + (85€×3) + 1.500€ = 2.109€
Payment Plan Full Cycle
Scenario: User kauft VE 4x 97€ Payment Plan

Steps:

1. Purchase 4x 97€
   ✓ Installment 1 → Circle Access
   ✓ PAYMENT_PLAN_PAID: 1
   ✓ Welcome Email

2. Wait 30 Tage → Installment 2
   ✓ Auto-Rebill success
   ✓ PAYMENT_PLAN_PAID: 2

3. Wait 30 Tage → Installment 3 FAILS
   ✓ BILLING_STATUS "paused"
   ✓ Dunning Emails start
   ✓ Circle noch aktiv (Grace Period)

4. User fixed Payment Day 5
   ✓ Installment 3 success
   ✓ BILLING_STATUS "active"
   ✓ Dunning stoppt

5. Wait 30 Tage → Installment 4 (Final)
   ✓ subscription.completed Webhook
   ✓ Auto-Convert zu VE Monthly (47€/M)
   ✓ BILLING*CYCLE: "monthly"
   ✓ PAYMENT_PLAN*\* cleared

Expected Total Time: ~2 Stunden (mit Fast-Forward)
Expected Total Paid: 388€
Expected Next Bill: 47€/M 3. User Acceptance Testing (UAT)
Beta Group Testing (10-20 Users)
Week 1: Soft Launch

- Invite 10 existing contacts to Trial
- Monitor alle Workflows live
- Collect Feedback:
  ✓ Circle Onboarding klar?
  ✓ Masterclasses zugänglich?
  ✓ Emails hilfreich?
  ✓ Payment Process smooth?

Week 2: Iterate

- Fix Bugs
- Optimize Email Copy
- Improve Circle UX

Week 3: Expand

- Invite weitere 10 Users
- Test Upsell Flows (VE → ProGroup)

Week 4: Full Launch

- Open to alle 300 Newsletter-Abonnenten

4. Performance Testing
   Load Testing
   Scenario: 100 Signups an einem Tag (Black Friday)

Test:

- Simulate 100 Webflow Form Submits in 1 Stunde
- Monitor:
  ✓ n8n Execution Times (< 5 Sek pro Workflow)
  ✓ Brevo API Rate Limits (300 Calls/Min)
  ✓ Zapier Task Usage (750 Tasks/Monat Limit!)
  ✓ Circle API (no public rate limits, aber monitor)

Expected Bottlenecks:
⚠ Zapier Tasks: 100 User Creations = 100 Tasks
→ Bei 750 Tasks/Monat Limit kritisch
→ Empfehlung: Upgrade zu Professional (750 → 2.000 Tasks)

⚠ n8n Self-Hosted: CPU/Memory Usage
→ Monitor Server Metrics
→ Scale vertically wenn nötig

Error Monitoring & Alerting
Critical Alerts (Sofort Email/SMS)
yamlAlert 1: ThriveCart Webhook Failed
Condition: n8n Workflow fails 3x für gleichen Event
Action: Email + SMS an Adrian
Severity: CRITICAL (Money at risk)

Alert 2: Brevo API Down
Condition: Brevo API returns 5xx error > 10 Min
Action: Email
Severity: HIGH (User Experience affected)

Alert 3: Circle User Creation Failed
Condition: Zapier fails to create User
Action: Queue for manual review + Email
Severity: MEDIUM (User can login manually)

Alert 4: Payment Plan Completion Failed
Condition: subscription.completed nicht verarbeitet
Action: Email
Severity: HIGH (Revenue Risk - User wird nicht zu Monthly konvertiert)

Alert 5: Engagement Score Calculator Failed
Condition: Daily Cron nicht gelaufen
Action: Email
Severity: LOW (Upsells verzögert, aber nicht kritisch)
Daily Monitoring Dashboard
Metrics to Track (Google Sheets + Looker Studio):

1. Funnel Metrics:
   - Newsletter Signups
   - Trial Purchases
   - Trial → VE Conversion Rate
   - VE → ProGroup Conversion Rate
   - Churn Rate

2. Revenue Metrics:
   - MRR (Monthly Recurring Revenue)
   - ARR (Annual Run Rate)
   - Average Order Value
   - Lifetime Value (LTV)

3. Technical Metrics:
   - n8n Workflow Success Rate (Target: > 99%)
   - Brevo Email Deliverability (Target: > 95%)
   - Failed Payments (Target: < 10%)
   - Circle Uptime (Target: > 99,9%)

4. Engagement Metrics:
   - Average Engagement Score
   - Circle Daily Active Users
   - Email Open Rates
   - Email Click Rates

5. Support Metrics:
   - Manual Interventions (Target: < 5/Woche)
   - User-Reported Bugs (Track in Notion)
   - Response Time (Target: < 24 Std)

Anhang: Technische Spezifikationen
A. API Dokumentation
Brevo API
Base URL: https://api.brevo.com/v3
Authentication: API Key in Header
headers: {
'api-key': 'YOUR_BREVO_API_KEY'
}
Key Endpoints:
yamlCreate/Update Contact:
POST /contacts
Body:
email: string (required)
attributes: object
listIds: array
updateEnabled: boolean (true für update existing)

Get Contact:
GET /contacts/{email}
Response: Contact object mit allen Attributes

Update Contact:
PUT /contacts/{email}
Body:
attributes: object
listIds: array

Add to List:
POST /contacts/lists/{listId}/contacts/add
Body:
emails: array

Remove from List:
POST /contacts/lists/{listId}/contacts/remove
Body:
emails: array

Get Email Campaigns Stats:
GET /emailCampaigns/{campaignId}/statistics
Response: opens, clicks, delivered, etc.
ThriveCart Webhooks
Webhook Events:
yamlsubscription.charge.succeeded:
Trigger: Payment erfolgt (inkl. Installments)
Payload:
customer:
id: string
email: string
name: string
subscription:
id: string
product_id: string
status: string
billing_cycle: string
amount: number
installment:
current: number (null für ongoing)
total: number (null für ongoing)

subscription.charge.failed:
Trigger: Payment fehlgeschlagen
Payload: (ähnlich wie succeeded)

subscription.upgraded:
Trigger: User upgraded Subscription
Payload:
old_product_id: string
new_product_id: string
prorated_amount: number (automatisch berechnet)

subscription.cancelled:
Trigger: User cancelled oder Auto-Cancel
Payload: Basic subscription info

subscription.completed:
Trigger: Payment Plan abgeschlossen
Payload: Final installment info

refund.issued:
Trigger: Refund verarbeitet
Payload:
refund_amount: number
refund_reason: string
Circle API (via Zapier)
Base URL: https://app.circle.so/api/v1
Key Actions:
yamlFind Member:
GET /community_members?email={email}
Response: Member object or 404

Create Member:
POST /community_members
Body:
email: string
name: string
send_invite: boolean

Update Member Role:
PUT /community_members/{id}
Body:
space_group_ids: array (Roles sind Space Groups)

Grant Space Access:
POST /spaces/{space_id}/members
Body:
community_member_id: string

Get Member Activity:
GET /community_members/{id}/events
Response: Array of events (posts, comments, logins)

B. Environment Variables & Secrets
n8n Environment:
bash# Brevo
BREVO_API_KEY=xkeysib-xxx...

# ThriveCart

THRIVECART_WEBHOOK_SECRET=whsec_xxx...

# Zapier

ZAPIER_WEBHOOK_URL_CIRCLE_CREATE=https://hooks.zapier.com/xxx...
ZAPIER_WEBHOOK_URL_CIRCLE_UPDATE=https://hooks.zapier.com/xxx...

# Database (optional für Events Log)

DATABASE_URL=postgresql://user:pass@host:5432/db

# Alerting

ALERT_EMAIL=adrian@adriangoldner.com
ALERT_SMS_NUMBER=+49xxx... (optional)
ThriveCart Webhooks Config:
yamlWebhook URL: https://your-n8n.domain/webhook/thrivecart
Events: ALL (oder spezifisch auswählen)
Format: JSON
Secret: (auto-generiert, save in n8n ENV)
Retry: Enabled (3x with exponential backoff)

C. Data Retention & Privacy
GDPR Compliance
yamlUser Rights:

- Right to Access: Brevo Export Funktion
- Right to Deletion:
  - Brevo: Delete Contact (API oder UI)
  - Circle: Delete Member (manuell)
  - ThriveCart: Customer Data Deletion (manuell)
  - n8n: Purge Events Log für User

Data Retention:

- Brevo Contacts: Unbegrenzt (bis Deletion Request)
- n8n Events Log: 90 Tage, dann Auto-Purge
- ThriveCart Orders: Unbegrenzt (Finanzarchiv)
- Circle Posts: Unbegrenzt (bis User Deletion)

Consent Tracking:

- Newsletter Opt-in: Double Opt-In (Brevo)
- Marketing Emails: Unsubscribe Link (Brevo Auto)
- Cookie Consent: Webflow Integration

Privacy Policy:

- Updated when tooling changes
- Link in Footer + Signup Forms
- Disclose: Brevo, ThriveCart, Circle, Zapier, n8n

D. Backup & Disaster Recovery
Backup Strategy
yamlBrevo:
Frequency: Wöchentlich
Method: API Export → CSV → Google Drive
Includes: Contacts, Attributes, Lists
Restore Time: 2-4 Stunden (manuell)

n8n:
Frequency: Täglich
Method: Docker Volume Snapshot + GitHub für Workflows
Includes: Workflows, Credentials, Events Log
Restore Time: 30 Minuten (automatisch)

Circle:
Frequency: Monatlich
Method: Manueller Content Export (Circle bietet kein Auto-Backup)
Includes: Posts, Members, Spaces
Restore Time: N/A (Rebuild nötig)

ThriveCart:
Frequency: N/A
Method: ThriveCart backed up by vendor
Includes: Products, Orders, Customers
Restore Time: Contact ThriveCart Support
Disaster Recovery Plan
yamlScenario 1: n8n Server Crash

1. Restore Docker Container from Backup
2. Verify Webhooks erreichbar
3. Test kritische Workflows
   Expected Downtime: 30-60 Min

Scenario 2: Brevo Account suspended (Spam)

1. Contact Brevo Support
2. Während Downtime: Manuell Emails via Gmail
3. Export Contacts → Import in Backup Email Tool (z.B. Mailchimp)
   Expected Downtime: 4-24 Std

Scenario 3: ThriveCart Issues

1. ThriveCart ist SaaS - Vendor verantwortlich
2. Währenddessen: Manuell Payments via PayPal
3. Sync manuell nach Recovery
   Expected Downtime: Depends on ThriveCart

Scenario 4: Circle Downtime

1. Circle ist SaaS - Vendor verantwortlich
2. Während Downtime: Communication via Email
3. Keine Action nötig (Circle recovered automatisch)
   Expected Downtime: < 2 Std (Circle SLA)

E. Glossar & Begriffserklärung
yamlProrating:
Definition: Automatische Berechnung von anteiligen Kosten beim Subscription Upgrade/Downgrade
Beispiel: User zahlt 47€/M, upgradet nach 15 Tagen. Credit = (15/30) × 47€ = 23,50€

Split-Pay / Payment Plan:
Definition: Zahlung in Raten (z.B. 4x 97€ statt 347€ einmalig)
ThriveCart: "Subscription (Limited Rebills)"

Installment:
Definition: Einzelne Rate in einem Payment Plan
ThriveCart Webhook: "installment.current" / "installment.total"

Subscription (Ongoing):
Definition: Wiederkehrende Zahlung ohne End-Datum (z.B. 47€/M)
Läuft bis: User cancelt oder Payment fails

Subscription (Limited):
Definition: Wiederkehrende Zahlung mit fixem End-Datum (z.B. 12x 47€)
Läuft bis: Alle Rebills durchgelaufen

Dunning:
Definition: Prozess zur Wiederherstellung fehlgeschlagener Zahlungen
ThriveCart: "Subscription Saver" Feature

Rollover Credit:
Definition: Anrechnung bereits bezahlter Beträge beim Upgrade
Beispiel: ProGroup 3 Monate à 85€ = 255€ → Credit beim Coaching-Upgrade

Grace Period:
Definition: Zeitraum nach Failed Payment, in dem Zugang noch aktiv bleibt
Dauer: 7 Tage (Standard)

Churn:
Definition: Anteil der Kunden, die kündigen
Berechnung: (Cancellations / Active Subscriptions) × 100
Target: < 10% pro Monat

MRR (Monthly Recurring Revenue):
Definition: Vorhersagbarer monatlicher Umsatz aus Subscriptions
Berechnung: Sum(alle aktiven Monthly Subscriptions)

LTV (Lifetime Value):
Definition: Durchschnittlicher Gesamtumsatz pro Kunde
Berechnung: MRR × (1 / Churn Rate)
Beispiel: 47€ MRR / 10% Churn = 470€ LTV

Engagement Score:
Definition: Metrisches Rating der User-Aktivität (0-100)
Nutzung: Upsell-Trigger, Churn-Prevention

🎯 Zusammenfassung für KI-Team
Was ist fertig?
✅ Komplettes Datenmodell (23 Brevo Attributes)
✅ Business Model (5 Core Products + Upsells/Downsells)
✅ Tool-Setup Guides (ThriveCart, Brevo, Circle, n8n, Zapier)
✅ Customer Journeys (4 Haupt-Flows dokumentiert)
✅ Automation Workflows (8 kritische n8n Workflows spezifiziert)
✅ Implementation Roadmap (3 Phasen, 12 Wochen)
✅ Testing Plan (Unit, Integration, UAT, Performance)
✅ Technical Specs (APIs, Webhooks, Environment)
Nächste Schritte

Phase 1 starten (Woche 1-4)
n8n Workflows bauen nach Spezifikation
Brevo Sequences erstellen nach Template
End-to-End Testing vor Launch

Key Decisions bereits getroffen
✓ ThriveCart Pro+ (Prorating automatisch)
✓ Brevo als Source of Truth (keine separate DB)
✓ Zapier für Circle Integration (günstiger als Circle höherer Plan)
✓ Grace Period 7 Tage bei Failed Payment
✓ Payment Plans: VE 4x97€, ProGroup 3x247€ (Start)

Ende des Master-Dokuments
Version: 1.0 | Letzte Aktualisierung: 03. Oktober 2025
