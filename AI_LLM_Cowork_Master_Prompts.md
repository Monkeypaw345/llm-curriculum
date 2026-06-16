# AI/LLM Cowork Master Prompts
## Vu | NTUST Taipei | June 16 – June 30, 2026
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
DAILY AI/LLM TEACHING SESSION — ADAPTIVE CURRICULUM
Context file: Read the full learning plan below before doing anything.

═══════════════════════════════════════
LEARNING CONTEXT
═══════════════════════════════════════

ROLE: I am a Master's student at NTUST Taipei, final year.
Hard deadline: June 30, 2026 — internship starts July 1.

MY ONE GOAL: Close all 4 AI/LLM foundation layers and
produce one working end-to-end RAG pipeline running
locally on Ollama (Qwen2.5-coder:32b), with code pushed
to GitHub.

MY SETUP:
- Local LLM: Ollama + Qwen2.5-coder:32b + Open WebUI
- IDE: Antigravity
- Self-hosted n8n on VPS
- Python basics already in place
- Learning style: 80% doing, 20% reading. Hands-on first,
  theory second. Never passive explanation without a
  build task attached.

WHAT TO IGNORE COMPLETELY:
- LangChain or any wrapper library
- LangGraph, agents, tool use, MCP servers
- Multi-agent systems
- RAG variants (hybrid, multi-hop, re-ranking)
- Fine-tuning of any kind
- RAGAS evaluation setup
- Framework comparisons or switching tools mid-build
- Any new course, bootcamp, or video series
- Anything that does not directly help close the
  current layer

═══════════════════════════════════════
THE 4 LAYERS
═══════════════════════════════════════

LAYER 1 — How LLMs Actually Work
Deadline: June 16 | Duration: 2 days
Concepts (exactly these, nothing more):
- Token: what an LLM reads, why token limits matter
- Context window: the hard constraint, what happens
  when exceeded
- Temperature: 0 = deterministic, high = unpredictable,
  when each is useful
- System prompt vs user prompt: what each does, why
  order matters, how they interact
- Why output varies: same input, different output,
  how to control for it
Done when: Can explain all 5 concepts without notes AND
can deliberately cause each failure mode in local Ollama.

LAYER 2 — Prompt Engineering That Actually Works
Deadline: June 19 | Duration: 3 days
Skills (exactly these, nothing more):
- System prompt design: role, constraints, output format
- Few-shot examples: showing beats describing
- Chain of thought: reason before answering
- Structured output: consistent JSON reliably
- Iteration discipline: change ONE variable per iteration
Test bed task: Extract a business rule from text as JSON
with keys: rule_description, condition, action, edge_cases
Done when: Logged prompt iteration file with minimum 5
versions, each with ONE variable changed, final prompt
produces consistent JSON 4/5 runs on novel inputs.

LAYER 3 — Building With the API in Python
Deadline: June 21 | Duration: 2 days
Skills (exactly these, nothing more):
- Call Ollama API in Python (10 lines)
- Pass system prompt + user message
- Maintain conversation history as message list
- Parse response and use it
- Handle errors with try/except — no crashes
Core pattern to write from memory:

  import requests

  def chat(messages, system_prompt):
      response = requests.post(
          "http://localhost:11434/api/chat",
          json={
              "model": "qwen2.5-coder:32b",
              "messages": [{"role": "system",
                "content": system_prompt}] + messages,
              "stream": False
          }
      )
      return response.json()["message"]["content"]

  history = []
  while True:
      user_input = input("You: ")
      history.append({"role": "user",
        "content": user_input})
      reply = chat(history, "You are a helpful assistant.")
      history.append({"role": "assistant",
        "content": reply})
      print(f"AI: {reply}")

Done when: Script rewritten from memory, runs clean,
handles 3 turns, handles bad API call gracefully,
pushed to GitHub.

LAYER 4 — RAG End to End
Deadline: June 30 | Duration: 8 days
The RAG loop:
  Document → chunk → embed → store in ChromaDB
                                      ↓
  User question → embed → retrieve top-K chunks
                                      ↓
               chunks + question → Ollama → answer

