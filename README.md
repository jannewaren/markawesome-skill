# markawesome-skill

An [Agent Skill](https://docs.claude.com/en/docs/agents-and-tools/agent-skills)
that teaches an AI assistant to **author and review
[Markawesome](https://github.com/jannewaren/markawesome)-flavoured Markdown** —
the terse syntax (`:::`, `===`, `@@@`, `!!!`, `%%%`, `^^^`, `++++++`, `&&&`, …)
that the **markawesome** (Ruby) and **markawesome-js** (Node) engines transform
into [Web Awesome](https://webawesome.com/) web components.

It does two things:

1. **Recognizes opportunities proactively** — while you write or review Markdown,
   it spots prose that would read better as a component and suggests it unprompted
   ("this warning should be a `:::danger` callout"; "these three features want a
   `::::grid` of `===` cards").
2. **Writes the exact syntax** — every component's delimiter, attributes, and when
   to reach for it, verified against both engines so it never emits syntax only
   one accepts.

The skill is **pure Markdown knowledge** — no build step, and installing it needs
no clone of the Ruby or JS engine.

## Install

The skill installs with [`npx skills`](https://github.com/vercel-labs/skills) —
the same CLI Web Awesome ships their skill with.

### Recommended — one line, from GitHub

```bash
npx skills add jannewaren/markawesome-skill
```

No `npm install`, no engine clone. This symlinks the skill into each detected
agent's directory (`.claude/skills/markawesome`, `.agents/skills/markawesome`, …).

### From npm

```bash
npm install markawesome-skill
npx skills experimental_sync          # auto-discovers skills/markawesome/
# …or point at it explicitly:
npx skills add ./node_modules/markawesome-skill/skills/markawesome
```

> **Reality check:** `npx skills` has **no npm-registry resolver**. A bare package
> name — `npx skills add markawesome-skill` — does **not** work: the CLI falls
> through to `git clone` and fails. The true one-liner is the **GitHub** form
> above; npm distribution is `install` + `experimental_sync` (or a path `add`).

## Companion skills

This is the **authoring layer** — which Markawesome Markdown to write, and when.
For the underlying `<wa-*>` component APIs and for page layout / theming / brand
color, also install Web Awesome's own skills:

- **`webawesome`** — the individual `<wa-*>` component APIs.
- **`webawesome-design`** — page layout, theming, and design tokens.

This skill deliberately does not duplicate their content.

## What's inside

```
skills/markawesome/
├── SKILL.md                         # routing body + the proactive "brain"
└── references/
    ├── when-to-use.md               # content-pattern → component decision guide
    ├── components-content.md        # callout, card, tag, badge, button, copy button, icon
    ├── components-interactive.md    # details, accordion, tabs, dialog, popover, tooltip, random content, tree
    ├── components-media.md          # carousel, comparison, video, playlist, format date, relative time
    ├── layouts.md                   # grid, stack, cluster, split, flank, frame
    ├── authoring.md                 # dual syntax, caveats, the WA 3.10.0 pin
    └── examples.md                  # generic full-page worked examples
```

## The Markawesome ecosystem

This skill is the **teaching layer** for a family of repositories that keep the
same Markdown dialect in lockstep:

| Repo | Role |
|------|------|
| [`markawesome`](https://github.com/jannewaren/markawesome) | Authors the syntax (Ruby engine) |
| [`markawesome-js`](https://github.com/jannewaren/markawesome-js) | Authors the syntax (Node engine) |
| [`jekyll-webawesome`](https://github.com/jannewaren/jekyll-webawesome) | Uses it (Jekyll integration) |
| [`eleventy-plugin-webawesome`](https://github.com/jannewaren/eleventy-plugin-webawesome) | Uses it (Eleventy integration) |
| [`markawesome-vscode`](https://github.com/jannewaren/markawesome-vscode) | Produces it (editor tooling) |
| **`markawesome-skill`** | **Teaches it (AI authoring skill)** |

Because the two engines accept byte-for-byte identical input, everything the skill
documents works in both the Ruby and Node worlds. See the
[live examples site](https://jannewaren.github.io/jekyll-webawesome/) to watch the
Markdown render into components side by side.

## License

[MIT](LICENSE.txt) © Janne Warén
