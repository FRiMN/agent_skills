# AGENTS.md

Instructions for AI agents who want to install the skills in this repository themselves.

## What this is

This repository is a collection of skills: every top-level folder (`archify`, `cq`, `curl`, `ddgs`, `find-skills`, `youtube-transcript`) contains a `SKILL.md` with instructions for the agent. Short descriptions and documentation links are in [README.md](README.md).

The invariant to preserve: after installation the skills must end up in the directory your harness reads, as `<skills-dir>/<skill>/SKILL.md`.

## Where to install

Choose the directory yourself — just make sure your harness actually scans it:

- usually it is `~/.agents/skills`;
- other common locations: `~/.claude/skills`, `.agents/skills` in the project root;
- if you are unsure, check the harness configuration or ask the user. Do not guess silently.

## Procedure

1. **Check whether it is already installed.** If the target directory is a git clone of this repository, simply update it:

   ```bash
   git -C <skills-dir> remote get-url origin
   git -C <skills-dir> pull --ff-only
   ```

2. **Clone.** If the target directory does not exist or is empty:

   ```bash
   git clone https://github.com/FRiMN/agent_skills.git ~/.agents/skills
   # SSH variant:
   # git clone git@github.com:FRiMN/agent_skills.git ~/.agents/skills
   ```

3. **If the target directory already holds other skills** — do not delete or overwrite them. Clone the repository elsewhere and symlink the skills you need:

   ```bash
   git clone https://github.com/FRiMN/agent_skills.git ~/src/agent_skills
   ln -s ~/src/agent_skills/<skill> <skills-dir>/<skill>
   ```

4. **Verify the installation:**

   ```bash
   ls <skills-dir>/*/SKILL.md
   ```

   Every skill must provide a `SKILL.md` file. If the harness caches the skill list, restart the session or make it re-read the directory.

5. **Install only the dependencies you need** (see below) and tell the user where everything is installed and what still has to be done manually.

## Skill dependencies

- **archify** — Node.js >= 18.
- **cq** — a local cq MCP server (see [docs](https://github.com/mozilla-ai/cq/tree/main/docs)); without it the `query`/`propose` tools are unavailable.
- **curl** — `curl` and `pandoc`.
- **ddgs** — `uv` (launched via `uvx`).
- **find-skills** — `npx skills` (Node.js).
- **youtube-transcript** — Node.js; run `npm install` once inside the skill folder.

## Rules

- Do not delete existing files or overwrite other people's skills without the user's explicit confirmation.
- Skills may run commands and access the network: review `SKILL.md` before activating them, especially if the installation source is not trusted.
- Flexibility matters more than following the steps literally: if the path layout or the activation mechanism in your harness differs, adapt the steps while preserving the `<skills-dir>/<skill>/SKILL.md` invariant, and ask the user when in doubt.
- Alternative to cloning: individual skills can be installed with their native tooling (e.g. `npx skills add <owner/repo@skill>`) if your harness supports it; the result must be the same — a skill folder with `SKILL.md` inside the skills directory.
