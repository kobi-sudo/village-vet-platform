# Village Vet — AI Revenue Growth Platform

A single-file, browser-based intelligence platform for independent veterinary surgeries. Built for reception, clinical, and management teams — no installation required.

---

## Quick Start

1. Open `index.html` in any modern browser (Chrome recommended)
2. Log in with the default credentials below
3. Click **"Load demo data"** on the Dashboard or Import page to explore with sample data
4. Add your Claude API key (from [console.anthropic.com](https://console.anthropic.com)) to enable AI features

**Default credentials**
- PIN: `241085`
- Password: `VillageVet2026!`

> Change these in the `<script>` block at the top of `index.html` before deployment.

---

## What's Inside

### 8 Core Modules

| Module | Tab | Purpose |
|--------|-----|---------|
| A. Executive Dashboard | Dashboard | Revenue KPIs, charts, service mix, outstanding invoices |
| B. Revenue Growth Engine | Growth | Lapsed client detection, reactivation scoring, outreach scripts |
| C. Health Plans | Health Plans | Plan tiers, revenue calculator, patient eligibility |
| D. Pricing Intelligence | Pricing | UK benchmark comparison, underpriced service flags |
| E. Clinical Assistant | Clinical | AI-assisted differential diagnosis, consultation notes |
| F. Campaign Builder | Campaigns | Ready-to-use SMS, email, social, and reception scripts |
| G. Staff Prompts | Staff Prompts | Per-patient action prompts for front desk teams |
| H. KPI Forecasting | Forecast | 12-month revenue uplift in 3 scenarios |

---

## Module Detail

### A — Executive Dashboard
- Revenue by period (day / week / month / year / import)
- Service mix donut chart
- Revenue by vet (bar chart)
- Average invoice value trend
- Outstanding balance tracking
- Top 10 services by revenue or volume
- Payment status breakdown
- Configurable alert thresholds

### B — Revenue Growth Engine
**30 demo patients** pre-loaded, each scored on:
- Vaccination overdue
- Estimate pending (not converted)
- Post-op review not booked
- Chronic care recheck overdue
- Senior wellness due (7yr+ dogs, 8yr+ cats)
- Dental check overdue
- Parasite prevention lapsed
- Neutering not performed
- General lapsed (12m+ inactive)

Each opportunity shows: priority badge (High / Medium / Low), estimated revenue, reason tags, and one-click outreach script generation.

**Outreach scripts** available in 4 formats per patient:
- SMS (under 160 chars)
- Email (with subject line)
- Phone call script
- Reception desk prompt

With Claude API key: AI-improved personalised versions generated on demand.

**Export**: All opportunities exportable as CSV for mail-merge or CRM use.

### C — Health Plans
- Dog and cat plan tiers (Bronze / Silver / Gold / Puppy)
- Interactive revenue calculator (adjust member counts to forecast MRR)
- Eligible non-member list with suggested tier
- Current member list with MRR breakdown

**Plan pricing (defaults)**

| Tier | Dogs | Cats |
|------|------|------|
| Bronze | £22/mo | £18/mo |
| Silver | £32/mo | £26/mo |
| Gold | £45/mo | £38/mo |
| Puppy | £28/mo | — |

### D — Pricing Intelligence
Compares your fee schedule to published BVA/RCVS UK benchmarks across:
- Consultations
- Surgery
- Diagnostics
- Dentistry & Specialist

Services flagged >10% below benchmark are highlighted as revenue opportunities.

### E — Clinical Assistant
- AI-assisted differential diagnosis
- Structured SOAP consultation note generation (ready to paste into Merlin)
- Diagnostic result slots: IDEXX bloods, Signal Pet x-ray, Zoetis cytology, HT Vista
- PDF extraction and image analysis (requires Claude API key)
- Voice recording (Chrome)
- Case history with restore and copy-to-Merlin

### F — Campaign Builder
6 pre-built campaign templates with ready copy:
1. Spring Dental Awareness Month
2. Senior Pet Wellness Screening
3. Spring Parasite Prevention Drive
4. Health Plan Enrolment Campaign
5. Lapsed Client Reactivation
6. Estimate Follow-Up

Each campaign includes SMS, email, social post, and reception script. AI-enhanced versions available with Claude API key.

**Recommended campaign calendar:**
- April: Dental awareness
- May: Parasite prevention
- June: Senior wellness screening
- Quarterly: Lapsed client reactivation

### G — Staff Prompts
- Search any patient by name, owner surname, or breed
- Instant per-patient action prompt card showing all overdue items
- Priority-coded prompts: urgent (red), action (green), info (blue), amber warning
- Today's priority contact list for morning briefings
- Practice morning briefing summary

### H — KPI Forecast
Three revenue scenarios (Conservative / Base / Optimistic):
- 12-month uplift bar chart
- Health plan MRR growth projection
- Revenue by initiative (reactivation, plans, campaigns, upsell)
- Initiative ROI table

---

## Data Import

Upload CSV exports from any of these platforms:

| Platform | What it adds |
|----------|-------------|
| Merlin PMS | Invoice records, services, vets, clients |
| GoCardless | Direct debit data, failure rates |
| Google Ads | Campaign spend, CPC, impressions |
| PetsApp | Client messaging data |
| IDEXX VetConnect | Lab results |
| Signal Pet | Imaging data |
| Zoetis | Cytology results |
| HT Vista | Histopathology results |

The import engine auto-maps column headers from Merlin exports. Supported date formats: UK (DD/MM/YYYY), ISO (YYYY-MM-DD), US (MM/DD/YYYY), and named month formats.

---

## AI Features (Claude API)

All AI features require a Claude API key from [console.anthropic.com](https://console.anthropic.com).

Enter your key in the **AI Reports** tab. It is saved to browser localStorage — never sent to any server other than Anthropic's API directly.

| Feature | API Required |
|---------|-------------|
| AI practice Q&A chat | Yes |
| Outreach script AI improvement | Yes |
| Campaign copy AI generation | Yes |
| Clinical differential diagnosis | Yes |
| Consultation note (SOAP / history) | Yes |
| PDF result extraction | Yes |
| X-ray image analysis | Yes |
| All rule-based features | No |
| Demo data, dashboards, scoring | No |

---

## Architecture

```
index.html (single file, ~230KB)
│
├── CSS — custom design system (green/amber palette, UK vet brand)
├── HTML — 12 page sections, modal overlay, login screen
└── JavaScript
    ├── Auth — PIN + password session (sessionStorage)
    ├── Data store — S object (localStorage)
    ├── Chart.js — revenue, service mix, vet breakdown, forecast charts
    ├── Module A — Dashboard rendering engine
    ├── Module B — Reactivation scoring engine (30 demo patients)
    ├── Module C — Health plan calculator
    ├── Module D — Pricing benchmark engine
    ├── Module E — Clinical AI assistant
    ├── Module F — Campaign template library
    ├── Module G — Staff prompt engine
    ├── Module H — KPI forecasting model
    └── Claude API — abstracted fetch layer (all AI calls)
```

**Data flow:**
- Import CSVs → auto-parse → localStorage → dashboard + AI context
- Demo patients (hardcoded seed) → scoring engine → reactivation + prompts + forecast
- No server required — runs entirely in the browser

**To add real integrations:**
- Replace `DEMO_PATIENTS` array with API call to your PMS
- The scoring engine (`scorePatient()`) works identically on real data
- The outreach modal and campaign builder are data-agnostic

---

## Security

- Session expires after 12 hours (configurable in `tryLogin()`)
- All data stored in browser localStorage — never leaves the device
- Claude API calls go directly from browser to `api.anthropic.com` — no proxy
- Change PIN and password before production deployment
- For multi-user environments, consider a server-side session layer

---

## Customisation

### Change PIN and password
```javascript
// In the <script> block at the top:
var PIN='241085', PASS='VillageVet2026!';
```

### Change practice details
```javascript
// In buildCtx():
'Village Veterinary Surgery, Hatfield Garden Village AL10 9JS'

// In campaign templates (CAMPAIGNS array):
phone = '01707 123456';
```

### Change health plan prices
```javascript
// PLAN_TIERS object — adjust price property:
{ name:'Silver', price:32, ... }
```

### Add real patients
```javascript
// Replace or extend DEMO_PATIENTS array
// Required fields: id, name, species, breed, age, sex, weight, neutered,
//   owner, phone, email, lastVisit, nextVaccDue, lastDental,
//   onHealthPlan, planTier, conditions, estimatePending, postOpDue, notes
```

---

## Browser Requirements

- Chrome 90+ (recommended — required for voice recording)
- Firefox 88+, Safari 15+, Edge 90+
- No server, no Node.js, no build step

---

## How This Increases Revenue — Real Practice Impact

### 90-Day Revenue Opportunities

| Initiative | Effort | Estimated Value |
|-----------|--------|----------------|
| Vaccine recall (lapsed patients) | Low | £1,200–£2,400 |
| Dental estimate follow-up | Low | £800–£1,800 |
| Post-op review booking | Very low | £300–£600 |
| Senior wellness campaign | Medium | £1,500–£3,200 |
| Health plan enrolment (5 new) | Medium | £1,056–£2,160/yr |
| Parasite prevention drive | Low | £600–£1,200 |
| Estimate conversion improvement | Medium | £500–£2,000 |

**Conservative 90-day estimate: £6,000–£13,000 in incremental revenue**

### How the Tool Delivers This

1. **Visibility** — turns invisible missed revenue into a ranked, actionable list
2. **Speed** — reception can act in seconds with pre-written scripts
3. **Consistency** — same prompts every day, for every patient
4. **Ethical framing** — every recommendation is clinically appropriate first, commercial second
5. **Team alignment** — vets, nurses, and reception see the same priorities

---

## 30-Day Rollout Plan

### Week 1 — Setup & Familiarisation
- [ ] Load demo data, explore all 8 modules
- [ ] Add Claude API key
- [ ] Review and adjust plan tier pricing
- [ ] Brief reception team on Staff Prompts module
- [ ] Identify top 10 lapsed clients from Growth Engine

### Week 2 — First Outreach
- [ ] Contact top 10 high-priority patients (vaccine + estimate + post-op)
- [ ] Run dental check campaign via SMS/email to clients 3yr+
- [ ] Begin importing Merlin CSV exports for live data
- [ ] Launch Spring Dental Month campaign (if April)

### Week 3 — Health Plan Growth
- [ ] Pitch health plans to every non-member client visiting this week
- [ ] Set up health plan calculator with your actual member numbers
- [ ] Target 3 new plan enrolments this week
- [ ] Review forecast under Base scenario

### Week 4 — Optimise & Measure
- [ ] Review Growth Engine — which opportunities were converted?
- [ ] Run a Senior Wellness campaign for pets 7+
- [ ] Calculate MRR improvement from new plan members
- [ ] Identify next month's campaign focus

---

## Required Data Inputs from the Practice

To get maximum value from live integrations:

| Data | Source | Used For |
|------|--------|---------|
| Invoice records | Merlin PMS | Dashboard KPIs, revenue trends |
| Patient records | Merlin PMS | Growth engine, staff prompts |
| Vaccination history | Merlin PMS | Vaccine recall scoring |
| Dental history | Merlin PMS | Dental campaign targeting |
| DD mandate data | GoCardless | Failure rate alerts |
| Ad spend | Google Ads | Marketing ROI tracking |
| Estimate records | Merlin PMS | Estimate conversion tracking |

---

## Fastest Wins to Implement in First 90 Days

1. **Call the top 5 patients flagged "High Priority"** — these have outstanding estimates or clinical rechecks overdue. Each call is worth £50–£350.
2. **Run a dental awareness SMS** to all clients with pets 3yr+ — dental is the highest-volume underserved service in most practices.
3. **Sign up 3 new health plan members** — each generates £264–£540/year in predictable recurring revenue.
4. **Book all post-op reviews** — Ruby Anderson (TPLO) is flagged in demo data. Every unbooked post-op is both a clinical risk and a missed appointment.
5. **Follow up all pending estimates** — Rosie (£340), Poppy (£210), Bella (£185), Coco (£285) are all demo patients with unconverted estimates totalling £1,020.
6. **Add a health plan pitch to every check-out** — "Before you go, can I mention our health plan?" — even a 10% conversion rate compounds into significant MRR.
7. **Use Staff Prompts at every check-in** — search the patient, read the card, mention one thing. One prompt per visit, every visit.

---

*Built for Village Vet, Hatfield Garden Village. Independent veterinary practice growth tool — clinical care first, revenue second.*
