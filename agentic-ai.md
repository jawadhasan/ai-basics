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

Think of it like you're hiring a smart contractor (the LLM) to do a job. You:

Give them a goal (the prompt)
Give them a toolbox (your Python functions)
They figure out the steps and call you when they need a tool run

Your job as the developer shifts from writing the steps to building the toolbox and setting up the workspace. That's a real skill shift but it builds directly on what you already know.



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

```

# Example - Read/Write Files Agent


run_agent("Read notes.txt and write a summary to summary.txt")

You still wrote read_file and write_file — identical Python functions. The difference is you're not hardcoding the sequence. The model figures out the steps from the goal.

This becomes powerful when the task is dynamic — like "look at these 10 files and decide which ones need updating" — where you can't pre-define every step. The model reasons its way through it while your tools do the actual work.



```python


import os
import json
from dotenv import load_dotenv
import anthropic

load_dotenv()
client = anthropic.Anthropic(api_key=os.getenv("ANTHROPIC_API_KEY"))

# ── 1. TOOL DEFINITIONS ──────────────────────────────────────────────────────
# These tell Claude what tools are available and what arguments they accept.

tools = [
    {
        "name": "read_file",
        "description": "Read the contents of a file from disk.",
        "input_schema": {
            "type": "object",
            "properties": {
                "filename": {
                    "type": "string",
                    "description": "The name of the file to read (e.g. notes.txt)"
                }
            },
            "required": ["filename"]
        }
    },
    {
        "name": "write_file",
        "description": "Write text content to a file on disk.",
        "input_schema": {
            "type": "object",
            "properties": {
                "filename": {
                    "type": "string",
                    "description": "The name of the file to write (e.g. summary.txt)"
                },
                "content": {
                    "type": "string",
                    "description": "The text content to write into the file"
                }
            },
            "required": ["filename", "content"]
        }
    }
]

# ── 2. TOOL EXECUTION ─────────────────────────────────────────────────────────
# This is YOUR code that actually does the work when Claude requests a tool.

def execute_tool(tool_name, tool_input):
    if tool_name == "read_file":
        filename = tool_input["filename"]
        try:
            with open(filename, "r") as f:
                content = f.read()
            print(f"  [Tool] Read '{filename}' ({len(content)} chars)")
            return content
        except FileNotFoundError:
            return f"Error: File '{filename}' not found."

    elif tool_name == "write_file":
        filename = tool_input["filename"]
        content = tool_input["content"]
        with open(filename, "w") as f:
            f.write(content)
        print(f"  [Tool] Wrote '{filename}' ({len(content)} chars)")
        return f"Successfully wrote to '{filename}'."

# ── 3. AGENT LOOP ─────────────────────────────────────────────────────────────
# The loop: send message → Claude may request a tool → we run it → repeat
# until Claude gives a final text response (no more tool calls).

def run_agent(user_message):
    print(f"\nUser: {user_message}\n")
    messages = [{"role": "user", "content": user_message}]

    while True:
        response = client.messages.create(
            model="claude-opus-4-6",
            max_tokens=1024,
            tools=tools,
            messages=messages
        )

        # Check why Claude stopped
        if response.stop_reason == "end_turn":
            # Claude is done — extract and print the final text
            final_text = next(b.text for b in response.content if hasattr(b, "text"))
            print(f"Agent: {final_text}")
            break

        elif response.stop_reason == "tool_use":
            # Claude wants to use a tool — find which one
            tool_use_block = next(b for b in response.content if b.type == "tool_use")
            tool_name  = tool_use_block.name
            tool_input = tool_use_block.input

            print(f"  [Agent] Requesting tool: {tool_name}({json.dumps(tool_input)})")

            # Run the tool and get the result
            tool_result = execute_tool(tool_name, tool_input)

            # Add Claude's response and the tool result back into the conversation
            messages.append({"role": "assistant", "content": response.content})
            messages.append({
                "role": "user",
                "content": [{
                    "type": "tool_result",
                    "tool_use_id": tool_use_block.id,
                    "content": tool_result
                }]
            })
            # Loop again — Claude will now continue with the tool result


# ── 4. RUN IT ─────────────────────────────────────────────────────────────────

run_agent("Read the file notes.txt, then write a short summary of it to summary.txt")




```