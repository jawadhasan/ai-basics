## What makes a prompt effective

- Clarity: Say exactly what you mean
- Cotext: Give relavent background information
- Structure: Organize your request

## Role-Task-Context-Format (RTCF) Framework

RTCF gives reusable structure for building effective prompts.

RTCF is a starting point, not the finish line.

- Role: Who
- Task: What (Core of prompt)
- Context: Why (provides background info)
- Format: How (format to structure output)

## RTCF Example

Role: You are an expierienced business analyst skilled at clear communication.

Task: Create a meeting summary from my notes that captures key decisions,  action items and open questions.

Context: This is a 45-minute stakeholder meeting about a new inventory system. Here are my notes....

Format: Structure with sections: key decisions, action items, open questions, next steps, use bullet points, under 300 words


## Refine Your Pormpt

RTCF gets us solid results. May be response is good, but you wants to push further. May be you want to see it from a different perspective. or you may want claude to show its reasoning so you can verify the logic before acting on it.

- Change Perspective (Persona Prompting): Role

> now review this summary as a skeptical project sponsor. What questions or concerns would you raise about the timeline, budget or resource allocation?


- Show Reasoning (Chain of Thought): Task

....claude respose.....

> based on those concerns, think step by step about which risk is most critical to address before our steering committee meeting, and recommend one specific action I should take this week.


- Increase Focus: Context, Format


## Prompting Strategies for Better Results

- Zero-shot: No examples, just instructions
  Use zero-shot for standard format, where claude default structure works well such as summeries, explanation and simple analysis (Standard format)

- One-Shot : One example to follow.
  Use one-shot when your team expects a specific custom template.

- Few-shot: More examples to establish a pattern.
  Use few-shot for complex and custom patterns.


## Domain-specific and Multi-turn prompting





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

