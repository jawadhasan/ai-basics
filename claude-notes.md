
# Claude Notes

## Confiugration added to CLAUDE.md

- Git workflows
- Test writing instructions
- Documentation Guidelines

## Claude Code Skills

Where Claude code skills are stored?

- System-level (~/.claude/skills-skill-name)
- Project-levle (.claude/skills/skill-name)
- Plugins (/plugin marketplace)

## Claude Code Hooks

User-defined shell commands that execute at various points in Claude code's lifecyle, providing deterministic control over Calaude Code's behavior. Claude code skills are stored?

## Claude Skills vs. CLAUDE.md effcts on Context

Prompt:

Generate a chart with attached sales data (attach abc.csv).

- CLAUDE.md with Rules - always uses tokens with every prompt .
- Skills (use these colors to design charts...) - uses token on demand 

Response:

Response text and artifact with brand colors.


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


>> Can you generate API documenation for all the auth endpoints we've created. Follow the format in @CLAUDE.md - keep it simple and practical.

