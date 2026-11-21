# dMatrix Decision Capture — Skill

This folder is the dMatrix decision-capture **Skill** ([`SKILL.md`](SKILL.md)) in the shape
ChatGPT's Skill upload takes it. Every release publishes it as `decide.zip`: the `decide/` folder
at the top of the archive, without this README. Download it from the
[latest release](https://github.com/oxford-heavy/dmatrix-extensions/releases/latest/download/decide.zip).

The Claude plugin (`claude/dmatrix/`) and the Antigravity bundle (`google/antigravity/dmatrix/`)
each carry their own copy of the same Skill, so you never install this folder for those.

The Skill is the behavior only: on its own it cannot create or save anything in dMatrix. It needs
the connection to dMatrix, which each guide sets up:

- [Claude](../../claude/README.md)
- [OpenAI (ChatGPT and Codex)](../../openai/README.md)
- [Google (Antigravity)](../../google/README.md)

> `SKILL.md` is generated from the canonical prompt in the dMatrix repository. Do not edit it by
> hand. See the [overview](../../README.md).
