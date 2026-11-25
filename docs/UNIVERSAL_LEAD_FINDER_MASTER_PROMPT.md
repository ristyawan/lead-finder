# UNIVERSAL LEAD FINDER — MASTER DEVELOPMENT PROMPT

**Multi-Source Lead Discovery, Contact Intelligence & Integrated CRM SaaS Platform**

---

## 1. PROJECT OVERVIEW

Build a complete, professional, scalable SaaS web application named **Universal Lead Finder**.

**Universal Lead Finder** is an all-in-one lead generation, prospect discovery, contact intelligence, data enrichment, and CRM management platform. It enables businesses, sales teams, marketers, agencies, and entrepreneurs to discover potential customers across multiple connected online sources from a single unified workspace.

Users can search by keyword, industry, business category, location, company name, job title, or target audience. Example queries:
- Villa Owners in Bali
- Hotel Managers in Indonesia
- Restaurant Owners in Jakarta
- Real Estate Developers in Bali
- Solar Energy Companies
- Marketing Directors in Singapore
- Property Management Companies
- Business Owners in Australia
- Construction Companies in Indonesia

The system retrieves publicly available and authorized business/professional information, normalizes and deduplicates records, enriches contact details via connected enrichment providers, calculates lead scores, and allows users to save and manage qualified prospects in an integrated CRM.

**Core Product Principle:**
> One application. Multiple data sources. One unified lead database. One integrated CRM.

This must be built as a real, production-ready SaaS architecture—not a static dashboard or clickable mockup.

---

## 2. CORE PRODUCT CAPABILITIES

1. **Multi-Criteria Prospect Search:** Search potential customers using keywords, roles, industries, and locations.
2. **Independent Multi-Provider Management:** Connect, configure, test, and manage search engines, social platforms, business directories, and enrichment services independently.
3. **Selective Multi-Source Execution:** Select one, several, or all connected sources per search job and execute them concurrently.
4. **Unified Result Normalization:** Merge results from heterogeneous providers into a single standardized lead schema while preserving source attribution.
5. **Contact Enrichment & Email Verification:** Enrich discovered leads and verify business emails through authorized, user-configured providers.
6. **Confidence-Based Deduplication:** Detect and merge duplicate leads across sources without losing source history or verification metadata.
7. **Configurable Lead Scoring:** Score and prioritize prospects based on weighted relevance and contact completeness criteria.
8. **Integrated CRM & Pipeline:** Manage saved leads, companies, Kanban/Table deal pipelines, follow-ups, notes, tasks, and communication logs.
9. **Analytics & Attribution:** Track search jobs, provider performance, conversion funnels, and API usage from real database records.
10. **Multi-Tenant Workspace & SaaS Governance:** Support workspaces, role-based access control (RBAC), theme/language preferences, security policies, and subscription limits.

---

## 3. UI/UX DESIGN & DESIGN SYSTEM

Create a clean, modern, high-density B2B SaaS interface inspired by the usability and information hierarchy of **Attio, HubSpot, Linear, and Pipedrive** (without copying their branding or layouts directly).

### Design Guidelines
- Minimal, structured, business-grade visual hierarchy with comfortable spacing and crisp typography.
- Fully responsive across **desktop, tablet, and mobile**.
- Avoid excessive gradients, neon colors, sci-fi decorations, unnecessary card clutter, or generic AI-dashboard aesthetics.
- Favor structured data tables, slide-over detail drawers, compact filter bars, tabs, and clear status badges.
- Every visible interactive control must perform a real action.

### Color System
- **Primary:** `#3568E8`
- **Dark:** `#111827`
- **Secondary Dark:** `#1F2937`
- **Light Background:** `#F4F6FA`
- **White / Surface:** `#FFFFFF`
- **Primary Text:** `#172033`
- **Secondary Text:** `#64748B`
- **Success:** `#16A36A`
- **Warning:** `#E6A23C`
- **Danger:** `#DC5252`
- **Border:** `#E5E7EB`

### Theme & Localization
- **Themes:** Light Mode, Dark Mode, System Theme.
- **Languages:** **Bahasa Indonesia** and **English** (full UI localization across navigation, forms, buttons, validation messages, notifications, and system labels; do not auto-translate user-generated lead data).

