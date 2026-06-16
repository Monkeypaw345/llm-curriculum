# COBOL Cowork Master Prompts
## Vu | NEC Client Project (via Tony) + NTUST Thesis (Prof. Yang) | June 2026
## Paste these into Claude Cowork → Tasks whenever memory is lost

---

> **How to use this file:**
> - **Prompt A** = paste daily to generate your lesson document
> - **Prompt B** = paste once to set up the 9am schedule (re-paste if Cowork loses it)
> - This file is your source of truth. If Cowork forgets anything, come back here.

---

## PROMPT A — DAILY TEACHING SESSION
### Paste this into Cowork → Tasks every morning (or let the schedule run it)

```
DAILY COBOL TEACHING SESSION — ADAPTIVE CURRICULUM
Context file: Read the full learning plan below before
doing anything.

═══════════════════════════════════════
LEARNING CONTEXT
═══════════════════════════════════════

ROLE: I am a Master's student at NTUST Taipei, final
year. I have two COBOL-related tracks:

1. Client project (NEC via Tony): Read real COBOL
   codebases and annotate business rules in plain
   English. Active client obligation. Two-week
   timeline to become functional.

2. Thesis (Prof. Yang): Evaluate how well an LLM
   translates COBOL business rules to JavaScript —
   specifically where business logic survives or is
   lost. I am the verifier. Fine-tuning is Phase 2.
   Current phase is pure evaluation.

These are separate outputs. Never conflate them.

MY ONE JOB: Read a COBOL program and write a
plain-English sentence that captures what the
business rule is doing.

I will never write COBOL.
I will never run COBOL.
I read it and extract what it means in plain English.

WHAT TO IGNORE COMPLETELY:
- Writing COBOL
- Compiling or running COBOL (no GnuCOBOL setup)
- COBOL history or mainframe architecture
- JCL (Job Control Language)
- COBOL file I/O (READ, WRITE, OPEN, CLOSE)
- SORT and MERGE operations
- Report writer
- Anything beyond reading comprehension

CHAPTER 7 FILTER — apply before every session:
"Does this help me read and annotate a business
rule faster and more accurately?"
Yes → include it.
No → skip it entirely.

═══════════════════════════════════════
THE FOUR LAYERS
═══════════════════════════════════════

LAYER 1 — The Four Divisions
Duration: Half a day | Deadline: Day 1

Every COBOL program has the same four-part structure:

  IDENTIFICATION DIVISION. → Program name only. Glance
                              and move on.
  ENVIRONMENT DIVISION.    → File connections. Skim,
                              don't study.
  DATA DIVISION.           → All variables + possible
                              values. CRITICAL.
  PROCEDURE DIVISION.      → All business logic.
                              CRITICAL.

The skill: Open any COBOL file and within 30 seconds
locate the DATA DIVISION and PROCEDURE DIVISION.

Done when: Given a 500-line COBOL program, can jump
directly to DATA DIVISION and PROCEDURE DIVISION
without reading top to bottom.

LAYER 2 — DATA DIVISION Fluency
Duration: 1–2 days | Deadline: Day 3

Level numbers — the data hierarchy:
  01  CUSTOMER-RECORD.
      05  CUSTOMER-NAME       PIC X(30).
      05  CUSTOMER-BALANCE    PIC 9(7)V99.
      05  CUSTOMER-STATUS     PIC X.
01 is parent. 05 is child. Indentation = relationship.

PIC clauses — data type and size:
  PIC X(n)   → text, n characters
  PIC 9(n)   → number, n digits
  PIC 9(n)V99 → number with 2 decimal places
  PIC S9(n)  → signed number (can be negative)

88-level conditions — THE MOST IMPORTANT THING:
  05  CUSTOMER-STATUS     PIC X.
      88  ACTIVE-CUSTOMER     VALUE 'A'.
      88  SUSPENDED           VALUE 'S'.
      88  CLOSED-ACCOUNT      VALUE 'C'.

When you see IF ACTIVE-CUSTOMER in PROCEDURE DIVISION
it means IF CUSTOMER-STATUS = 'A'.

Why this matters for thesis: LLMs regularly miss this
mapping. Every annotation using 88-levels gets flagged:
"LLM failure risk: High."

Done when: Given an unseen DATA DIVISION, can list
all variables, types, and 88-level values within
5 minutes without notes.

LAYER 3 — PROCEDURE DIVISION Reading
Duration: 2–3 days | Deadline: Day 6

IF/ELSE chains — can nest deeply:
  IF CUSTOMER-BALANCE > 10000
      IF ACTIVE-CUSTOMER
          PERFORM APPLY-PREMIUM-RATE
      ELSE
          PERFORM APPLY-STANDARD-RATE
  ELSE
      PERFORM FLAG-LOW-BALANCE
  END-IF.

EVALUATE — COBOL's switch/case:
  EVALUATE CUSTOMER-STATUS
      WHEN 'A'    PERFORM PROCESS-ACTIVE
      WHEN 'S'    PERFORM PROCESS-SUSPENDED
      WHEN 'C'    PERFORM CLOSE-ACCOUNT
      WHEN OTHER  PERFORM HANDLE-UNKNOWN
  END-EVALUATE.

PERFORM — calls a paragraph (like a function):
When you see PERFORM APPLY-PREMIUM-RATE, find that
paragraph and read what it does. This is how logic
is reused across the program.

COMPUTE and MOVE — arithmetic and state changes:
  COMPUTE FINAL-AMOUNT = BASE-AMOUNT * INTEREST-RATE / 100.
  MOVE 'A' TO CUSTOMER-STATUS.

Done when: Given a PROCEDURE DIVISION snippet with
IF/ELSE, EVALUATE, and PERFORM, can write the
plain-English business rule within 5 minutes.

LAYER 4 — Business Rule Extraction
Duration: Ongoing | Starts Day 4, parallel with L3

THE ANNOTATION FORMAT — use every single time:

  SNIPPET ID: [filename + line numbers]

  COBOL BLOCK:
  [paste the relevant COBOL block here]

  BUSINESS RULE:
  [1–3 plain-English sentences]

  RULE TYPE:
  [ ] Conditional logic
  [ ] Calculation
  [ ] State change
  [ ] Validation
  [ ] Other

  KEY DATA ELEMENTS:
  [list critical variables and 88-level values if any]

  LLM FAILURE RISK: [High / Medium / Low]
  Reason:
    High: 88-level conditions, nested IF chains,
          PERFORM chains across paragraphs
    Medium: COMPUTE with multiple variables,
            EVALUATE with many WHEN clauses
    Low: Simple MOVE, straightforward IF/ELSE
         with literal values

Why the failure risk field matters: I am predicting
where the LLM will fail BEFORE experiments run.
That prediction + verification is the hallucination
detection layer — the novel contribution of the thesis.

Done when: Can open any X-COBOL dataset snippet and
produce a complete annotation within 5 minutes.

═══════════════════════════════════════
THE 15-DAY PLAN
═══════════════════════════════════════

Day 1  | L1 | Open 3 different COBOL programs from
  X-COBOL dataset. Navigate to DATA and PROCEDURE
  DIVISION in each. Time yourself.
  Done when: Under 30 seconds per file.

Day 2  | L2 | Read DATA DIVISION of 3 programs. List
  all variables, PIC types, 88-level conditions.
  No PROCEDURE DIVISION yet.
  Done when: 3 data maps written by hand.

Day 3  | L2 | Drill 88-level conditions. Find 5
  programs with 88-levels. For each, write what each
  named condition maps to in raw values.
  Done when: Can translate any 88-level to its VALUE
  instantly.

Day 4  | L2+L3 | Read first PROCEDURE DIVISION. Focus
  on one IF/ELSE chain only. Write the plain-English
  rule. Find PERFORM targets and read those paragraphs.
  Done when: First complete annotation in standard
  format.

Day 5  | L3 | EVALUATE statements — find 3 programs
  that use EVALUATE. Read each, write the rule set
  in plain English.
  Done when: 3 EVALUATE annotations completed.

Day 6  | L3 | PERFORM chains — find a program where
  PERFORM calls lead to sub-paragraphs. Map the full
  call chain. Write the rule including sub-paragraphs.
  Done when: One multi-level PERFORM chain fully mapped.

Day 7  | L3+L4 | Full program read — pick one complete
  program, read DATA + PROCEDURE together. Produce
  2–3 annotations covering different rule types.
  Done when: 3 more annotations logged. Running total: 5.

Day 8  | L4 | Speed drill — annotate 2 snippets back
  to back, timing yourself. Target: under 7 min each.
  Done when: 2 timed annotations. Note where you
  slowed down.

Day 9  | L4 | Failure risk focus — go back to existing
  5 annotations. Re-examine LLM failure risk field.
  Adjust any that feel wrong.
  Done when: All 5 annotations have justified failure
  risk ratings.

Day 10 | L4 | COMPUTE-heavy programs — find programs
  with calculation logic. Annotate 2.
  Done when: 2 calculation annotations. Running total: 7.

Day 11 | L4 | Cold read — pick an unseen program.
  Annotate completely within 10 minutes without help.
  Done when: One cold annotation completed under time.

Day 12 | L4 | Nested complexity — nested IF inside
  EVALUATE inside PERFORM. The hardest pattern.
  Take your time.
  Done when: One complex annotation completed.

Day 13 | L4 | Annotations 9 and 10. Two new snippets,
  full format, timed. Target: under 5 min each.
  Done when: 10 total annotations in log.

Day 14 | Review | Review all 10 annotations. Are the
  business rules accurate? Are failure risk ratings
  consistent? Fix anything wrong.
  Done when: 10 clean, consistent annotations.

Day 15 | Checkpoint | Cold test — pick 2 programs never
  seen before. Annotate both. No time pressure.
  Quality only.
  Done when: Ready to show Prof. Yang.

═══════════════════════════════════════
SESSION STRUCTURE — 90 MIN/DAY
═══════════════════════════════════════

0–15 min  | One new syntax pattern — open IBM COBOL
            reference or X-COBOL paper, read one
            concept, close it.
15–75 min | Open X-COBOL dataset, annotate real
            snippets using the standard format.
75–90 min | Log what confused you and why — this
            becomes your annotation guide.

The log is non-negotiable. One paragraph per session.
What you annotated, what confused you, what pattern
you noticed.

═══════════════════════════════════════
YOUR TASK RIGHT NOW
═══════════════════════════════════════

STEP 1 — FIND TODAY'S DAY NUMBER
Check today's date. Count from June 15, 2026 as Day 1.
Today is Day [N]. Identify which layer and task from
the plan above.

STEP 2 — SCAN MY COBOL BOOKS AND RESOURCES
Search these folders for any PDF or ebook files
related to: COBOL, mainframe programming, IBM COBOL,
business rules, PROCEDURE DIVISION, DATA DIVISION,
PIC clauses, COBOL syntax.
Check: Desktop, Documents, Downloads, and any folder
named "COBOL", "Books", "Programming", or "Reference".
List every relevant file you find before proceeding.

STEP 3 — APPLY THE CHAPTER 7 FILTER
Before extracting anything, ask:
"Does this content help me read and annotate a
business rule faster and more accurately?"
If yes → extract it.
If no → skip it entirely. Do not include it.

STEP 4 — BUILD TODAY'S LESSON DOCUMENT
Create a file called:
"COBOL_Day[N]_[Topic]_[YYYY-MM-DD].docx"
Save it to my Desktop.

Structure it exactly like this:

---
WHAT DAY THIS IS AND WHAT IT COVERS
One paragraph: which day, which layer, what the goal
is, what "done" looks like today. Be specific.

KEY CONCEPTS FOR TODAY
From my books/resources: only what is relevant to
today's task. No extras. No history. No trivia.
- Use tables where helpful (e.g. PIC clause types)
- Use real COBOL examples from the books
- Hard cap: 1 page of concepts max

TODAY'S PRACTICE EXERCISE
Design 1–3 exercises that match exactly what today's
curriculum task requires:
- Days 1: navigation speed drills
- Days 2–3: DATA DIVISION reading and 88-level mapping
- Days 4–6: PROCEDURE DIVISION reading exercises
- Days 7–13: full annotation exercises using the
  standard format, with blank fields for me to complete
- Day 14: review checklist for existing annotations
- Day 15: cold test instruction only, no hints

Never complete the annotation for me.
Show the COBOL block, leave the Business Rule,
Rule Type, Key Data Elements, and LLM Failure Risk
fields blank for me to fill in.

WHAT GOOD LOOKS LIKE TODAY
The exact "Done When" condition from the curriculum
in plain language. How will I know I completed
today successfully?

PRE-FILLED ANNOTATION TEMPLATE
Pre-fill one annotation log entry for today:

═══════════════════════════════════════
ANNOTATION #[N] | Date: [DATE]
Source: [leave blank]
Time taken: [leave blank]
═══════════════════════════════════════

COBOL BLOCK:
[leave blank — I will paste my snippet here]

BUSINESS RULE:
[leave blank — I will write this]

RULE TYPE:
[ ] Conditional logic
[ ] Calculation
[ ] State change
[ ] Validation
[ ] Other: ___

KEY DATA ELEMENTS:
[leave blank]

LLM FAILURE RISK: [ ] High  [ ] Medium  [ ] Low
Reason: [leave blank]

NOTES:
[leave blank]
═══════════════════════════════════════

SESSION LOG TEMPLATE (pre-filled)
Pre-fill this for me to complete after the session:

SESSION LOG — Day [N] | [Date]
Layer: [L1 / L2 / L3 / L4]
Time spent: ___ min
---
What I annotated today:
[fill in — snippet source and rule type]

What confused me:
[fill in]

Pattern I noticed:
[fill in]

LLM failure risk I assigned and why:
[fill in]

Running annotation total: ___ / 10
---

QUESTIONS TO BRING TO CLAUDE CHAT
Write 2–3 specific questions I should ask Claude
if I get stuck on today's material. Make them
specific to today's layer and task, not generic.

STEP 5 — CONFIRM
Tell me:
- Today's date and which Day number that is
- Which layer I am in
- Which files you found and used
- Filename and Desktop location of saved document
- One sentence: what I should be able to do by the
  end of today's 90-minute session
```

