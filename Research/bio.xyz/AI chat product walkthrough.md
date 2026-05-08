# AI Chat Product Walkthrough

Date: 2026-05-08
Source videos:
- `/Users/admin/Desktop/Screen Recording 2026-05-07 at 5.54.15 PM.mov`
- `/Users/admin/Desktop/Screen Recording 2026-05-07 at 11.44.18 PM.mov`
Product URL: https://chat.bio.xyz/

## Product Summary

Based on the recordings, `chat.bio.xyz` works like an AI research workspace, not just a simple chatbot.

The product helps users start or continue a research thread, submit a scientific or technical research query, let the AI run a multi-step research process, and inspect structured outputs such as objectives, hypotheses, rationales, literature, and analyses.

## Main Product Flow

1. Start or select a research thread.

   The left sidebar includes `New Research`, search, shared research, research center, generated papers, projects, and a history of prior research threads. Each thread is organized like a project artifact.

2. Enter a research query.

   In the main chat area, the user asks a scientific or research question. Examples shown in the recordings include:

   - `Summarize the notebook cell-by-cell in plain language`
   - `Compare the mechanisms of neuroplasticity in biological brains with weight updates in artificial neural networks. What insights from neuroscience remain unexploited in modern AI architectures?`

3. The system runs a multi-step research process.

   The UI shows progress such as `Researching...`, step counters, and status labels like `Step 1`, `Step 2`, `Analyzing data`, and `Viewing`.

   In the notebook example, the system traces work such as ingesting notebook metadata and reading the notebook cell list.

4. The center panel becomes the generated answer.

   Once enough analysis is done, the central pane fills with a structured response: summaries, paragraphs, evidence-backed reasoning, and follow-up-ready explanations.

5. The right panel acts as the research state panel.

   The right side shows tabs such as `Overview`, `Literature`, `Analysis 1`, and `Analysis 2`. It captures the current research state, including objective, hypothesis, rationale, novelty statement, and detailed analytical outputs.

6. The system builds hypotheses, not only answers.

   The product appears to convert the user's question and uploaded or contextual material into a formal research hypothesis, then explains why that hypothesis is plausible.

7. The workflow supports continuation.

   The second recording shows a completed research session with a prompt to continue or auto-continue the task. The product is designed for iterative research: ask, analyze, generate an overview, inspect supporting analysis, then continue with follow-up questions.

## Right Panel Tabs Explained With 5W1H

The right panel turns the chat from a one-off answer into a traceable research workflow.

### Overview

| 5W1H | Explanation |
|---|---|
| What | Shows the current research framing: objective, current objective, hypothesis, rationale, novelty statement, and sometimes next research direction. |
| Who | For the end-user, reviewer, principal investigator, scientist, analyst, or anyone who needs to understand the reasoning without reading the whole chat. |
| When | Useful during and after AI generation, especially when the user wants to check whether the AI understood the task correctly. |
| Where | In the right-side panel, separate from the main chat answer. |
| Why | Gives a concise control summary of the research. The user can quickly see what the AI is trying to prove, what assumption it is making, and why the result matters. |
| How | The AI extracts the user query, uploaded files or notebooks, and generated reasoning, then summarizes them into structured research fields. |

End-user value: the main chat may be long. `Overview` gives the research thesis in a compact, reusable form.

### Literature

| 5W1H | Explanation |
|---|---|
| What | Shows literature-based support: relevant papers, external findings, prior work, citations, or summarized scientific context. |
| Who | For users who need evidence, not just an AI-generated claim. This includes researchers, students, analysts, and paper writers. |
| When | Useful when validating a claim, preparing a paper, checking novelty, or comparing the AI's answer against existing research. |
| Where | In the right-side tab area, usually next to `Overview` and `Analysis`. |
| Why | Answers whether the research is grounded in existing knowledge, and what prior work supports or contradicts it. |
| How | The system likely searches, reads, or summarizes relevant literature, then connects those findings back to the current research question. |

End-user value: `Literature` prevents the product from feeling like a black-box chatbot. It gives evidence and research context.

### Analysis

| 5W1H | Explanation |
|---|---|
| What | Shows deeper reasoning or task-specific investigation. The videos show tabs like `Analysis 1` and `Analysis 2`, suggesting multiple analysis runs or sub-analyses. |
| Who | For users who want to inspect how the AI reached its conclusion, such as data scientists, researchers, technical users, or reviewers. |
| When | Useful after the AI generates an answer, or while it is processing uploaded data or notebooks. |
| Where | In the right-side tab area, beside `Overview` and `Literature`. |
| Why | Explains the reasoning path: what was inspected, what patterns were found, what assumptions were made, and what conclusions follow. |
| How | The system breaks the research task into analytical steps, such as reading notebook cells, comparing methods, evaluating hypotheses, or extracting methodological insights. |

End-user value: `Analysis` is the audit trail. It helps users trust, debug, or refine the AI's answer.

## Simple Mental Model

- `Overview` = What is the research claim?
- `Literature` = What evidence from prior work supports it?
- `Analysis` = How did the AI reason through the data or task?

Together, these tabs help the end-user move from `AI gave me an answer` to `I understand the objective, evidence, reasoning, and research value behind this answer`.
