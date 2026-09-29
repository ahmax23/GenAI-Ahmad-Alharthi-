# IT Helpdesk Meeting Follow-up Assistant

Final project for the Generative AI for Productivity course (SDAIA Academy).
Tool used: Claude. All names and data in this project are fictional.

---

## Project Name
**IT Helpdesk Meeting Follow-up Assistant**

## Idea Selected
**1. Meeting Follow-up Assistant**, customized for an IT Helpdesk team.

## Project Goal
Help the IT Helpdesk team turn quick meeting notes into a clear follow-up: a summary, a task list with owners, and a follow-up email. The assistant should also hide any passwords or sensitive data found in the notes.

## Problem Statement
In our IT team we have many meetings, like weekly meetings and calls after a system outage. The notes are usually short and messy. Because of this:

- Some tasks are forgotten or have no owner.
- Writing the follow-up email takes time, so sometimes it is not sent.
- Sometimes notes include sensitive data, like a temporary password, and it can be shared by mistake.

## Target Users
- IT Helpdesk team leads
- IT staff who write meeting notes and follow up on tasks

---

## How to Use
1. Copy the prompt below into Claude (or ChatGPT / Gemini).
2. Paste the meeting notes under it. Remove any real passwords or personal data first.
3. Review the output before sending the email.

---

## R-C-T-F Prompt

```text
Role:
You are an experienced IT Service Desk coordinator who writes clear, professional
meeting follow-ups for an IT Helpdesk team in a university environment.

Context:
I will paste raw notes from an IT team meeting (weekly sync, outage call, or change
review). The notes are messy: short fragments, abbreviations, missing owners or dates,
and sometimes sensitive technical details. The follow-up will be shared with the IT
team and possibly with non-technical stakeholders.

Task:
1. Read the notes and extract: summary, decisions, action items, open questions,
   and risks.
2. For each action item, identify the owner, due date, and priority
   (P1 = urgent / service impact, P2 = important, P3 = normal).
3. Detect any sensitive data (passwords, API keys, IP addresses, usernames,
   personal data). Replace it with [REDACTED] and list it under "Needs Human Review".
4. Write a short, professional follow-up email that is safe to send.

Format:
Return the answer in Markdown using exactly these sections:
1. Executive Summary (2–3 sentences)
2. Key Decisions (bullets)
3. Action Items (table: # | Task | Owner | Due Date | Priority | Status)
4. Open Questions (bullets)
5. Risks & Blockers (bullets)
6. Needs Human Review (bullets: redacted data, unconfirmed facts, missing owners)
7. Suggested Actions (not from the notes) (bullets: your own recommendations,
   clearly separated from what was actually agreed)
8. Follow-up Email (Subject + body, max 150 words, agreed actions only)

Rules:
- Use only the information in the notes. Do not invent names, dates, numbers,
  root causes, decisions, or action items.
- Any recommendation that is not in the notes goes ONLY under "Suggested Actions".
- Mark any missing owner or date as TBD.
- If something is uncertain in the notes (e.g., "maybe", "?"), label it "Unconfirmed".
- Never repeat passwords or secrets in any section, including the email.
- Set Status to "Not started" unless the notes say otherwise.
- Keep the tone professional and concise.
```

---

## Sample Input 1: Weekly Helpdesk Sync

```text
IT Helpdesk weekly sync - Sun 27 Sep 2026
attendees: Faisal (lead), Noura, Majed, Reem
- ticket backlog is 143 open, up from 110 last week. mostly printer + VPN issues after the windows update
- agreed: majed to push printer driver fix via SCCM to all labs by thursday
- noura will write a KB article for VPN reconnect steps, no date yet
- reem asked if we need extra staff for registration week (starts 11 oct?) - faisal to check with management
- SLA for P1 tickets was missed twice this week
- everyone agreed to add a new ticket category "Student Portal"
- risk: only one person knows the backup server config (majed)
```

## Sample Output 1

### 1. Executive Summary
The team reviewed a rising ticket backlog (143 open, up from 110), driven mainly by printer and VPN issues after the Windows update. The team agreed on a printer driver fix, a new "Student Portal" ticket category, and a VPN knowledge base article. Staffing for registration week and repeated P1 SLA misses need follow-up.

### 2. Key Decisions
- Push the printer driver fix via SCCM to all labs.
- Add a new ticket category: **Student Portal**.

### 3. Action Items

| # | Task | Owner | Due Date | Priority | Status |
|---|---|---|---|---|---|
| 1 | Push printer driver fix via SCCM to all labs | Majed | Thursday | P1 | Not started |
| 2 | Write KB article for VPN reconnect steps | Noura | TBD | P2 | Not started |
| 3 | Check with management about extra staff for registration week | Faisal | TBD | P2 | Not started |
| 4 | Add "Student Portal" category to the ticketing system | TBD | TBD | P3 | Not started |