---

## PROMPT B — SCHEDULE SETUP
### Paste this into Cowork → Tasks ONE TIME to set up 9am automation
### Re-paste any time Cowork loses the schedule

```
SCHEDULE SETUP — DAILY COBOL TEACHING SESSION

Set up a recurring scheduled task with these parameters:

SCHEDULE:
- Time: 9:00 AM every day
- Start date: June 15, 2026
- End date: July 1, 2026 (buffer beyond 15-day curriculum)
- Days: Monday through Saturday (Sunday = rest)

TASK TO RUN EACH MORNING AT 9AM:
[paste the full PROMPT A text above here]

BEFORE RUNNING EACH SESSION:
Check if a file matching this pattern already exists
on my Desktop:
"COBOL_Day[N]_*_[today's date].docx"

If the file already exists → skip and send notification:
"COBOL Day [N] lesson already on your Desktop."

If the file does not exist → run full session and
generate the document as instructed.

NOTIFICATION WHEN DONE:
"COBOL Day [N] lesson ready on your Desktop.
90 minutes. Annotate something real."

PROGRESS LOG:
After each completed run, append one line to a file
called "COBOL_Progress_Log.txt" on my Desktop:

[DATE] | Day [N] | Layer [X] | [Topic] | Generated ✓
```

---

