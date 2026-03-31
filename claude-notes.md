
# Claude Notes

Claude generate content, but humans are accountable for how it is used.

## Workflow

1. Run /init to generate the base CLAUDE.md
2. Open CLAUDE.md and add your own context
3. Commit it so yur whole team benefits

## CLAUDE.md

Calaude's Context Window or working memory.

Typically contains:

- Tech Stack
- Project Structure
- Conventions

During work, your conversation, current working files, Claude's own responses add up -> 200,000 tokens limit ~600 pages of text.


## Confiugration added to CLAUDE.md

- Git workflows
- Test writing instructions
- Documentation Guidelines

## Claude Code Skills

A skill is a folder, it contains one required md file named SKILL.md which defines how claude should perform the task. The folder can also include optional supporting material.

your-skill-name-folder -> SKILL.md

Where Claude code skills are stored?

- System-level (~/.claude/skills-skill-name)
- Project-levle (.claude/skills/skill-name)
- Plugins (/plugin marketplace)

## Claude Code Hooks

User-defined shell commands that execute at various points in Claude code's lifecyle, providing deterministic control over Calaude Code's behavior. Claude code skills are stored?

- PreToolUse  (Run before any tool-use)
- PostToolUse (Run after tool-use)

## MCP Why it Matters

Allows Claude to access beyound local file system.

- Lets claude-code review pull requests directly.
- Fetches design updates form tools like Figma.

## Claude Skills vs. CLAUDE.md effcts on Context

Prompt:

Generate a chart with attached sales data (attach abc.csv).

- CLAUDE.md with Rules - always uses tokens with every prompt .
- Skills (use these colors to design charts...) - uses token on demand 

Response:

Response text and artifact with brand colors.

## What's a Subagent

- Task-specific assistant - called by the main agent for specialized help.
- Isolated execution context - Separate context window, defined role, scoped tool access.
- Independent execution - Returns results to main agent.

## WhyUse Subagents

- Preserve main context - keep the core conversation focused.
- Reduce cognitive clutter - Offload verbose skills like tests, audits and documentation.
- Enable specialization - Delegate work to role-specific subagents.

- Examples, code-reviewer.md, content-reviewer.md, doc-generator.md under .claude directory

- command `/agents`



## Plan Mode

- Planning new projects: Select architectures and create tasks and timelines

- Multi-step implementations: When your feature requires making edits to many files.

- Code Exploration: When you want to research the codebase throughly before changing anything

- Interactive Development: When you want to iterate on the direction with Claude.


## Example 

(Plan-mode)

> We have a new developer joining the team and I want to show them the authentication process. Can you analyze the authentication flow across all related fields. Trace how a login request flows from the route handler through to the database and back to the response. Include all files involved.

.....RESPONSE.....

(Edit-automatically)

> Can you also create the README.md with current setup instructions. Incliude enviornment variables, database setup, and how to run the dev server - follow the format in @CLAUDE.md. Keep it concise - just what someone needs to get started.


> Can you generate API documenation for all the auth endpoints we've created. Follow the format in @CLAUDE.md - keep it simple and practical.

## Examples

>Analyze this code for any security concerns and report back in bulleted list of aras that are concerning.

>Can you check the code for any error in fetch URL?

## Knowledge System

Build a system that can hypothesize, experiment, and compound over time.

Paste following into your CLAUDE.md file:

Before Starting a new task, review existing rules and hypotheses for this domain.

Apply rules by default. Check if any hypothesis can be tested with today's work.

At the end of each task, extract insights, store them in domain folders e.g:
/knowledge/
knowledge.md (facts and patterns)
hypotheses.md (need more data)
rules.md (confirmed - apply by default)

Maintain a /knowledge/INDEX.md that routes to each domain folder.

When a hypothesis gets confirmed 5+ times, promoto it to a rule.

When a rule gets contradicted by new data, demote it back to a hypothesis.