---

## 4. APPLICATION NAVIGATION & SHELL

Implement a collapsible/expandable persistent sidebar with 12 functional modules:
1. **Dashboard**
2. **Lead Finder**
3. **My Leads**
4. **Contact Intelligence**
5. **Companies**
6. **CRM Pipeline**
7. **Follow Up**
8. **Email Center**
9. **WhatsApp Center**
10. **Analytics**
11. **Integrations**
12. **Settings**

**Top Header Bar:**
- Workspace switcher
- Global search
- Notification center
- Theme selector
- Language selector
- User profile menu

Every navigation item must route to a real, functional page.

---

## 5. DASHBOARD

Display real-time, database-backed business metrics and visualizations:

- **KPI Metrics:** Total Leads, New Leads, Qualified Leads, Interested Leads, Follow Up Required, Contacted Leads, Meetings Scheduled, Converted Leads, Conversion Rate, Total Companies, Search Jobs, Leads Discovered This Month.
- **Charts:** Lead acquisition over time, Pipeline distribution, Leads by industry, Leads by country/location, Leads by source provider, Conversion performance.
- **Operational Panels:** Recent Leads, Recent Search Activity, Upcoming Follow-Ups, Recent CRM Activities, Top Performing Sources, Source Connection Alerts.

**Data Integrity Rule:** Never display fabricated metrics in production mode. If sample data is shown in Demo Mode, clearly label the workspace/banner as **DEMO DATA**.

---

## 6. LEAD FINDER — MULTI-SOURCE SEARCH ENGINE

### Search Inputs
- Keywords, Business Name, Industry, Business Category, Job Title / Role, Target Audience, Company Type, Location, Country, City, Website Domain.

### Filters & Saved Searches
- **Filters:** Country, City, Industry, Business Category, Company Size, Job Title, Business Type, Website Available, Business Email Available, Business Phone Available, LinkedIn Available, Instagram Available, Facebook Available, Contact Verification Status, Lead Score Range, Source Provider.
- **Search Controls:** Select single source, select multiple sources, Select All Connected, Deselect All, Save Search Configuration, Run Search, Stop Running Search, View Search History, Re-run Previous Search.

**Execution Rule:** Only providers that are both `CONNECTED` and explicitly selected by the user may be queried in a search job.

---

## 7. MULTI-SOURCE PROVIDER ARCHITECTURE

Categorize providers by their actual technical function and enforce strict capability boundaries:

1. **Search Engines** (e.g., authorized Web Search APIs)
   - *Capabilities:* Public website discovery, business/professional page indexing, source URLs, public snippets.
   - *Limitation:* Do not inherently provide verified emails or private phone numbers.
2. **Professional Networks** (e.g., official/authorized B2B professional APIs)
   - *Capabilities:* Public/authorized professional profile lookup, job titles, company associations, profile URLs.
3. **Social Media Platforms** (e.g., Instagram, Facebook, TikTok, YouTube, X via official APIs)
   - *Capabilities:* Authorized public business/creator page info, public website links, explicitly listed business contacts within official API permissions.
4. **Business Discovery & Directories** (e.g., authorized Maps/Business Profile APIs, licensed business directories)
   - *Capabilities:* Business name, category, address, coordinates/location, website, public business phone/email, listing URL.
5. **Contact Enrichment & Verification Providers** (authorized B2B contact intelligence and email verification APIs)
   - *Capabilities:* Company enrichment, professional contact enrichment, business email discovery, email verification, domain-to-company matching.
   - *Rule:* Do not list enrichment-only providers as discovery search sources unless their API genuinely supports prospect search.

### Declared Provider Capabilities
Each provider adapter must explicitly declare its supported capability flags:
`SEARCH` | `PROFILE_LOOKUP` | `COMPANY_LOOKUP` | `BUSINESS_DISCOVERY` | `CONTACT_ENRICHMENT` | `EMAIL_DISCOVERY` | `EMAIL_VERIFICATION` | `PHONE_DISCOVERY` | `SOCIAL_PROFILE_LOOKUP`

Never advertise or execute a capability that a provider's API does not support.

---