Skills (exactly these, nothing more):
- Chunking: ~300 word chunks, 50-word overlap
- Embedding: sentence-transformers, semantic similarity
- ChromaDB: local vector store, query by similarity
- Retrieval: embed question, find similar chunks
- Generation: retrieved chunks as context → Ollama
- Stress testing: 10 questions, log failures by type:
  retrieval failure / generation failure / chunking
  failure

Tools — exactly these, nothing else:
- Python
- ChromaDB (local)
- sentence-transformers
- Ollama + Qwen2.5-coder:32b
- GitHub

Test document: A PDF from the thesis domain — COBRAIN
paper or any COBOL-related research paper.

Done when: Pipeline answers 8/10 test questions,
failures diagnosed by type, refactored into clean
functions, README written, pushed to GitHub.

═══════════════════════════════════════
THE 15-DAY PLAN
═══════════════════════════════════════

Day 1  | Jun 16 | L1 | Read Anthropic prompting docs
  (30 min cap). Run 10 deliberate Ollama experiments:
  no system prompt, temperature 1.0, temperature 0,
  context overflow. Observe and note what changes.
  Done when: Each experiment described in own words,
  written down.

Day 2  | Jun 17 | L1 | Close all tabs. Write one-page
  explanation of all 5 L1 concepts from memory.
  Check against docs.
  Done when: Accurate with no major gaps. L1 closed.

Day 3  | Jun 18 | L2 | Pick test bed task. Write 3
  different system prompts. Run each 3 times. Log all
  9 outputs.
  Done when: 9 logged outputs, can identify most
  consistent prompt and why.

Day 4  | Jun 19 | L2 | Add few-shot examples to best
  prompt from Day 3. Add chain-of-thought instruction.
  Compare results.
  Done when: Concrete evidence few-shot + CoT improved
  output quality or consistency.

Day 5  | Jun 20 | L2 | Stress test best prompt on 5
  novel inputs. Log failures. Diagnose each. One
  targeted fix per failure.
  Done when: Works on 4/5 novel inputs. Failures
  diagnosed not just observed. L2 closed.

Day 6  | Jun 21 | L3 | Read Ollama Python API docs
  (20 min max). Write script: user input → API call →
  parse response → print. Add conversation history loop.
  Done when: Script runs, live input, history across
  3 turns.

Day 7  | Jun 22 | L3 | Close all references. Rewrite
  script from memory in a new file. Add try/except for
  failed API call. Push to GitHub.
  Done when: From memory, runs clean, error handled,
  on GitHub. L3 closed.

Day 8  | Jun 23 | L4 | Read one RAG explainer (30 min
  cap). Draw the RAG loop on paper. Understand what
  ChromaDB is and why.
  Done when: Can draw and explain full loop from memory.

Day 9  | Jun 24 | L4 | Install ChromaDB +
  sentence-transformers. Write script: read test
  document, chunk into ~300 words with 50-word overlap,
  embed, store in Chroma.
  Done when: Chroma collection exists with all chunks
  embedded. Print chunk count to confirm.

Day 10 | Jun 25 | L4 | Write retrieve() function:
  embed user question, query Chroma top 3, return
  chunks. Test with 5 questions manually.
  Done when: Returns sensible chunks for 4/5 questions.
  Know why 5th failed.

Day 11 | Jun 26 | L4 | Connect retrieval to generation.
  Full pipeline: question → retrieve → format as
  context → Ollama → print answer + source chunk.
  Run end-to-end on 3 questions.
  Done when: Runs without errors, grounded answer
  for 2/3 questions.

Day 12 | Jun 27 | L4 | Stress test: 10 questions.
  Log every result. Categorize failures: retrieval /
  generation / chunking.
  Done when: Logged table of 10 results, can name
  primary failure mode.

Day 13 | Jun 28 | L4 | Fix the most common failure
  mode from Day 12. ONE fix only. Re-run same 10
  questions.
  Done when: Pipeline answers 8/10 correctly. If not,
  document why the fix wasn't enough.

Day 14 | Jun 29 | L4 | Refactor into clean functions:
  load_and_chunk(), embed_and_store(), retrieve(),
  generate(). Write README. Push final version to GitHub.
  Done when: Someone else could clone and run following
  only the README.

