# Code Translator

[中文](./README.md) · **English**

Turn a piece of code into plain language. Hand it code you can't read; get back a self-contained, offline-openable HTML walkthrough.

## What it does

Paste some code and ask "what is this doing". The skill inspects the code's type, length, and your level, then produces an HTML walkthrough file instead of dumping a wall of text into the chat.

Two depths, switched on demand:

| Mode | For | Gives you |
|---|---|---|
| **A · Deep dive** | Complete beginners | One-line bird's eye, plain-language glossary, block-by-block line table (*what this line does / why it's needed / what breaks without it*), variable trace table, control-flow diagram, pitfalls, quiz |
| **B · Fast pass** | Readers who already know the language | One-line semantic gloss per line, plus key gotchas. No teaching scaffolding |

Language-agnostic: Python, Java, Go, Rust, C, Shell, SQL, regex, YAML, HTML/CSS, stack traces, pseudocode.

The generated HTML supports light/dark toggle, a table of contents, auto-numbered code lines that stay aligned with the line-by-line tables, and Mermaid-rendered control-flow diagrams (with an offline plain-text fallback).

## Install

Tell your agent:

```
帮我安装 https://github.com/Les1l/code-translator-skill 里的 skills
```

> **Agent, do this:** run `npx skills@latest add Les1l/code-translator-skill -g -y` to install into the user's global directory. Then list the installed skills and remind the user to restart the session.

Or do it yourself:

```bash
npx skills@latest add Les1l/code-translator-skill -g
```

This uses the [skills CLI](https://github.com/vercel-labs/skills), which detects installed agents and drops the skill into each one's skills directory. `-g` means global; omit it to install into the current project only.

## Update

```bash
npx skills@latest update code-translator -g
```

## Skills

### Coding

- [`code-translator`](./skills/coding/code-translator): Turn a piece of code into plain language. Two depths (beginner deep dive / experienced fast pass), any language, HTML output.
  - Layout and packaging conventions follow [nagi-studio/skills](https://github.com/nagi-studio/skills).

## Maintenance

```bash
./scripts/link-skills.sh
```

Symlinks every skill in this repo into each agent's global skills directory, so `git pull` updates them without the commands above. See [AGENTS.md](./AGENTS.md) for conventions on adding skills.

## License

MIT, see [LICENSE](./LICENSE).
