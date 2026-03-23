---
name: project-navigator
description: >
  Navigate, search, and reuse work from past conversations and projects with this user.
  Use this skill whenever the user references a past project, asks to find something from
  a previous chat, wants to continue or build on earlier work, asks you to follow the same
  approach/template/structure from a past project, or when you detect that the current task
  overlaps with an active project you've worked on together before.

  Trigger on phrases like: "remember when we...", "that project we did", "do it like we did
  for...", "find the...", "what did we decide about...", "pull up...", "follow the same
  approach", "use the same template", "like the [project name] one", "continue from where
  we left off", "summarize our work on...", "what's the status of...", or any reference to
  a named project from past conversations.

  Also trigger PROACTIVELY when the user starts a task that clearly relates to an active
  project — don't wait to be asked. For older/inactive projects, only search when explicitly
  requested.
---

# Project Navigator

A skill for searching, retrieving, connecting, and replicating work across past conversations and projects.

## Core Capabilities

This skill enables five modes of operation:

### 1. Decision Finder
Find specific decisions, names, structures, or plans from past work.

### 2. Output Retriever
Locate files, documents, drafts, or deliverables created together.

### 3. Evolution Tracker
Trace how an idea developed across multiple conversations — show the arc.

### 4. Project Summarizer
Give a comprehensive status report on everything done for a specific project.

### 5. Pattern Replicator
Extract the *method, structure, or approach* from a past project and apply it as a template to new work. This is not just copying content — it's replicating the workflow, the logic, the format, or the creative process.

---

## How to Operate

### Step 1: Identify the Mode

Based on the user's request (or proactive detection), determine which mode applies. Multiple modes can combine — e.g., the user might want a project summary (Mode 4) that also extracts a reusable template (Mode 5).

### Step 2: Search Strategy

Use the `conversation_search` and `recent_chats` tools aggressively. Do not rely solely on memory — always search.

**Search approach by mode:**

| Mode | Search Strategy |
|------|----------------|
| Decision Finder | Search with the specific topic/keyword. Try 2-3 query variations if first results are thin. |
| Output Retriever | Search with project name + output type (e.g., "marketing plan draft", "logo concepts"). Also check `/mnt/user-data/uploads/` for any related files. |
| Evolution Tracker | Run multiple searches across different phases of the topic. Use `recent_chats` with date ranges if the user gives time hints. Reconstruct the timeline. |
| Project Summarizer | Search with the project name, then follow threads. Use `recent_chats` to scan broadly. Compile: decisions made, outputs created, open questions, next steps. |
| Pattern Replicator | Search for the reference project. Extract: the structure used, the sequence of steps, the format of outputs, the creative/logical approach. Then present it as a reusable template before applying it to the new task. |

**Query construction rules:**
- Use substantive keywords only — project names, topic nouns, specific terms
- If the user works in multiple languages, try query variants in each language
- If first search is thin, broaden or try synonyms
- For evolution tracking, search in chronological order using date filters

### Step 3: Synthesize and Present

**For Decision Finder:**
State the decision clearly and directly. Include the context of when/why it was made. Link to the source conversation.

**For Output Retriever:**
Describe what was created, its current state, and provide the conversation link. If it was a file, note whether it can be recreated or if the user needs to re-upload it (since files don't persist across sessions).

**For Evolution Tracker:**
Present a timeline view:
```
[Date/Chat 1] → Initial idea: ...
[Date/Chat 2] → Refined to: ...
[Date/Chat 3] → Final version: ...
```
Include links to each conversation.

**For Project Summarizer:**
Use this structure:
- **Project**: Name
- **Status**: Active / Paused / Completed
- **Key Decisions**: Bullet the important ones
- **Outputs Created**: What was produced
- **Open Questions**: Unresolved items
- **Suggested Next Steps**: Based on where things left off

**For Pattern Replicator:**
First, present the extracted pattern/template explicitly:
```
Template extracted from [Project Name]:
1. Step/element one
2. Step/element two
3. ...
```
Then ask the user to confirm before applying it to the new task. This ensures the pattern is correct before replication begins.

---

## Proactive Behavior

For **active projects** (projects discussed in the last ~2 weeks or that the user has flagged as ongoing), proactively:
- Connect current work to relevant past decisions
- Flag if the current task contradicts or duplicates something already done
- Suggest reusing a past approach when a similar task comes up

For **older/inactive projects**, only search when the user explicitly asks.

### Discovering Active Projects
Do NOT maintain a hardcoded list of projects. Instead, dynamically discover active projects by:
1. Using `recent_chats` to scan the last ~2 weeks of conversations
2. Identifying recurring project names, topics, or threads
3. Using memory (if available) to note any projects the user has flagged as ongoing

This keeps the skill general-purpose and adapts to any user's workflow automatically.

---

## Important Rules

1. **Always search before answering.** Never rely on memory alone when this skill triggers. Run at least one `conversation_search` or `recent_chats` call.

2. **Show your sources.** Always link back to the conversations you're pulling from so the user can verify and revisit.

3. **Respect the user's voice.** When replicating patterns, maintain the user's style and creative approach — don't sanitize or over-formalize their work.

4. **Handle gaps honestly.** If a search turns up incomplete info, say so clearly. Mark gaps rather than filling them with assumptions.

5. **Multilingual awareness.** If the user works in multiple languages, search in all relevant languages. Present in whichever language the user is currently using, but preserve original terms and names as-is.

6. **Files don't persist.** Remind the user (when relevant) that files from past sessions aren't available unless re-uploaded. Offer to recreate them if the conversation history has enough detail.

7. **Template confirmation.** When using Pattern Replicator mode, always show the extracted template and get confirmation before applying it. The user should validate that you captured the right approach.