Day 15 | Jun 30 | Checkpoint | Close all references.
  Explain all 4 layers without notes. Run RAG pipeline
  from scratch. Write one-page reflection.
  Done when: All 4 layers explainable. Code on GitHub.
  Reflection written. Ready for July 1.

═══════════════════════════════════════
SESSION STRUCTURE — 75 MIN/DAY
═══════════════════════════════════════

0–15 min  | One concept only. Hard stop at 15 min.
15–65 min | Build something that runs. Even if ugly.
65–75 min | Session log: what you built, what broke,
            what failure type. One paragraph. Push
            to GitHub.

═══════════════════════════════════════
YOUR TASK RIGHT NOW
═══════════════════════════════════════

STEP 1 — FIND TODAY'S DAY NUMBER
Check today's date. Count from June 16, 2026 as Day 1.
Today is Day [N]. Identify which layer and task from
the plan above.

STEP 2 — SCAN MY AI/LLM BOOKS AND RESOURCES
Search these folders for any PDF or ebook files related
to: LLMs, machine learning, Python, RAG, embeddings,
vector databases, prompt engineering, ChromaDB,
sentence-transformers, Ollama, transformers.
Check: Desktop, Documents, Downloads, and any folder
named "AI", "LLM", "ML", "Books", "Programming",
"Python", or "Reference".
List every relevant file you find before proceeding.

STEP 3 — APPLY THE CHAPTER 7 FILTER
Before extracting anything, ask:
"Does this content help close Layer [N] specifically?"
If yes → extract it.
If no → skip it entirely. Do not include it.

STEP 4 — BUILD TODAY'S LESSON DOCUMENT
Create a file called:
"LLM_Day[N]_[Topic]_[YYYY-MM-DD].docx"
Save it to my Desktop.

Structure it exactly like this:

---
WHAT DAY THIS IS AND WHAT IT COVERS
One paragraph: which day, which layer, what the goal
is, what "done" looks like today. Be specific.

KEY CONCEPTS FOR TODAY
From my books/resources: only what is relevant to
today's task. No extras.
- Use tables where helpful
- Use code blocks for any Python patterns
- Use real examples from the books where possible
- Hard cap: 1 page of concepts max. I learn by doing,
  not by reading.

TODAY'S BUILD TASK
Design the exact hands-on task for today based on
the curriculum. Be specific:
- Days 1-2: Ollama experiments to run, what to observe,
  where to write observations
- Days 3-5: Prompt versions to write, log template
  to fill, what to compare
- Days 6-7: Code structure to build, what each
  function should do, leave blanks for me to fill in
- Days 8-15: RAG component to build, exact function
  signature, expected output to verify it works

Never give complete working code. Give the shape
and leave the key pieces for me to fill in.
Ask me what I think goes in the blank BEFORE
revealing the answer.

WHAT GOOD LOOKS LIKE TODAY
The exact "Done When" condition from the curriculum
in plain language. How will I know I completed
today successfully?

SESSION LOG TEMPLATE (pre-filled)
Pre-fill this for Vu to complete after the session:

SESSION LOG — Day [N] | [Date]
Layer: [L1 / L2 / L3 / L4]
Time spent: ___ min
---
What I built today:
[fill in — what runs, not what I read]

What broke and why:
[fill in]

Failure type (if any):
[ ] Concept misunderstanding
[ ] Python error
[ ] API error
[ ] Retrieval failure
[ ] Generation failure
[ ] Chunking failure
[ ] Other: ___

Did I touch the 0.1%?
[ ] No
[ ] Yes — what was it: ___

GitHub push: [ ] Done  [ ] Not yet — reason: ___

One thing to bring to Claude Chat if stuck:
[fill in]
---

QUESTIONS TO BRING TO CLAUDE CHAT
Write 2-3 specific questions I should ask Claude
if I get stuck today. Make them specific to today's
layer and build task, not generic.

STEP 5 — CONFIRM
Tell me:
- Today's date and which Day number that is
- Which layer I am in
- Which files you found and used
- Filename and Desktop location of saved document
- One sentence: what I should have built or produced
  by the end of today's 75-minute session
```

---

## PROMPT B — SCHEDULE SETUP
### Paste this into Cowork → Tasks ONE TIME to set up 9am automation
### Re-paste any time Cowork loses the schedule

```
SCHEDULE SETUP — DAILY AI/LLM TEACHING SESSION