## 8. PROVIDER CONNECTION MANAGEMENT

Manage each provider independently inside **Integrations** and the **Lead Finder** source selector:

- **Displayed Metadata:** Logo & Name, Category, Connection Status, Supported Capabilities, Last Connection Test, Last Successful Search, API Usage & Quota Limits.
- **Connection States:** `CONNECTED`, `NOT_CONNECTED`, `CONNECTION_ERROR`, `EXPIRED`, `CONFIGURATION_REQUIRED`, `DISABLED`.
- **Actions:** Connect, Disconnect, Reconnect, Test Connection, Configure, View Details, Select/Deselect for Search.
- **Connection Workflow:**
  1. Support official OAuth flows where applicable, or secure credential forms (`API Key`, `Client ID`, `Client Secret`, `Redirect URI`, `Account/Workspace ID`, `Scopes`).
  2. Validate credentials server-side via Edge Functions and run a live connection test.
  3. Store secrets encrypted on the server—never expose secrets in frontend bundles, browser storage, logs, or API responses.
  4. Mark `CONNECTED` only after real validation succeeds.

---

## 9. MULTI-SOURCE SEARCH ORCHESTRATION

### Execution Pipeline
1. Validate user input, workspace permissions, and usage limits.
2. Verify selected providers are `CONNECTED` and support `SEARCH` / `BUSINESS_DISCOVERY`.
3. Create a `search_jobs` record and per-provider `search_job_providers` records.
4. Execute selected providers concurrently via asynchronous backend workers/Edge Functions (avoiding single-request timeouts).
5. Stream or poll real-time per-provider status (`Queued`, `Searching`, `Completed`, `Failed`, `Not Connected`, `Cancelled`).
6. Normalize raw payloads into a unified `NormalizedLead` schema with full source attribution.
7. Run deduplication, optional auto-enrichment (if enabled & configured), and lead scoring.
8. Persist results and update job metrics.

### Fault Tolerance
- **Partial Availability:** If a selected source is disconnected or unsupported, skip it with a clear status message without blocking active sources.
- **Isolated Provider Failure:** If one provider times out or errors, capture the specific error, allow retrying that provider, and preserve all successful results from other providers.
- **Honest Progress:** Display actual provider counts, unique leads, enriched count, and elapsed duration—never fake progress bars.

---

## 10. UNIFIED RESULTS, DEDUPLICATION & SCORING

### Unified Lead Table
Display normalized fields: Name, Job Title, Company Name, Industry, Location, Country, Business Email, Email Verification Status, Business Phone, Website, Social URLs (LinkedIn, Instagram, Facebook, Others), Lead Score, Source Providers, Discovery Date, Contact Availability.
- Display `Not Available` for missing fields—never fabricate values.
- **Row & Bulk Actions:** View Details, Save Lead, Add to CRM, Enrich Contact, Verify Email, Add Note, Assign Owner, Schedule Follow-Up, Export, Mark Qualified / Not Relevant, Delete (enabled only when required data & provider capabilities exist).

### Intelligent Deduplication
- Match potential duplicates using **Email Address, Business Phone, Website Domain, LinkedIn Profile URL, Company Name, and Name + Company**.
- Assign match confidence scores; auto-merge only high-confidence deterministic matches and flag uncertain matches for user review.
- When merging, preserve all `lead_source_records`, discovery timestamps, verification logs, notes, and CRM history with a full audit trail.

### Configurable Lead Scoring (0–100)
- Weighted factors: Industry Match, Location Match, Job Title Match, Company Relevance, Website Availability, Business Email Availability, Email Verification Status, Business Phone Availability, Social Profile Presence, and custom workspace rules.
- Tiers: **80–100** (High Potential), **60–79** (Good Potential), **40–59** (Moderate Potential), **0–39** (Low Potential).
- Display a transparent breakdown explaining why the score was assigned.

---

## 11. CRM, INTELLIGENCE & COMMUNICATION MODULES

