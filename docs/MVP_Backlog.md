# Cortex OS MVP Backlog (User Stories)

Scope: MVP only. Target: 2,000 users, OpenRouter, web + bot, no on-prem models, no multi-tenant. PWA/offline is part of full version, not MVP.

## Legend
- Priority: P0 (must), P1 (should), P2 (could)
- Effort: S, M, L (relative)

---

## Sprint plan (3 sprints)

**Sprint 1: Foundations and safety (P0 focus)**  
Stories: A1, A3, A5, B4, B5, C1, C5, K1, K2, K4, L1, L2, L3.

**Sprint 2: Core data sources and dashboards**  
Stories: B1, B2, B3, C2, H1, H2, K3.

**Sprint 3: Product value features and pilot readiness**  
Stories: D1, D2, D3, E1, E2, F1, F2, F3, G1, H3, I1, I2, J1, J2, A2, A4, A6, C3, C4.

---

## Epic A: Consent, Privacy, and Safety

**A1. Consent flow** (P0, M)
- As a user, I can read and accept participation terms before any data is collected.
- Acceptance criteria:
  - Consent screen shown on first launch.
  - User cannot proceed without consent.
  - Consent timestamp stored.

**A2. Pause participation** (P1, S)
- As a user, I can pause and resume participation.
- Acceptance criteria:
  - Pause stops data processing and recommendations.
  - Resume restores scheduled flows.

**A3. Privacy Firewall** (P0, M)
- As the system, I mask PII before sending data to LLM.
- Acceptance criteria:
  - Mask names, phones, emails, contract/card numbers.
  - Masked payload is logged in audit trace.

**A4. Data retention** (P1, M)
- As admin, I can set retention for raw events and aggregates.
- Acceptance criteria:
  - Defaults: raw 90 days, aggregates 12 months.
  - Data can be deleted on user request within 30 days.

**A5. No diagnosis protocol** (P0, S)
- As the system, I do not output medical diagnoses.
- Acceptance criteria:
  - Language avoids medical terms like depression/anxiety diagnosis.
  - Safety disclaimer is visible in bot help.

**A6. SOS help** (P1, S)
- As a user, I can call for help and get support contacts.
- Acceptance criteria:
  - SOS command returns local support contacts and crisis guidance.

---

## Epic B: Integrations and Data Layer

**B1. Jira integration** (P0, L)
- As admin, I can connect Jira and ingest task events.
- Acceptance criteria:
  - Status changes and timestamps ingested.
  - Tasks mapped to user and team.

**B2. Outlook calendar integration** (P0, L)
- As admin, I can connect Outlook to ingest meetings.
- Acceptance criteria:
  - Meeting start/end and attendees ingested.
  - Double bookings detected.

**B3. Chat integration (Teams or Telegram)** (P0, L)
- As admin, I can connect selected chat channel.
- Acceptance criteria:
  - Messages and metadata ingested for work channels.
  - Personal chats are excluded.

**B4. Data normalization pipeline** (P0, M)
- As the system, I normalize all events into a common schema.
- Acceptance criteria:
  - Tasks, meetings, and messages have consistent user IDs.
  - Events are time-bucketed for aggregates.

**B5. Scheduler and retry** (P0, M)
- As the system, I sync data on schedule and retry on failure.
- Acceptance criteria:
  - Daily sync for all sources.
  - Failed jobs are retried and logged.

---

## Epic C: Bot Core and User Flows

**C1. Bot onboarding** (P0, M)
- As a user, I can start the bot and set timezone and working hours.
- Acceptance criteria:
  - User sets timezone and work hours.
  - Intro explains privacy boundaries.

**C2. Weekly PERMA micro survey** (P0, S)
- As a user, I receive a weekly 2-question PERMA check-in.
- Acceptance criteria:
  - Survey appears on schedule.
  - Answers stored and shown in personal dashboard.

**C3. Gratitude prompt** (P1, S)
- As a user, I receive a daily gratitude question.
- Acceptance criteria:
  - Prompt can be turned off in settings.

**C4. MCTQ chronotype survey** (P1, M)
- As a user, I can complete MCTQ to define chronotype.
- Acceptance criteria:
  - Results stored and used for golden hours.

**C5. Quiet delivery** (P0, S)
- As a user, I do not receive messages outside work hours.
- Acceptance criteria:
  - Bot delays notifications beyond configured hours.

---

## Epic D: Flow Engine (Base)

