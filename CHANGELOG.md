# Changelog

All notable changes to `markawesome-skill` are documented here. The format is
based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and this
project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added

- **Stepper** (`>>>>>>` around a task list → a display-only `<wa-stepper>`, Web Awesome 3.14.0, experimental): a new section in `references/components-content.md` (container `horizontal`/`vertical`/`auto` + `label:"…"`; per-step `[x]`, `active`/`loading`/`disabled`, variants, attention, `icon:name`, indented descriptions; how the current step is chosen; the flag-word and status-not-content caveats), a roster row in `SKILL.md`, a "multi-step process" entry in `references/when-to-use.md`, and a static-safety note plus a `>>>>>>` vs `>>>` note in `references/authoring.md`.
- **Labeled divider** (`--- label ---` → `<wa-divider>` with a label, Web Awesome 3.13.0+): a new section in `references/layouts.md` (placement/orientation/icon tokens, the `:::wa-divider` form for labels that start with a token word, plain `---` staying an `<hr>`), a roster row in `SKILL.md`, and an "alternatives / section break" entry in `references/when-to-use.md`.
- The `SKILL.md` frontmatter `description` now names the `>>>>>>` and `--- label ---` delimiters and the stepper/divider components, so the skill triggers on them.

### Changed

- The documented **Web Awesome version pin moves 3.10.0 → 3.14.0** (`references/authoring.md`, plus the `SKILL.md` and `README.md` pointers to it), matching the bumped CDN pins in the `jekyll-webawesome` and `eleventy-plugin-webawesome` examples sites. The skill's attribute vocabulary was re-verified against 3.11.0, 3.12.0, 3.13.0 and 3.14.0: the icon families, the 18 animations, the `xs–xl` size scale and canvas sizing all still match, and no enum any transformer accepts lost a value. The historical "added in WA 3.10.0" attributions in `references/components-content.md` are left as-is — they say when a value appeared, not which version is pinned.
- **Accordion and Random content are no longer called "experimental"** (`references/authoring.md`, `references/components-interactive.md`): Web Awesome 3.13.0 promoted both to stable. Video and Video playlist stay flagged — they are still experimental Pro components.

## [0.1.0] - 2026-07-05

### Added

- Initial release of the `markawesome` Agent Skill.
- `SKILL.md` routing body: what Markawesome is, the proactive behavioral
  contract, a one-line "use when" roster for every component, the
  progressive-disclosure index, and a companion-skills pointer to Web Awesome's
  own `webawesome` / `webawesome-design` skills.
- Reference files under `skills/markawesome/references/`:
  - `when-to-use.md` — content-pattern → component decision guide plus
    anti-patterns.
  - `components-content.md` — callout, card, tag, badge, button, copy button,
    icon.
  - `components-interactive.md` — details, accordion, tabs, dialog, popover,
    tooltip, random content, tree.
  - `components-media.md` — carousel, comparison, video, video playlist, format
    date, relative time.
  - `layouts.md` — grid, stack, cluster, split, flank, frame, the shared gap
    scale, and nesting rules.
  - `authoring.md` — dual syntax, Markdown-in-blocks, image/link auto-detection,
    the `>>>` separator, the Web Awesome 3.10.0 pin, and static-safety / Pro
    caveats.
  - `examples.md` — generic full-page worked examples (landing page, docs
    getting-started, changelog + FAQ).
- Distribution as an npm package (`files: ["skills", …]`) installable through the
  `npx skills` CLI from GitHub or npm.
