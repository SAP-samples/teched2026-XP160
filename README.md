# XP160 — Cybersecurity Tabletop Exercise for SAP BTP

**SAP TechEd 2026 · Workshop Session XP160**

> Hands-on incident-response tabletop exercise powered by generative AI on SAP Business Technology Platform.

---

## Table of Contents

1. [Welcome](#1-welcome)
2. [Pre-Session Setup](#2-pre-session-setup)
3. [Session Flow](#3-session-flow)
4. [Wrap-up](#4-wrap-up)
5. [Facilitation Guidelines](#5-facilitation-Guidelines)
6. [Technical Reference](#6-technical-reference)
7. [Contact & Support](#7-contact--support)

---

## 1. Welcome

This workshop puts you in the seat of a security responder during an active ransomware incident targeting an SAP landscape. Using **TTXGenAI** — an AI-powered tabletop exercise generator running on SAP AI Core — you will generate a tailored scenario, work through a series of timed injects, evaluate your team's decisions, and receive a board-ready security report.

<table>
<tr>
<td width="33%" valign="top">

### Scenario Overview
A fictitious NORDIC-CERT advisory has alerted Nordic retail organizations to an active ransomware campaign exploiting an SAP Gateway vulnerability. Your team must be ready to detect, contain, and recover — following the incident-response phases of your chosen framework (NIST / ISO 27001 / SAP SIRT).

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

📄 **[Download Client Brief (PDF)](docs/GlobalRetail4U_Client_Profile.pdf)**

### Step 3 — Access the TTXGenAI Tool

Open the exercise generator in your browser:

```
https://ttxgenai.cfapps.eu10-005.hana.ondemand.com
```

### Step 4  — Powerpoint slides

📄 **[Presentation Slides (pptx)](/teched2026-XP160.pptx)**

---

## 3. Session Flow 

```
──────────────────────────────────────────────────────────────────────────────
  0:00        0:10         0:40                    0:50          1:00
   │           │            │                       │             │
   ▼           ▼            ▼                       ▼             ▼
[Briefing] [Generate] [Evaluate & Report] ──────── [Debrief]   [Wrap-up]
```

### Phase 1 — Introduction & Demo (0:00 – 0:10)

- Introduction of the TableTop exercise concept 
- Presentation of the tool
- Quick Demo on how to use the tool

### Phase 2 — Generate (0:10 – 0:40)

This is the core exercise phase. Today, you're stepping into the role of a security consultant using TTXGenAI to deliver rapid incident response training to a client. You'll learn how to transform threat intelligence from real-world incidents into actionable tabletop exercises in **minutes**, **not weeks**. You need to understand the customer profile, the threat and configure accordingly the exercise to be generated and executed.

1. From the security bulletin published by the CERT organisation **[View the NORDIC-CERT Advisory — NorthernStorm Campaign](fakeincident.md)** create a .docx or .txt file containing all the report. Save this file locally and name it with a mention to your identifier/pseudo/name.
2. Open the tool https://ttxgenai.cfapps.eu10-005.hana.ondemand.com and click on "Incident Library". Add the file that you just created to the library
3. Back to the main page to create a new exercise. In the field "Exercise Title" add a title to you exercise with a reference to your identifier/pseudo/name.
4. Use the information of the GlobalRetail4U company **[Download Client Brief (PDF)](docs/GlobalRetail4U_Client_Profile.pdf)** to fill the "Exercise Parameters". For the "Standard/Guideline" use NIST SP 800-84
5. In the section "Scenario Description" explain the type of exercise you want, and stick with a **15 minutes**  duration and **only 2 injects**
6. In the "Real Incident Inspiration" section, select the name of the file thatyou uploaded to your library
7. Click on Generate exercise and have a drink


**Let's spend 5 minutes to compare the different results**



### Phase 3 — Evaluate & Report (0:40 – 0:50)

1. Now it's time to test the evaluation capabiltities
2. For the first "Inject Evaluation" select **fail** and chose a random observation (like no answer)
3. For the Secont "Inject Evaluation" select **Success** and copy pase the "Expected Actions" suggestion in the observation.
4. Click **Generate Security Report** when all injects are submitted
5. Wait for AI to generate your recommendations (~20 seconds)
6. Review the **Security Recommendations** That we will discuss together
7. Export two documents:
  - **Recommendations (DOCX)** — detailed findings grouped by priority
  - **Board Summary (DOCX)** — executive briefing for non-technical stakeholders

---

## 4. Wrap-up 

💼 Some Homework:
Within 48 hours after this session, we invite you to :
1.	Generate ONE exercise for a real or hypothetical Company 
2.	Upload ONE threat intelligence document (news article, CERT advisory, etc.)
3.	Draft a 1-page service offering you could pitch to your team or to your customer
4.	If you see a value torun the exercise we can support you 

---

## 5. Facilitation Guidelines

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

---

## 6. Technical Reference

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


---

## 7. Contact & Support

| | |
|---|---|
| **Slim TRABELSI** | slim.trabelsi@sap.com |
| **Technical issues (tool)** | Open an issue in this repository |
| **SAP Security questions** | [SAP Trust Center](https://www.sap.com/about/trust-center/security.html) |
| **SAP AI Core documentation** | [SAP Help Portal — AI Core](https://help.sap.com/docs/sap-ai-core) |

---

<details>
<summary>About This Exercise</summary>

This tabletop exercise was developed for **SAP TechEd 2026, Session XP160**. The scenario, threat actor, victim organizations, and all technical indicators in the NORDIC-CERT advisory are **entirely fictional** and created for educational purposes.


Contributions and feedback are welcome via GitHub Issues.

</details>

---

*SAP TechEd 2026 · Session XP160 · [SAP Samples](https://github.com/SAP-samples)*
