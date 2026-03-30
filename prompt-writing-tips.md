# Prompt writing Tips

## Overview

Understanding "why" an AI tool responds in a certain way helps you contruct better prompts and, in turn, get better answers.

- Write explicit instructions.
- Be direct about what outputs should look like.
- Creat specialized agents.
- Provide examples of tasks and outputs.


## Popular Prompt Frameworks

- Zero-shot.
- Few-shot.
- Chain-of-thought.
- React.
- Role-based.
- Tree-of-thought


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

## Stratigies to Counter

- Focused Prmopts
- Good Documentation
- Strategic File Referenes

- Leverage the Claude.md file
>Make sure you create one with the /init comand for any existing codebases.

- Work in Focused Chunks
> Refactor the authentication module to use the new error handling pattern.

- Explicit file inclusion
>Looking only @backend/src/symptoms.ts @backend/src/controllers/symbptomsController ....

- Module specific summary
>Create a summary of the authentication module - what files are involved, how they connect and what patterns they use.

- Start New Chats