Set up a recurring scheduled task with these parameters:

SCHEDULE:
- Time: 9:00 AM every day
- Start date: June 16, 2026
- End date: July 1, 2026
- Days: Monday through Saturday (Sunday = rest)

TASK TO RUN EACH MORNING AT 9AM:
[paste the full PROMPT A text above here]

BEFORE RUNNING EACH SESSION:
Check if a file matching this pattern already exists
on my Desktop:
"LLM_Day[N]_*_[today's date].docx"

If the file already exists → skip and send notification:
"AI/LLM Day [N] lesson already on your Desktop."

If the file does not exist → run full session and
generate the document as instructed.

NOTIFICATION WHEN DONE:
"AI/LLM Day [N] lesson ready on your Desktop.
75 minutes. Build something that runs."

PROGRESS LOG:
After each completed run, append one line to a file
called "LLM_Progress_Log.txt" on my Desktop:

[DATE] | Day [N] | Layer [X] | [Topic] | Generated ✓
```

---

## QUICK REFERENCE — DAY MAP

| Day | Date | Layer | Topic | Done When |
|-----|------|-------|-------|-----------|
| 1 | Jun 16 | L1 | LLM experiments — break things in Ollama | 10 experiments observed and written down |
| 2 | Jun 17 | L1 | Write all 5 L1 concepts from memory | Accurate, no gaps. L1 closed. |
| 3 | Jun 18 | L2 | 3 system prompts × 3 runs = 9 logged outputs | Know which prompt is most consistent and why |
| 4 | Jun 19 | L2 | Add few-shot + CoT to best prompt | Concrete evidence of improvement |
| 5 | Jun 20 | L2 | Stress test on 5 novel inputs, diagnose failures | Works 4/5. L2 closed. |
| 6 | Jun 21 | L3 | Write Ollama API script with history loop | Runs, takes input, 3-turn history |
| 7 | Jun 22 | L3 | Rewrite from memory + try/except + GitHub push | From memory, clean, on GitHub. L3 closed. |
| 8 | Jun 23 | L4 | Read RAG explainer, draw loop on paper | Can draw and explain loop from memory |
| 9 | Jun 24 | L4 | Chunk + embed + store in ChromaDB | Chroma collection exists, chunk count printed |
| 10 | Jun 25 | L4 | Write retrieve() function, test 5 questions | Sensible chunks returned for 4/5 |
| 11 | Jun 26 | L4 | Connect retrieval → generation, run 3 questions | Pipeline runs end-to-end, 2/3 grounded answers |
| 12 | Jun 27 | L4 | Stress test 10 questions, categorize failures | Logged table, primary failure mode named |
| 13 | Jun 28 | L4 | Fix primary failure mode, re-run 10 questions | 8/10 correct |
| 14 | Jun 29 | L4 | Refactor + README + GitHub final push | Someone else can clone and run it |
| 15 | Jun 30 | ✅ | Explain all 4 layers cold, run pipeline, write reflection | Ready for July 1 |

---

## THE 0.1% — NEVER ALLOWED

If Cowork or any resource tries to go here, close it immediately:

- LangChain or any LLM wrapper
- LangGraph, agents, tool use, MCP servers
- Multi-agent systems
- RAG variants (hybrid, multi-hop, re-ranking)
- Fine-tuning of any kind
- RAGAS or evaluation frameworks
- Framework comparisons
- Any new course, bootcamp, or video series
- Invoice extractor or any artifact build (September)

---

## IF COWORK LOSES MEMORY — RECOVERY CHECKLIST

1. Open this file
2. Check the Day Map above to confirm what day you are on
3. Copy PROMPT A in full
4. Paste into Cowork → Tasks
5. Let it run — it recalculates the day automatically from today's date
6. If schedule is also lost: copy PROMPT B and paste it separately

**The schedule and the daily prompt are two separate tasks in Cowork.**
Never paste them together as one task.

---

*File: AI_LLM_Cowork_Master_Prompts.md*
*Project: AI/LLM Foundation Learning*
*Hard deadline: June 30, 2026*
*Internship starts: July 1, 2026*
*Last updated: June 16, 2026*
