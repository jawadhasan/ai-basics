## What makes a prompt effective

- Clarity: Say exactly what you mean
- Cotext: Give relavent background information
- Structure: Organize your request

---

## Prompt Elements

- Task: What claude should do.
- Instructions: How it should do it.
- Context: What it need to know

Use **Project** when it seems we are repeating above prompt.

## Project

A project is a dedicated workspace with three core elements.

- Knowledge base - persistent knowledge-base for our documents pdf, csv etc.
- custom instructions - guides claude behavior in every chat.
- Conversations - shared conversation space, that keeps related work togather.

---

## Claude Code Use Cases

### Code/File Analysis

- New Codebase - Ask Claude to explain the architecture.
- Code reviews - Ask Claude to trace the impact of a change across the system.
- Debugging - Ask Claude to follow data through the system to find when things go wrong.


### Full Stack Features

- Reference existing patterns with @ 

e.g. "Follow the pattern in @existingFile.ts" helps Claude match your codebase’s style

- Be specific about your needs - 

Listing out the components - route, controller, service, types  helps Claude create a complete solution.

- Review Changes - Claude can make mistakes

