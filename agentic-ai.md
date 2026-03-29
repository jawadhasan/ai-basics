# Agentic AI

An agent is a loop where an LLM decides what to do, calls a tool (function), gets a result, and repeats until the task is done.

## The simplest practical path

1. Pick the Anthropic Claude API (or OpenAI — same concepts apply). Install the SDK.

`pip install anthropic`

2. Understand Tool Use

This is the foundational primitive. You define functions your code can execute (e.g., search_web, read_file, run_sql), describe them to the model, and the model decides when to call them. Your code actually executes the function and feeds the result back. That's it — that's an agent.

3. Write your first agent loop

something like a file summarizer or a code reviewer that can read files, ask clarifying questions, and write output. Keep the tools simple at first (read file, write file, run bash command).

4. Try a framework once you feel the friction

After building one by hand, frameworks like LangChain, LlamaIndex, or Anthropic's own Claude Agent SDK start making sense. They handle the loop boilerplate, memory, and multi-agent coordination. Don't start here — the abstractions will confuse you before you understand what they're abstracting.

## Concrete first project idea

Build a "repo explainer" agent. Give it tools to list_files, read_file, and write_file. Ask it to explore an unfamiliar codebase and produce a summary doc. You'll immediately hit real agentic challenges: token limits, tool sequencing, error handling, knowing when to stop.

## Key mental shifts from traditional software development

- You're writing the environment (tools + loop), not the logic. The model supplies the logic.
- Reliability comes from good tool design and clear prompts, not control flow.
- Debugging means reading traces of model decisions, not stack traces.


# Example

- Create virtual environment
python -m venv venv

- Activate it (Windows)
venv\Scripts\activate

- Install packages
pip install -r requirements.txt

- Create .env file

ANTHROPIC_API_KEY=sk-ant-api03-xxxxxxxxxxxxxxxx

- Run Program
`python hello_agent.py`


```python

import os
from dotenv import load_dotenv
import anthropic

# Load API key from .env file
load_dotenv()

# Create the Anthropic client
client = anthropic.Anthropic(api_key=os.getenv("ANTHROPIC_API_KEY"))

# Send a simple message
message = client.messages.create(
    model="claude-opus-4-6",
    max_tokens=1024,
    messages=[
        {"role": "user", "content": "Hello! Can you confirm you're working? Reply in one sentence."}
    ]
)

print("Agent response:")
print(message.content[0].text)