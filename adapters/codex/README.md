# Codex / AGENTS.md adapter

OpenAI Codex (and Gemini CLI, Jules, and other agents that follow the open
[AGENTS.md](https://agents.md) convention) read an `AGENTS.md` file from your
project root.

## Install

Copy this repo's root [`AGENTS.md`](../../AGENTS.md) into your own project:

```bash
# from your project root
curl -fsSL https://raw.githubusercontent.com/fasterv410/design-dna/main/AGENTS.md \
  -o AGENTS.md
```

If your project already has an `AGENTS.md`, append the Design DNA section to it
instead of overwriting — Codex reads the whole file.

For Codex specifically you can also place it at `~/.codex/AGENTS.md` to make the
method available in every project.

That's it — the method in `AGENTS.md` is complete and self-contained.