### 4. Open Questions
- Is extra staff needed for registration week?
- What is the exact start date of registration week? (Notes say "11 Oct?")
- Who will add the new "Student Portal" category?

### 5. Risks & Blockers
- **Single point of failure:** only Majed knows the backup server configuration.
- Backlog is growing (+33 tickets in one week).
- P1 SLA was missed twice this week.

### 6. Needs Human Review
- Registration week start date (11 Oct) is **Unconfirmed**.
- Due dates are missing for items 2–4, and the owner is missing for item 4.
- "Thursday" has no exact date. Confirm which Thursday.

### 7. Suggested Actions (not from the notes)
- Investigate why the P1 SLA was missed twice and agree on a fix.
- Document the backup server configuration and train a second team member.

### 8. Follow-up Email
**Subject:** Follow-up: IT Helpdesk Weekly Sync – 27 Sep 2026

Dear team,

Thank you for today's sync. Our backlog is now 143 open tickets, mainly printer and VPN issues after the Windows update.

Agreed actions:
- Majed will push the printer driver fix to all labs via SCCM by Thursday.
- Noura will prepare a KB article on VPN reconnect steps.
- Faisal will check with management about extra staff for registration week.
- We will add a new "Student Portal" ticket category.

Please note that the P1 SLA was missed twice this week. We also noted that only Majed currently knows the backup server configuration.

Best regards,
[Your Name]

---

## Sample Input 2: Outage Call Notes (contains sensitive data)

```text
quick notes from call w/ network team after the outage yesterday
email down for ~2 hrs, root cause maybe the firewall rule change?? not confirmed
khalid said he'll send the RCA report
temp admin pw for the mail server is Mail@2026! - share with the team
we need to inform the users + deans office
someone needs to review change mgmt process, who?
next call same time next week
```

## Sample Output 2

### 1. Executive Summary
Email service was down for about 2 hours yesterday. The root cause is not confirmed; a firewall rule change is suspected. Khalid will send the RCA report, users and the Dean's office need to be informed, and the change management process needs review.

### 2. Key Decisions
- A follow-up call will be held at the same time next week.

### 3. Action Items

| # | Task | Owner | Due Date | Priority | Status |
|---|---|---|---|---|---|
| 1 | Send the RCA (Root Cause Analysis) report | Khalid | TBD | P1 | Not started |
| 2 | Inform users and the Dean's office about the outage | TBD | TBD | P1 | Not started |
| 3 | Review the change management process | TBD | TBD | P2 | Not started |

### 4. Open Questions
- What was the confirmed root cause of the outage?
- Who will review the change management process?
- Who will send the communication to users and the Dean's office?

### 5. Risks & Blockers
- A privileged password was written in plain text in the meeting notes and marked "share with the team".
- If the firewall change is the cause, similar changes may cause another outage without a proper review process.

### 6. Needs Human Review
- **[REDACTED] admin password** for the mail server was found in the notes. It was removed from this output and must not be shared.
- Root cause (firewall rule change) is **Unconfirmed**.
- Outage duration ("~2 hrs") is approximate.
- Owners are missing for items 2 and 3. Due dates are missing for all items.
- "Same time next week" has no exact date or time.

### 7. Suggested Actions (not from the notes)
- Change the mail server admin password, because it was written in plain text.
- Share credentials only through an approved password manager, never by email or chat.

### 8. Follow-up Email
**Subject:** Follow-up: Email Service Outage Call

Dear team,

Thank you for joining the call about yesterday's email outage, which lasted about 2 hours. The root cause is still under investigation.

Next steps:
- Khalid will share the RCA report.
- We need to inform users and the Dean's office (owner to be confirmed).
- We need a volunteer to review the change management process.

Our next call is at the same time next week.

Best regards,
[Your Name]

---

## Safety Checklist
- [x] I used fictional names and dummy data only, no real work data.
- [x] No real passwords, IDs, or confidential information were pasted into the AI tool (the password in Input 2 is fake).
- [x] I tested the prompt with notes that include a password (Input 2), and the AI hid it as [REDACTED].
- [x] The prompt tells the AI not to invent information and to write TBD when something is missing.
- [x] I checked the names, numbers, and dates in the output against the original notes.
- [x] A person must review the output before sending it. The AI does not send anything by itself.

---

## Reflection

**What I learned:**
I learned how to write a prompt using R-C-T-F. Adding clear rules, like "do not invent" and "use TBD", made the output more accurate.

**How AI helped me:**
It turned messy notes into a clear summary, task table, and email in a few seconds. It also showed me missing owners and dates.

**What I checked:**
I compared the output with the original notes and made sure the password in Input 2 did not appear in the output.

**What I would improve next:**
I would save the prompt in a Claude Project so my team can reuse it, and add an Arabic version of the email.
