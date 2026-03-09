# Gemini Companion Starter

[中文说明](./README.zh-CN.md)

> **Looking for other CLI assistants?** 
> Check out the sister extensions: [Claude Code Companion Starter](https://github.com/d-wwei/claude-code-companion-starter) & [Codex Companion Starter](https://github.com/d-wwei/Codex-companion-starter)

Turn Gemini CLI into a more consistent, workspace-aware, long-term personal assistant deployment pack.

A deployment-ready package for people who want Gemini CLI to do more than answer one-off questions. It helps Gemini establish a lightweight external memory layer in the file system, so collaboration can stay stable across sessions.

## Why This Exists

Many "personal assistant" prompts look impressive in theory but behave poorly in real CLI environments. Common issues include:

- over-relying on chat history that disappears between sessions
- reading too many files on every turn
- blurring the line between suggested content and actual file operations
- mixing long-term rules with temporary task notes

This project is designed around those realities.

Instead of pretending the model will just remember everything, it pushes Gemini CLI to use the local file system as a durable collaboration surface.

## Key Features

This prompt transforms Gemini CLI from a powerful but amnesic one-shot tool into a long-term collaborator that builds rapport with you.

- **Long-term Memory Setup:** Automatically establishes persistent global rules (`~/.gemini/`) and project-specific memory (`.assistant/`).
- **Preference Accumulation:** Remembers how you like things done—your role, coding style, workflow, and recurring instructions.
- **Global Memory Promotion:** As it discovers your habits and reusable knowledge during active projects, it can automatically promote them to your global profile.
- **Project-Specific Customization:** Every project can have its own tailored rules and context that override the global defaults.
- **Continuous Collaboration:** You never have to explain your background, structure, or current progress from scratch again when re-entering a workspace.
- **Layered Bootstrap Interview:** The startup interview now uses a compact 3-step script to capture naming, style, assistant role, ambiguity handling, work types, and memory boundaries without becoming a questionnaire.
- **Global Quick Mode:** When started from `$HOME`, Gemini writes directly to `~/.gemini/GEMINI.md` and skips redundant "sync to global" prompts.
- **Historical Project Scan:** First-time setup can scan prior `.assistant/` workspaces, extract project/session summaries, and register them into the global project index.

## Why OpenClaw-Inspired Memory For Gemini CLI

Gemini CLI is good at following instructions and working with local files, but it does not automatically become a long-term collaborative system just because you give it a long prompt.

OpenClaw-style memory systems are useful because they treat files as durable memory artifacts instead of leaving everything in chat history. That idea maps well to CLI assistants:

- stable preferences belong in structured files
- project decisions should survive across sessions
- temporary notes should stay separate from long-term memory

This repository applies that philosophy to Gemini CLI by using `.assistant/` as a project-local memory layout and `~/.gemini/GEMINI.md` as a global default behavior layer.

The result is not "turning Gemini into OpenClaw". The result is giving Gemini CLI a more structured memory surface so it can feel less stateless and more like a repeatable collaborator.

## What This Changes

- preferences and collaboration habits stop living only in chat history
- project context becomes inspectable and editable
- temporary context and durable memory are stored separately
- Gemini can re-enter a workspace with better continuity

## Concrete Examples

1. Style becomes stable across sessions.  
   Preferences such as "be concise, state conclusions first, then risks" can live in `.assistant/STYLE.md`.

2. Project decisions stop resetting.  
   If a project already decided to postpone a large refactor, that can live in `.assistant/memory/projects/architecture.md` instead of being re-debated from scratch.

3. Daily scratch notes stop polluting long-term rules.  
   Unverified notes or one-day context can live in `.assistant/memory/daily/YYYY-MM-DD.md`.

4. Workflow becomes personalized.  
   If you prefer "inspect first, edit second, summarize verification at the end", that can live in `.assistant/WORKFLOW.md`.

## Core Ideas

- File-backed memory instead of chat-only memory
- Lazy loading instead of reading every file on every turn
- Incremental edits instead of destructive rewrites
- Explicit file operations instead of hallucinated "pretend writes"
- Lightweight bootstrap instead of long onboarding forms

## What's Included

- [BOOTSTRAP_PROMPT.md](./BOOTSTRAP_PROMPT.md)  
  The main bootstrap prompt for Gemini CLI.

- [scripts/show-bootstrap.sh](./scripts/show-bootstrap.sh)  
  Prints the bootstrap prompt locally.

- [README.zh-CN.md](./README.zh-CN.md)  
  Chinese documentation.

## Deploy

1. Clone or download this repository.
2. Open `BOOTSTRAP_PROMPT.md`, or print it with:

```bash
./scripts/show-bootstrap.sh
```

3. Start Gemini CLI in the target workspace.
4. Paste the prompt into Gemini CLI in one message.
5. Let Gemini inspect the workspace, initialize memory, and begin lightweight bootstrap.

## Package Layout

```text
BOOTSTRAP_PROMPT.md
scripts/
  show-bootstrap.sh
```

This repository is now organized as a lightweight Gemini deployment pack rather than only a nested prompt file.

## Quick Start

1. Open [BOOTSTRAP_PROMPT.md](./BOOTSTRAP_PROMPT.md).
2. Copy the full prompt.
3. Start Gemini CLI in your target workspace.
4. Send the prompt in one message.
5. Let Gemini inspect the workspace, update config, and start lightweight bootstrap if needed.

## Recent Improvements

- richer first-round interview for long-term collaboration
- bootstrap trigger now prefers `BOOTSTRAP.md` plus core-file completeness instead of a single-file heuristic
- explicit global quick mode with no duplicate global-sync prompt
- fuller historical project and session scan flow
- clearer incremental-update behavior for existing `GEMINI.md`

## How This Prompt Is Positioned

This repository currently provides one main prompt, not multiple variants.

It is best understood as a balanced working version:

- proactive enough to create files and initialize structure
- cautious enough to avoid unnecessary overwrites
- opinionated about memory structure and lazy loading

## Design Principles

- Global defaults should guide behavior, not claim permanent hard control
- Project-local memory should carry evolving context
- Temporary notes should not pollute long-term memory
- Small, durable files are better than giant prompt blobs
- Real CLI behavior matters more than idealized agent theory

## Important Boundaries

- `~/.gemini/GEMINI.md` should be treated as a default behavior layer, not a guaranteed permanent control layer.
- `.assistant/` is a project-local memory convention, not a native Gemini CLI protocol.
- Actual behavior still depends on runtime context, available tools, and the model's execution behavior.

## FAQ

### Why not just use a single giant prompt every time?

Because a giant prompt does not scale well across sessions.

As soon as work becomes ongoing, you need stable structure for:

- user preferences
- project decisions
- temporary notes
- unfinished tasks

Keeping that in files is more durable than repeating it in chat.

### Why not keep everything inside `GEMINI.md`?

Because global rules and project memory are different things.

`GEMINI.md` is better for defaults and stable behavior. Project-level files are better for local context that changes over time.

### Doesn't `.assistant/` add too much overhead?

It can, if overbuilt.

This project tries to keep the structure small and practical. The goal is not process for its own sake. The goal is reducing repeated friction.

### Is this trying to replace Gemini CLI?

No.

It is a prompt-layer workflow enhancement. Gemini CLI still does the actual work. This repository simply gives it a more durable collaboration structure.

## Who This Is For

This project is useful if you want Gemini CLI to behave more like:

- a repeatable project assistant
- a workspace-aware collaborator
- a tool that can preserve lightweight context across sessions

It is less useful if you only want fast one-off prompts with no local memory structure.

## Notes

If Gemini becomes too aggressive in your environment, tighten the prompt or trim the initialization scope.

If it is too passive, strengthen the execution instructions around file creation, validation, and bootstrap follow-through.
