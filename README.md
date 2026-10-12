# XP160 — Cybersecurity Tabletop Exercise for SAP BTP

**SAP TechEd 2026 · Workshop Session XP160**

> Hands-on incident-response tabletop exercise powered by generative AI on SAP Business Technology Platform.

---

## Table of Contents

1. [Welcome](#1-welcome)
2. [Pre-Session Setup](#2-pre-session-setup)
3. [Session Flow](#3-session-flow-60-minutes)
4. [Facilitation Guidelines](#4-facilitation-guidelines)
5. [Technical Reference](#5-technical-reference)
6. [FAQ](#6-faq)
7. [Contact & Support](#7-contact--support)

---

## 1. Welcome

This workshop puts you in the seat of a security responder during an active ransomware incident targeting an SAP landscape. Using **TTXGenAI** — an AI-powered tabletop exercise generator running on SAP AI Core — you will generate a tailored scenario, work through a series of timed injects, evaluate your team's decisions, and receive a board-ready security report.

<table>
<tr>
<td width="33%" valign="top">

### Scenario Overview
A fictitious NORDIC-CERT advisory has alerted Nordic retail organizations to an active ransomware campaign exploiting an SAP Gateway vulnerability. Your team must detect, contain, and recover — following the incident-response phases of your chosen framework (NIST / ISO 27001 / SAP SIRT).

</td>
<td width="33%" valign="top">

### Learning Objectives
By the end of this session you will be able to:
- Identify SAP-specific attack vectors and IoCs
- Apply a structured IR framework to an SAP incident
- Generate and evaluate injects with AI assistance
- Produce a security recommendations report and executive summary

</td>
<td width="33%" valign="top">

### How To Use This Guide
Follow the numbered sections in order. Facilitators should read [Facilitation Guidelines](#4-facilitation-guidelines) before the session. Participants only need the tool URL and the client brief. All AI generation happens in the browser — no local install required.

</td>
</tr>
</table>

---

## 2. Pre-Session Setup

Complete these four steps **before** the workshop begins.

### Step 1 — Read the Scenario Brief

Your team has received an urgent advisory from NORDIC-CERT. Review it carefully before the exercise begins — it contains the threat intelligence your team will be working with.

**[View the NORDIC-CERT Advisory — NorthernStorm Campaign](fakeincident.md)**

> The advisory covers: attack timeline across three victim organizations, 6-phase TTP breakdown (MITRE ATT&CK mapped), Indicators of Compromise (IP addresses, SAP usernames, file hashes, YARA rules), and recommended immediate actions.

### Step 2 — Download the Client Brief

Your fictional client is **RetailNordic GmbH**, a mid-size multi-country retailer running SAP S/4HANA 2022 on SAP BTP. The client brief describes their system landscape, team structure, and existing security controls.

📄 **[Download Client Brief (PDF)](docs/client-brief.pdf)** *(provided by your facilitator)*

### Step 3 — Access the TTXGenAI Tool

Open the exercise generator in your browser:

```
https://ttxgenai.cfapps.eu10-005.hana.ondemand.com
```

> Your facilitator will provide the API key for this session. Enter it in the **API Access** field on the home screen. The key is valid for the duration of the workshop only.

### Step 4 — Configure Your Exercise

On the home screen, set the following parameters for the workshop scenario:

| Field | Value |
|---|---|
| **Standard / Guideline** | NIST SP 800-61 |
| **SAP Context** | SAP BTP (Business Technology Platform) |
| **Incident Scenario** | Ransomware / Extortion |
| **Industry** | Retail & E-Commerce |
| **Exercise Title** | *(enter your team name, e.g. "Team Alpha — XP160 TechEd 2026")* |
| **Scenario Description** | *(optional — add any specific focus areas from the client brief)* |

Click **Generate Exercise** and wait approximately 30–60 seconds for your tailored exercise to be created.

---

## 3. Session Flow — 60 Minutes

```
──────────────────────────────────────────────────────────────────────────────
  0:00        0:10         0:25                    0:50          1:00
   │           │            │                       │             │
   ▼           ▼            ▼                       ▼             ▼
[Briefing] [Generate] [Work Injects] ──────── [Debrief] [Report & Wrap-up]
```

### Phase 1 — Briefing & Setup (0:00 – 0:10)

- Facilitator presents the NORDIC-CERT advisory (10 min)
- Teams read the client brief
- Each team configures and generates their exercise in TTXGenAI
- Confirm the exercise loaded correctly before proceeding

### Phase 2 — Inject Evaluation (0:10 – 0:50)

This is the core exercise phase. Teams work through **8 timed injects**, each representing a decision point in the incident response. For each inject:

1. Read the situation update out loud to your team
2. Discuss what your team would do — reference the client brief and your chosen IR framework
3. Select **Success** or **Fail** based on whether your team's response matches best practice
4. Add a comment explaining your decision (required for the final report)
5. Click **Submit** to move to the next inject

**Time guidance per inject: ~5 minutes**

> The facilitator will announce time at the midpoint (inject 4) and at inject 7. If your team is running behind, prioritize discussion over perfect answers — the debrief is where learning happens.

### Phase 3 — Debrief & Report (0:50 – 1:00)

- Click **Generate Security Report** when all injects are submitted
- Wait for AI to generate your recommendations (~20 seconds)
- Review the **Security Recommendations** page with your team
- Export two documents:
  - **Recommendations (DOCX)** — detailed findings grouped by priority
  - **Board Summary (DOCX)** — executive briefing for non-technical stakeholders

---

## 4. Facilitation Guidelines

### Do's and Don'ts

<table>
<tr>
<th width="50%">✅ Do</th>
<th width="50%">❌ Don't</th>
</tr>
<tr>
<td>

- Encourage every team member to speak
- Let teams make imperfect decisions — that's the point
- Use the "inject timer" to create time pressure (5 min per inject)
- Reference real SAP transactions and tools during discussion
- Ask "what would you actually do in your environment?" after each inject
- Pause at inject 4 for a 2-minute gut-check with the group
- Allow disagreement — divergent views reveal gaps

</td>
<td>

- Don't correct teams mid-inject; save it for the debrief
- Don't let one person dominate — rotate the "spokesperson" role
- Don't skip injects to save time — every inject builds on the previous one
- Don't treat the AI's evaluation as ground truth; it's a starting point for discussion
- Don't ignore inject comments — they drive the quality of the final report
- Don't close the browser tab during generation (session is in-memory)

</td>
</tr>
</table>

### Facilitator Cheat Sheet

Use this table during the inject phase to guide discussion when a team is stuck.

| Inject Theme | Prompt Question | Key Point to Surface |
|---|---|---|
| Initial Detection | "How would you know this was happening?" | SAP Security Audit Log (SM20), SIEM alerting on RFC anomalies |
| Scope Assessment | "Which systems are you most worried about?" | S/4HANA, HANA DB, Backup infrastructure — in that order |
| Containment | "What do you isolate first and how?" | Gateway firewall block, disable suspicious user accounts (SU01) |
| Communication | "Who gets a call in the first hour?" | CISO, Legal, Data Protection Officer — all simultaneously |
| Evidence Preservation | "What logs are you capturing and how?" | SM20, SM21, OS-level logs — chain of custody matters |
| Eradication | "How do you know it's fully gone?" | Re-image compromised systems; don't just patch and restart |
| Recovery | "What's your go/no-go criteria before going live?" | Validated clean backup, patched vulnerability, reset all credentials |
| Lessons Learned | "What would you change in your environment today?" | Drives the board summary — most important inject |

---

## 5. Technical Reference

<details>
<summary><strong>TTXGenAI — Architecture & How It Works</strong></summary>

### System Architecture

```
Browser
  │
  ▼
TTXGenAI (FastAPI / SAP BTP Cloud Foundry)
  │
  ├─ Exercise Generation ──► SAP AI Core (Claude claude-sonnet-4-6)
  │                              via Orchestration Service
  │
  ├─ Exercise Store ──────► In-memory (session lifetime)
  │
  ├─ Exercise Library ────► SQLite (persistent, WAL mode)
  │                              exercise_runs → evaluations_json + recommendations_json
  │
  └─ Document Export ─────► python-docx (DOCX generation in-process)
```

### Key Capabilities

| Feature | How to Access |
|---|---|
| Generate tailored scenario | Home page → fill form → Generate Exercise |
| Evaluate injects | Exercise page → Success/Fail + comment per inject |
| Generate security report | Exercise page → Generate Security Report |
| Export Recommendations DOCX | Security Report page → "Recommendations (DOCX)" |
| Export Board Summary DOCX | Security Report page → "Board Summary (DOCX)" |
| View historical runs | Library → expand exercise row → View Evaluation |
| Fork / modify exercise | Library → Fork button |
| Upload incident documents | Incident Library → Upload PDF/DOCX |

### Session Lifecycle

The exercise session is stored in-memory and tied to a browser session. If you close the tab or the session expires, the exercise will be lost unless you have already run it (which saves it to the library automatically). Always complete the full flow — from generation through to report — in one session.

</details>

<details>
<summary><strong>SAP Security Context — Attack Surface Reference</strong></summary>

### SAP Attack Vectors (Relevant to This Exercise)

| Vector | Description | Detection |
|---|---|---|
| **CVE-2024-0847** | SAP Gateway RCE — unauthenticated remote code execution on unpatched systems | SAP Security Note 3411067; check via SPAM |
| **RFC Backdoor** | Unauthorized RFC connection created to enable persistent access | SM59 — audit all connections, especially Z_ prefix |
| **Privilege Escalation** | Creation of accounts with SAP_ALL or reactivation of dormant privileged users | SE16 → USR02; SU01 — check creation date and profile |
| **Data Exfiltration** | Export of key SAP tables (KNA1, LFA1, BSEG, USR02) to external storage | Network DLP; SAP Security Audit Log RFC_CALL events |
| **Backup Targeting** | Ransomware operators compromise backup infrastructure before encrypting production | Verify backup system network isolation; test restore weekly |

### Critical SAP Transactions for IR

| Transaction | Purpose |
|---|---|
| `SM20` | Security Audit Log — review all critical events |
| `SM21` | System Log — OS-level and ABAP messages |
| `SU01` | User Administration — list, lock, delete accounts |
| `SM59` | RFC Connections — audit all remote connections |
| `SE16` | Table Browser — query USR02, AGR_USERS, RSAUPROF |
| `SPAM / SAINT` | Software patch management — apply SAP Security Notes |
| `RSAU_CONFIG` | Configure Security Audit Log parameters |
| `SM66` | Global Work Process Overview — detect unusual RFC processes |

### SAP BTP Security Considerations

In a BTP context, the attack surface extends to:
- **SAP BTP Cockpit** — Global Account / Subaccount access control
- **SAP XSUAA** — OAuth2 token misuse; check bound service instances
- **SAP AI Core** — Model API access; audit AI resource group bindings
- **Cloud Foundry** — App environment variables containing secrets; `cf env` exposure
- **Destination Service** — RFC/HTTP destinations with stored credentials

</details>

<details>
<summary><strong>NIST SP 800-61 — IR Framework Quick Reference</strong></summary>

This exercise follows the NIST SP 800-61 Rev. 2 incident response lifecycle. Use this reference during inject evaluation.

### Phase 1 — Preparation
*Done before the incident. Cannot be "played" — but injects will test whether preparation was adequate.*

Key preparation activities: IR plan, contact lists, out-of-band communication channel, documented backup/restore procedures, security monitoring configured.

### Phase 2 — Detection & Analysis

| Activity | SAP Specifics |
|---|---|
| Monitor alerts | SM20 / SIEM integration; SAP ETD (Enterprise Threat Detection) |
| Identify affected systems | Landscape diagram; RFC connections map (SM59) |
| Determine incident scope | Business impact: which processes are down? Customer data exposure? |
| Assign severity | P1 = production down / data exfiltration; P2 = partial; P3 = suspected |
| Notify stakeholders | CISO + Legal + DPO within 1 hour of P1 declaration |

### Phase 3 — Containment, Eradication & Recovery

| Step | Action |
|---|---|
| **Short-term containment** | Isolate affected system(s) from network; block attacker IPs at firewall |
| **Evidence collection** | Preserve SM20/SM21 logs; memory dump if possible; chain of custody |
| **Eradication** | Remove malware artifacts; revoke all compromised credentials; patch CVE |
| **Recovery** | Restore from last known-clean backup; verify data integrity before go-live |

### Phase 4 — Post-Incident Activity

- Written incident report within 72 hours (data breach) or 5 business days (internal policy)
- Root cause analysis
- Control improvements — map to CIS Controls or ISO 27001 Annex A
- Update IR playbook
- Executive briefing (use the Board Summary export from TTXGenAI)

### GDPR/Notification Obligations (EU context)
If personal data was exfiltrated, supervisory authority notification is required **within 72 hours** of becoming aware of the breach. Customer notification is required if the breach is likely to result in high risk to individuals.

</details>

---

## 6. FAQ

**Q: The exercise generation is stuck or returned an error — what do I do?**

Check the API key is entered correctly (no leading/trailing spaces). If the error message mentions "401" or "authentication", the key may have expired — ask your facilitator for a fresh key. If generation times out (>90 seconds), refresh and try again.

---

**Q: Can I save my exercise and come back to it later?**

Yes — once you complete the full flow and the exercise is saved to the library, it persists in the database. Use the **Library** page to find previous exercises and click **View Evaluation** on any run to see the full security report.

---

**Q: My team disagrees on whether an inject is Success or Fail — what do we submit?**

Submit the majority vote and capture the minority view in the comment field. The AI-generated recommendations will reflect your submitted evaluations, but the debrief discussion is where the real learning happens. Disagreement is a feature, not a bug.

---

**Q: The Board Summary DOCX export doesn't have our company name — is that expected?**

Yes — the document uses the exercise title you entered in the setup form. For a branded output, set the **Exercise Title** field to include your organization name (e.g., "RetailNordic GmbH — BTP Ransomware Response, TechEd 2026") before generating.

---

**Q: We finished early — what should we do with the remaining time?**

Use the **Fork** feature in the library to create a variant of your exercise. Try changing the SAP Context (e.g., from BTP to S/4HANA on-premise) or the Scenario (e.g., from Ransomware to Insider Threat) and see how the injects change. You can also upload a real (anonymized) incident PDF to the **Incident Library** to inspire the next exercise.

---

**Q: Is the data from this exercise shared with Anthropic or stored outside SAP?**

No. The LLM calls are made via SAP AI Core's Orchestration Service using SAP's own tenant credentials. Data does not leave the SAP AI Core infrastructure. The exercise content is stored only in the BTP Cloud Foundry application's local SQLite database. No personal data should be entered into the tool.

---

**Q: Can I deploy TTXGenAI in my own SAP BTP tenant?**

Yes — the source code is available in this repository. You will need an SAP AI Core instance with a Claude model deployment. See the [Technical Reference](#5-technical-reference) section for architecture details. The deployment uses a standard `cf push` workflow with a `manifest.yml`.

---

## 7. Contact & Support

| | |
|---|---|
| **Session facilitator** | Your designated TechEd session host |
| **Technical issues (tool)** | Open an issue in this repository |
| **SAP Security questions** | [SAP Trust Center](https://www.sap.com/about/trust-center/security.html) |
| **SAP AI Core documentation** | [SAP Help Portal — AI Core](https://help.sap.com/docs/sap-ai-core) |

---

<details>
<summary>About This Exercise</summary>

This tabletop exercise was developed for **SAP TechEd 2026, Session XP160**. The scenario, threat actor, victim organizations, and all technical indicators in the NORDIC-CERT advisory are **entirely fictional** and created for educational purposes.

The TTXGenAI tool is an open-source project built on:
- SAP BTP Cloud Foundry (hosting)
- SAP AI Core / Orchestration Service (LLM generation)
- FastAPI + Jinja2 (web framework)
- SQLite (exercise persistence)
- python-docx (report generation)

Contributions and feedback are welcome via GitHub Issues.

</details>

---

*SAP TechEd 2026 · Session XP160 · [SAP Samples](https://github.com/SAP-samples)*
