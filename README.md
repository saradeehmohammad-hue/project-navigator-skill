# Project Navigator — Claude Skill

**Navigate, search, and reuse work across your entire conversation history with Claude.**

Most Claude skills help you *do* things — write code, create documents, analyze data. This one helps Claude **remember how you work** and replicate it.

---

## The Problem

If you use Claude across multiple ongoing projects, you've probably hit this wall:

- "We decided on a name for this three weeks ago... what was it?"
- "We built a Terms of Reference together last month — can you follow the same structure for this new one?"
- "What's the current status of everything we've done on Project X?"

Claude's memory helps with bits and pieces, but it doesn't give you structured retrieval across projects, and it definitely doesn't extract *reusable patterns* from past work.

## What This Skill Does

Project Navigator gives Claude **five modes** for working with your conversation history:

### 1. Decision Finder
Pull up specific choices you made together — names, structures, plans, directions.

> *"What did we decide to call the production company?"*

### 2. Output Retriever
Locate files, drafts, and deliverables you created in past sessions.

> *"Find the script outline we wrote for the documentary."*

### 3. Evolution Tracker
Trace how an idea developed across multiple conversations, displayed as a timeline.

> *"Show me how the product concept evolved from the first chat to now."*

### 4. Project Summarizer
Get a full status report: decisions made, outputs created, open questions, next steps.

> *"Summarize everything we've done on the website redesign project."*

### 5. Pattern Replicator ⭐
This is the one nobody else is doing. Claude extracts the **method, structure, or creative approach** from a past project and presents it as a reusable template — then applies it to new work after you confirm.

> *"I need a new Terms of Reference. Follow the same approach we used for the last one."*

> *"Build me a campaign plan using the same structure as the one we did last month."*

---

## Who Is This For?

- **Freelancers and creators** juggling multiple ongoing projects with Claude
- **Educators and trainers** who build curricula and programs iteratively
- **Media professionals** managing productions, scripts, and campaigns across sessions
- **Anyone** who uses Claude as a long-term creative partner, not just a one-off tool

If you've ever wished Claude could "learn from how we did it last time," this is for you.

---

## Installation

### Claude.ai (Pro, Max, Team, Enterprise)

1. Download the `project-navigator.skill` file from the [Releases](../../releases) page
2. Go to **Settings → Customize → Skills**
3. Upload the `.skill` file
4. Done — Claude will automatically use it when relevant

### Manual Installation

1. Clone this repo or download the `SKILL.md` file
2. Place it in your skills directory:
   ```
   ~/.claude/skills/project-navigator/SKILL.md
   ```

---

## How It Works

The skill uses Claude's built-in `conversation_search` and `recent_chats` tools to search your past conversations. It doesn't store anything externally — all data stays within your Claude account.

When the skill triggers, Claude:
1. Identifies which mode fits your request
2. Runs targeted searches across your conversation history (in both English and Arabic if relevant)
3. Synthesizes what it finds into a structured response
4. For Pattern Replicator mode: presents the extracted template for your confirmation before applying it

### Proactive vs. On-Demand

- **Active projects** (recent ~2 weeks): Claude proactively connects current work to past decisions
- **Older projects**: Claude only searches when you explicitly ask

---

## Examples

```
You: "Do it like we did for the marketing campaign"
Claude: [Searches past chats] → Extracts the campaign structure → Shows you the template → Applies it after confirmation

You: "What's the status of the website redesign project?"  
Claude: [Searches past chats] → Returns: key decisions, outputs created, open questions, suggested next steps

You: "We picked a name for the company, what was it?"
Claude: [Searches past chats] → States the decision directly with context and link
```

---

## Limitations

- **File persistence**: Files created in past sessions don't carry over. Claude can offer to recreate them if conversation history has enough detail.
- **Search depth**: Relies on Claude's `conversation_search` and `recent_chats` tools, which may not surface every past conversation. Multiple search queries help.
- **Not a database**: This skill makes Claude smarter about using its existing tools — it doesn't add external storage or indexing.

---

## Contributing

Found a way to improve it? PRs welcome. Some ideas:

- Additional modes (e.g., "Conflict Detector" — flag when current work contradicts a past decision)
- Better search strategies for specific project types
- Localization for other languages

---

## License

MIT — use it, modify it, share it.

---

## Credits

Created by **Mohammad Saradeeh (Joe)**.

Built for anyone who uses Claude as a long-term creative partner and got tired of repeating themselves.