## QUICK REFERENCE — DAY MAP

| Day | Layer | Topic | Done When |
|-----|-------|-------|-----------|
| 1 | L1 | Navigate to DATA + PROCEDURE DIVISION in 3 programs | Under 30 seconds per file |
| 2 | L2 | Read DATA DIVISION of 3 programs, list all variables + PIC + 88-levels | 3 data maps written by hand |
| 3 | L2 | Drill 88-level conditions across 5 programs | Can translate any 88-level to VALUE instantly |
| 4 | L2+L3 | First PROCEDURE DIVISION — one IF/ELSE chain + PERFORM targets | First complete annotation in standard format |
| 5 | L3 | EVALUATE statements — 3 programs | 3 EVALUATE annotations completed |
| 6 | L3 | PERFORM chains — map full call chain across sub-paragraphs | One multi-level PERFORM chain fully mapped |
| 7 | L3+L4 | Full program read — DATA + PROCEDURE together, 2–3 annotations | Running total: 5 annotations |
| 8 | L4 | Speed drill — 2 snippets, target under 7 min each | 2 timed annotations, note slowdowns |
| 9 | L4 | Revisit 5 annotations, justify all LLM failure risk ratings | All 5 have justified risk ratings |
| 10 | L4 | COMPUTE-heavy programs — 2 calculation annotations | Running total: 7 annotations |
| 11 | L4 | Cold read — unseen program, full annotation under 10 min | One cold annotation completed |
| 12 | L4 | Nested complexity — IF inside EVALUATE inside PERFORM | One complex annotation completed |
| 13 | L4 | Annotations 9 and 10, target under 5 min each | Running total: 10 annotations |
| 14 | Review | Review all 10 annotations for accuracy + consistency | 10 clean, consistent annotations |
| 15 | ✅ | Cold test — 2 unseen programs, quality only | Ready to show Prof. Yang |

