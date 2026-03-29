# Prompt writing Tips

## Overview

Some General Tips.

- Write explicit instructions.
- Be direct about what outputs should look like.
- Creat specialized agents.
- Provide examples of tasks and outputs.

## Improving the Odds of LLM success

- Asking models to explain themselves can improve the answers we recieve.

- Invoking chain of thought forces models to break down questions into smaller pieces.

- Models then rely on earlier work more heavily in forming their subsequent answers.

- Helpful in cutting back on hallucinations and increase respose accuracy.

- Makes it easier for users to verify outputs

## Zero Shot Chain of Thought

Only change made is appending a comand like...

>Explain your answer step by step

...to the end of a prompt


## Personified Responses

Asking models to respond as if they are an expert in particular field an help refine and elevate the quality of responses.

Requesting models responds as if we fit a certain persona can also make responses of good quality.


## Least to Most Chain of Thought

Instead of asking one complex or nebulous question, break it into multiple questions that are clearer.

Going step-by-step increases the odds of acceptable model performance.

This technique is similar to the use of work breakdown structures in project management.

## Consequences of reaching the Context Limit

- More Token Usage 
- Decreased quality or relevance
- Repetitive behavior or errors
- Slower response time

Stratigies to Counter

- Leverage the Claude.md file
- Work in Focused Chunks
- Explicit file inclusion
- Module specific summary
- Start New Chats

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