**D1. Boredom trigger** (P1, M)
- As the system, I detect boredom from fast task closures and context switching.
- Acceptance criteria:
  - Trigger thresholds are configurable.
  - When triggered, user gets sprint challenge.

**D2. Anxiety trigger** (P1, M)
- As the system, I detect anxiety from stalled tasks.
- Acceptance criteria:
  - Trigger thresholds are configurable.
  - When triggered, user gets mentor prompt.

**D3. Interventions opt-in** (P1, S)
- As a user, I can accept or skip an intervention.
- Acceptance criteria:
  - Skip does not penalize user.

---

## Epic E: Context Co-pilot (RAG)

**E1. Knowledge base indexing** (P0, L)
- As admin, I can connect a document source and index it.
- Acceptance criteria:
  - Indexing status is visible.
  - Partial failures are shown in admin.

**E2. RAG response format** (P0, M)
- As a user, I get a short step-by-step answer.
- Acceptance criteria:
  - Answer format: 1-2-3 steps + source link.

---

## Epic F: Calendar Guard

**F1. Recovery buffer** (P0, M)
- As the system, I add buffers after meetings.
- Acceptance criteria:
  - Buffer duration is configurable.
  - Users can see buffer entries.

**F2. Deep work day** (P1, M)
- As admin, I can set one no-meeting day.
- Acceptance criteria:
  - Invites on that day are declined with a message.

**F3. Meeting cost calculator** (P1, M)
- As a meeting owner, I can see meeting cost.
- Acceptance criteria:
  - Cost shown at scheduling time.
  - Cost uses configured salary ranges.

---

## Epic G: Kind Communication

**G1. Pre-flight check** (P1, M)
- As a user, I get a warning if my message is aggressive.
- Acceptance criteria:
  - Warning shown before sending.
  - Alternative rewrite is suggested.

---

## Epic H: Dashboards

**H1. Employee dashboard** (P0, M)
- As a user, I can see my weekly trend.
- Acceptance criteria:
  - PERMA trend chart visible.
  - Data updates weekly.

**H2. Team heatmap** (P0, M)
- As a manager, I see aggregated team metrics.
- Acceptance criteria:
  - Aggregates shown only for teams >=5.

**H3. HR dashboard** (P1, M)
- As HR, I see department trends.
- Acceptance criteria:
  - Trends by department and time.

---

## Epic I: People Analytics (Base)

**I1. Risk labels** (P1, M)
- As a manager, I see low/medium/high risk for my team.
- Acceptance criteria:
  - Labels are computed weekly.
  - No individual risk scores shown.

**I2. ROI calculator** (P1, M)
- As HR, I see estimated time savings from meetings.
- Acceptance criteria:
  - Savings computed from reduced meeting time.

---

## Epic J: Gamification

**J1. Cortex Coins** (P1, M)
- As a user, I earn coins for participation.
- Acceptance criteria:
  - Coins are granted on configured actions.
  - Ledger is visible to user.

**J2. Rewards catalog** (P1, M)
- As admin, I can add or remove rewards.
- Acceptance criteria:
  - Rewards have name, cost, availability.

---

## Epic K: Admin Panel and Configuration

**K1. Integration management** (P0, M)
- As admin, I can connect and disconnect sources.
- Acceptance criteria:
  - Connection status visible.
  - Errors are shown.

**K2. Module toggles** (P0, S)
- As admin, I can enable or disable modules.
- Acceptance criteria:
  - Changes apply without restart.

**K3. Threshold configuration** (P0, M)
- As admin, I can edit trigger thresholds.
- Acceptance criteria:
  - All triggers have defaults and overrides.

**K4. RBAC and audit** (P0, M)
- As admin, I can manage roles and see audit logs.
- Acceptance criteria:
  - Role permissions enforced.
  - Audit includes who/what/when.

---

## Epic L: Non-functional Requirements

**L1. Performance** (P0, M)
- As a user, I receive responses within SLA.
- Acceptance criteria:
  - Simple responses < 3s, LLM/RAG < 10s.

**L2. Security** (P0, M)
- As admin, I can confirm encryption in transit and at rest.
- Acceptance criteria:
  - TLS enabled.
  - Data at rest encrypted.

**L3. Monitoring** (P0, S)
- As ops, I can monitor integration health.
- Acceptance criteria:
  - Error rates and sync status are visible.

---

## Definition of Done (MVP)

- All P0 stories complete and accepted.
- P1 stories implemented for pilot scope.
- Privacy and aggregation rules enforced.
- Documentation for admin and user flows delivered.