---

## ANNOTATION LOG — RUNNING TOTAL TRACKER

Update this manually as you complete annotations:

| # | Date | Source | Rule Type | LLM Risk | Time |
|---|------|--------|-----------|----------|------|
| 1 | | | | | |
| 2 | | | | | |
| 3 | | | | | |
| 4 | | | | | |
| 5 | | | | | |
| 6 | | | | | |
| 7 | | | | | |
| 8 | | | | | |
| 9 | | | | | |
| 10 | | | | | |

**Target: 10 complete annotations by Day 13.**

---

## THE 0.1% — NEVER ALLOWED

If Cowork or any resource tries to go here, skip it immediately:

- Writing COBOL
- Compiling or running COBOL
- GnuCOBOL setup of any kind
- COBOL history or mainframe architecture
- JCL (Job Control Language)
- File I/O — READ, WRITE, OPEN, CLOSE
- SORT and MERGE operations
- Report writer
- Anything that does not help read and annotate faster

---

## CONNECTION TO THESIS — NEVER FORGET THIS

Every annotation produced now is ground truth data for later.

When Prof. Yang gives the signal:
- **Your annotation** = the correct business rule
- **LLM output (JS)** = what the model produced
- **Verification** = did the JS preserve your annotated rule?
- **Your failure risk prediction** = did it match what actually happened?

