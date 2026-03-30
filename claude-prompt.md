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



### Example

Role: You are a business analyst preparing stakeholder communications.

Task: Create a weekly status report for the inventory system project.

Context: The dev team completed their ERP integration assessment and found two integration options. Barcode scanning requirements are being documented. Budget is at $42K of $50K approved.

Format:  Include sections for accomplishments, in-progress items, risks and next steps. Use bullet points.


[....CLAUDE-RESPONSE MAY FORMAT OUTPUT DIFFERENTLY....]

Role:…\
Task: …\
Context:…
Format: Follow this exact template, with no emojis:\
PROJECT STATUS REPORT\
Week of: [date]\
Project:[name]\
ACCOMPLISHMENTS\
-[bullet points]\
IN PROGRESS\
-[bullet points]\
BLOCKERS/RISKS\
[bullet points]\
NEST WEEK\
-[bullet points]\


## Domain-specific and Multi-turn prompting

Some tasks are too complex for a single prompt. Trying to accomplish everything in one prompt often produces shallow results.

The solution is to break-down the work into focused steps:

- Step-1
- Step-2
- Step-3

Each prompting step handle one piece and you build toward a complete deliverable.

There are two approaches to achieve this.

1. Multi-turn prompting

You have a back-and-forth conversation, refining and expanding as you go.   Its kind of a exploraty process since you discover the path as you go along.

Step1 (you): Create an initial list of requirements

Role: You are a business analyst helping document system requirements.

Task: Identify the key business requirements for adding a low-stock alert feature to an inventory management system.

Context: The warehouse operations team needs automatic alerts when inventory falls below reorder thresholds. This is part of inventory system project with a Q2 deadline.

Format: List 5-7 high-level business requirements, each as a single sentence starting with “The system shall….”

[[Claude Response.....]you can decide to deeper on specific area...]

>>Now expand requirement 3 about configurable thresholds. What specific configuration options should users have? Consider different user roles and product categories.


[Claude Response.....]

>>Now expand requirement 3 about configurable thresholds. What specific configuration options should users have? Consider different user roles and product categories.

[Claude Response.....]

>>Based on everything we’ve discussed, create a requirements summary table with columns for RequriementId, Description, Priority (High/Medium/Low), and Acceptance Criteria.

Now, if we do this process regularly, we can turn these steps into a prompt-chain for further use.

2. Prompt Chaining
 
 Planning upfront a sequence of prompting steps before you start interacting with claude. 

 Step1: Gather info...
 Step2: Anlyze and expand....
 Step3: Create deliverables with...

Prompt-chaining works best for repetable workflows since it always following the pre-planned steps.


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