1. **Contact Intelligence:** Full lead profile view with contact/company details, source attribution history, field-level enrichment provenance, verification history, notes, and CRM timeline.
2. **My Leads:** Centralized database of saved prospects with search, multi-facet filters, sorting, pagination, custom tags, saved views, ownership assignment, CSV/Excel import/export, and status management (`New`, `Qualified`, `Interested`, `Contacted`, `Follow Up`, `Appointment`, `Proposal`, `Won`, `Lost`, `Not Relevant`).
3. **Companies:** Automatically group contacts under deduplicated company records showing industry, website, location, contact count, owner, notes, and opportunities.
4. **CRM Pipeline:** Visual drag-and-drop **Kanban** and **Table** views (`NEW LEAD` → `CONTACTED` → `INTERESTED` → `FOLLOW UP` → `APPOINTMENT` → `PROPOSAL` → `NEGOTIATION` → `WON` / `LOST`), logging every stage transition and expected deal value.
5. **Follow-Up Management:** Task scheduler (`Phone Call`, `WhatsApp`, `Email`, `Meeting`, `Site Visit`, `General Task`) categorized by Today, Upcoming, Overdue, and Completed with in-app reminders.
6. **Email Center:** Connect Gmail, Outlook, or SMTP accounts via OAuth/encrypted credentials; compose with templates, associate emails with leads/companies, and log verified delivery status (never fabricate open/click events).
7. **WhatsApp Center:** Integrate strictly via the **official WhatsApp Business Platform** or authorized BSP APIs; support approved message templates, opt-in compliance, conversation logging, and delivery error reporting (no unofficial WhatsApp Web scraping/automation).
8. **Analytics & Source Performance:** Compare providers by searches run, raw vs. unique leads, duplicate rate, enriched contacts, verified emails, failure rate, average latency, and API usage cost, with CSV/Excel export.

---

## 12. API-READY ADAPTER & DATABASE ARCHITECTURE

### Provider Adapter Interface
Implement a modular provider registry under `src/services/providers/` (separate from React context providers in `src/app/providers/`):

```ts
export interface LeadProvider {
  id: string;
  name: string;
  category: ProviderCategory;
  capabilities: ProviderCapability[];

  getProviderInfo(): Promise<ProviderInfo>;
  isConfigured(workspaceId: string): Promise<boolean>;
  getConnectionStatus(workspaceId: string): Promise<ConnectionStatus>;
  connect(workspaceId: string, payload: ConnectionPayload): Promise<ConnectionResult>;
  disconnect(workspaceId: string): Promise<ConnectionResult>;
  testConnection(workspaceId: string): Promise<ConnectionTestResult>;
  search(params: LeadSearchParams): Promise<ProviderSearchResult>;
  normalizeResults(rawResults: unknown[]): Promise<NormalizedLead[]>;
  getUsage(workspaceId: string): Promise<ProviderUsage>;
  handleError(error: unknown): ProviderError;
}
```

### Database Schema (Supabase PostgreSQL)
Inspect existing migrations first before creating tables. Implement normalized schemas with proper indexes, foreign keys, and Row Level Security (RLS):
- **Auth & Workspace:** profiles, workspaces, workspace_members, workspace_invitations, roles, permissions
- **Leads & Companies:** leads, companies, lead_companies, lead_tags, lead_notes, lead_activities, lead_owners, lead_status_history
- **Search & Providers:** search_providers, provider_connections, provider_credentials_metadata, user_search_preferences, workspace_search_preferences, search_jobs, search_job_providers, search_job_results, lead_source_records, provider_usage_logs
- **Enrichment & Verification:** enrichment_jobs, enrichment_records, email_verification_records, contact_field_sources
- **CRM & Comms:** crm_pipelines, crm_stages, crm_opportunities, follow_up_tasks, communication_logs, email_accounts, email_templates, email_logs, whatsapp_connections, whatsapp_templates, whatsapp_logs
- **System & Billing:** notifications, audit_logs, subscription_plans, subscriptions, usage_records, application_settings

---

## 13. SECURITY, COMPLIANCE, AI & SUBSCRIPTIONS

