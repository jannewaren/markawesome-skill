# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code
in this repository.

## What This Is

`markawesome-skill` is a single [Agent Skill](https://docs.claude.com/en/docs/agents-and-tools/agent-skills)
(`markawesome`) that teaches an AI assistant to **author and review**
[Markawesome](https://github.com/jannewaren/markawesome)-flavoured Markdown — the
terse syntax that the **markawesome** (Ruby) and **markawesome-js** (Node) engines
transform into [Web Awesome](https://webawesome.com/) components.

It is **Markdown + metadata only** — no build step, no code, no engine dependency.
The npm package exists solely to distribute the skill through the `npx skills`
CLI; there is no `bin`, no `exports`, no compiled output.

## The markawesome ecosystem — keep the syntax in sync

The Markawesome-flavoured Markdown syntax spans **six repositories that must stay
in lockstep**:

| Repo | Role | Stack | Registry |
|------|------|-------|----------|
| `markawesome` | **Authors** the syntax (engine) | Ruby | RubyGems |
| `markawesome-js` | **Authors** the syntax (engine) | TypeScript / Node | npm |
| `jekyll-webawesome` | **Uses** it (Jekyll integration) | Ruby | RubyGems |
| `eleventy-plugin-webawesome` | **Uses** it (Eleventy integration) | Node | npm |
| `markawesome-vscode` | **Produces** it (snippets/completions/validation) | TypeScript | VS Code Marketplace |
| `markawesome-skill` | **Teaches** it (AI authoring skill) | Markdown | npm |

**This repo's role:** **teaches** the syntax — it documents, for an AI assistant,
which Markawesome Markdown to write and when. It authors no syntax of its own; it
only describes what **both** engines already accept. It must never document a
delimiter or attribute that only one engine supports.

**Sync rule:** when the engines add or change syntax, update this skill's
`SKILL.md` roster and the relevant `references/*.md` file to match — but only after
the change has landed in **both** engines (`markawesome` *and* `markawesome-js`).
The single source of truth for syntax/attributes is
`markawesome-vscode/src/data/components.json`; cross-check the engines' transformers
and specs (`markawesome/spec/`, `markawesome-js/test/parity-corpus.test.ts`) before
documenting anything. Where `components.json`'s prose and an engine's actual
behavior disagree, **the engine wins** (e.g. a card's header is the first **bold
line**, not a `#` heading).

## Layout — why the skill lives at `skills/markawesome/`

The skill sits at **`skills/markawesome/`** in the repo root (not `dist/`). This is
the one layout that satisfies every `npx skills` install path: the CLI skips
`dist/`/`build/` during git discovery, and its `experimental_sync` looks for
`<pkg>/skills/<name>/SKILL.md`. The skill's directory name (`markawesome`) **must
equal** the `name:` field in its `SKILL.md` frontmatter — that is the installed
skill name.

```
skills/markawesome/
├── SKILL.md          # frontmatter (name/description/license/metadata) + routing body
└── references/       # progressive disclosure, one level deep
```

### SKILL.md constraints

- `name: markawesome` **must equal** the containing folder name.
- `description` is what the assistant sees at all times and decides activation —
  keep it ≤ 1024 characters, third person, naming the trigger contexts and the
  proactive intent, with **no** "claude"/"anthropic" strings.
- Keep the body compact (< ~200 lines): the proactive behavioral contract, the
  one-line "use when" roster, and the progressive-disclosure index. Detail lives
  in `references/`, loaded on demand.

## Branching & Commits

This repo works directly on `main` — there is **no feature-branch convention**.
Commit changes, including version bumps, straight to `main`; do not create a branch
when asked to commit.

## Release workflow

Mirrors the rest of the ecosystem. Work on `main`:

1. Bump `version` in `package.json` and move the `CHANGELOG.md` `Unreleased` notes
   under a new `vX.Y.Z` heading.
2. `npm publish` (public access is preconfigured).
3. Push the commit.
4. Tag the released commit `vX.Y.Z` — the **same** version as `package.json` — and
   `gh release create vX.Y.Z` with notes drawn from `CHANGELOG.md`.

The GitHub Release tag **must equal** the version published to npm.

## Verifying a change

- **Frontmatter:** `name` equals the folder name; `description` ≤ 1024 chars and
  contains no "claude"/"anthropic".
- **Local install:** `npx skills add ./skills/markawesome` lands it as
  `markawesome` in `.claude/skills/` / `.agents/skills/`.
- **Syntax is real, not hallucinated:** run representative snippets from the
  references through `markawesome-js` (Node) or the Ruby engine's specs and confirm
  the expected `<wa-*>` HTML. Reject any attribute an engine rejects.
- **Packaging:** `npm pack --dry-run` shows `skills/**`, README, CHANGELOG, and
  LICENSE in the tarball.