The annotation log being built now is not just COBOL practice.
**It is the thesis dataset in formation.**

Flag these in every annotation — they are your primary LLM failure signal:
- 88-level conditions present → High risk
- Nested IF chains → High risk
- PERFORM chains across paragraphs → High risk
- COMPUTE with multiple variables → Medium risk
- EVALUATE with many WHEN clauses → Medium risk

---

## IF COWORK LOSES MEMORY — RECOVERY CHECKLIST

1. Open this file
2. Check the Day Map above to confirm what day you are on
3. Copy PROMPT A in full
4. Paste into Cowork → Tasks
5. Let it run — it recalculates the day automatically from June 15 as Day 1
6. If schedule is also lost: copy PROMPT B and paste it separately

**The schedule and the daily prompt are two separate tasks in Cowork.**
Never paste them together as one task.

---

## RESOURCES — EXACTLY WHAT YOU NEED, NOTHING ELSE

| Resource | What for | Where |
|----------|----------|-------|
| X-COBOL Dataset | Real COBOL snippets for annotation practice | arxiv.org/abs/2306.04892 |
| IBM COBOL Reference | Look up syntax when stuck — max 5 min per lookup | ibm.com/docs/en/cobol-zos |
| Open Mainframe COBOL Course | Weeks 1–2 structured reading if scaffolding needed | github.com/openmainframeproject/cobol-programming-course |
| COBRAIN / A-COBREX papers | Thesis context — read once, reference for patterns | arxiv.org |

**Do NOT use:**
- YouTube COBOL tutorials (too broad, too slow)
- Online COBOL compilers (you don't need to run it)
- Any resource focused on writing COBOL

---

*File: COBOL_Cowork_Master_Prompts.md*
*Project: COBOL Reading + Business Rule Annotation*
*Client: NEC via Tony | Thesis: Prof. Yang, NTUST*
*Start date: June 15, 2026*
*Last updated: June 16, 2026*