- **Security & Compliance:** Enforce Supabase Auth, strict workspace-scoped RLS, RBAC, server-side secret encryption, input sanitization, rate limiting, and audit logs. Collect only public, licensed, or authorized data—never bypass CAPTCHAs, authentication walls, or platform Terms of Service.
- **AI Assistant (Optional, Server-Side):** Support query expansion, lead/company summaries, score explanations, duplicate review hints, and follow-up/email drafting via server-side LLM calls. Label all AI outputs clearly as AI-Generated Suggestions and never allow AI to invent contact details or verification statuses.
- **Subscriptions & Usage Limits:** Support tiered plans (Free, Starter, Professional, Business, Enterprise) with centralized quota enforcement, separating platform subscription quotas from external provider API usage. Never simulate successful payments without a real payment gateway integration.
- **Demo Mode vs. Live Mode:** Allow testing the UI without external API keys using clearly isolated and badged DEMO DATA, with a seamless switch to Live Mode once real providers are connected.

---

## 14. TECH STACK & FOLDER STRUCTURE

- **Frontend:** React, TypeScript, Vite, Tailwind CSS, shadcn/ui, Lucide Icons
- **Backend & Infra:** Supabase (Auth, PostgreSQL, Storage, Edge Functions), deployed via GitHub & Vercel

```text
src/
  app/
    routes/
    providers/          # React Context Providers (Theme, Auth, Workspace, i18n)
    layouts/
  components/
    ui/
    navigation/
    dashboard/
    lead-finder/
    lead-results/
    provider-connections/
    crm/
    analytics/
    settings/
  features/
    authentication/
    workspaces/
    lead-search/
    leads/
    companies/
    enrichment/
    crm/
    follow-ups/
    email/
    whatsapp/
    integrations/
    subscriptions/
  services/
    api/
    providers/          # External Lead/Enrichment Provider Adapters & Registry
    search-orchestration/
    deduplication/
    scoring/
    notifications/
  hooks/
  i18n/
  types/
  utils/
  styles/

supabase/
  migrations/
  functions/
    lead-search/
    provider-connect/
    provider-test/
    provider-disconnect/
    contact-enrichment/
    email-verification/
    lead-scoring/
```

---

## 15. PHASED EXECUTION & ENGINEERING RULES

Before modifying any codebase, inspect existing files, routes, components, and database migrations to preserve working functionality and avoid duplicate structures. Build sequentially in 7 disciplined phases:

- **Phase 1 — Foundation:** Project setup, Auth, Workspace & RBAC, DB schema + RLS, App shell & navigation, Design tokens, Theme & ID/EN localization.
- **Phase 2 — Core Lead Finder:** Search UI, filters, saved searches, Provider Registry, Connection Manager, async Search Job orchestration, Search History.
- **Phase 3 — Multi-Source Adapters:** Implement adapters for available Search Engines, Business Directories, Professional/Social APIs, and Enrichment providers with real connection tests and usage logs.
- **Phase 4 — Lead Intelligence:** Normalization, confidence-based deduplication, enrichment/verification workflows, configurable lead scoring, Contact Intelligence profile view.
- **Phase 5 — CRM Suite:** My Leads, Companies, Kanban/Table CRM Pipeline, Follow-Ups, Notes, Activity History.
- **Phase 6 — Communications & Analytics:** Email Center, official WhatsApp Business Center, Notification Center, Analytics & Source Performance exports.
- **Phase 7 — Hardening & Launch:** Subscription quota enforcement, security & RLS audit, responsive QA (desktop/tablet/mobile), documentation, production deployment.

---

## Ringkasan Perubahan

1. **Menghapus Apollo.io & Hunter.io:** Semua penyebutan spesifik kedua layanan tersebut diganti dengan konsep generik *Authorized Contact Enrichment & Email Verification Providers* agar arsitektur bebas terikat vendor tertentu.
2. **Memadatkan dari 35 bagian menjadi 15 bagian terstruktur:** Menghilangkan pengulangan aturan (seperti larangan data palsu dan aturan keamanan yang tadinya tersebar di 5–6 bagian terpisah) tanpa mengurangi satu pun detail teknis maupun spesifikasi fitur.
3. **Memperjelas teknis implementasi:** Menambahkan pemisahan tegas antara `src/app/providers/` (React Context) dan `src/services/providers/` (Adapter API eksternal), serta memperjelas eksekusi *async job* di Edge Functions agar tidak mudah *timeout*.
