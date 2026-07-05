# Worked examples

Three complete, generic pages showing how components compose. All content is a
stand-in — swap in the real thing. These use only the primary shorthand syntax.

## 1. Product landing page

A hero call to action, a feature grid, a copy-me install command, and a
before/after.

````markdown
# Acme Build

Ship static sites faster.

::::split
@@@brand pill New — v2.0 @@@

%%%brand icon:rocket
[Get started](https://example.com/start)
%%%
::::

:::success
**Now 3× faster.** The v2 engine builds a 10,000-page site in under a minute.
:::

## Why Acme Build

::::grid gap:l min:16rem
===
**Zero config**
Sensible defaults out of the box — no setup file required.
[Learn more](/docs/config)
===

===
**Framework-agnostic**
Works with any static site generator you already use.
[See integrations](/docs/integrations)
===

===
**Themeable**
Restyle everything with design tokens, no CSS overrides.
[Theming guide](/docs/theming)
===
::::

## Install in one line

<<<top copy-label="Copy install command"
npm install acme-build
<<<

## See the difference

The v2 redesign, side by side:

|||50
![Before](/img/v1.png)
![After](/img/v2.png)
|||
````

## 2. Docs — Getting started

A prerequisites callout, per-OS install tabs, an optional advanced-config Details
block, and inline tooltips for jargon.

````markdown
# Getting started

Get a project running in about five minutes.

:::warning
You need (((Node.js >>> A JavaScript runtime built on V8))) 18 or newer. Check
with `node --version` before you begin.
:::

## 1. Install

++++++manual
+++ macOS
<<<
brew install acme-build
<<<
+++
+++ Windows
<<<
winget install Acme.Build
<<<
+++
+++ Linux
<<<
curl -fsSL https://example.com/install.sh | sh
<<<
+++
++++++

## 2. Create a project

<<<
acme new my-site
<<<

## 3. Configure (optional)

^^^
Show advanced configuration
>>>
Most projects never touch these. Set them in `acme.config.js`:

```js
export default {
  incremental: true,
  concurrency: 8,
};
```
^^^

:::success
That's it — run `acme dev` and open the local URL. You're building with
(((SSG >>> Static Site Generator))) speed.
:::
````

## 3. Changelog + FAQ

A release with a relative-time stamp, tags for the kinds of change, and an FAQ
accordion.

````markdown
# Release notes

## v2.0.0 — [[[2026-06-26 style:long]]] ([[[relative 2026-06-26]]])

::::cluster gap:xs
@@@success Added @@@ @@@warning Changed @@@ @@@danger Removed @@@
::::

:::danger
**Breaking:** the `legacy` build mode is removed. Migrate to the default engine
before upgrading — see the migration guide.
:::

- @@@success Added @@@ incremental builds, on by default.
- @@@warning Changed @@@ the config file format to ESM.
- @@@danger Removed @@@ the deprecated `legacy` mode.

## FAQ

//////single heading:3
/// Is v2 a drop-in upgrade?
For most projects, yes — except the removed `legacy` mode noted above.
///
/// Do I need to change my config?
The config file is now ESM (`export default { … }`). Rename it to
`acme.config.js` and convert `module.exports` to `export default`.
///
/// expanded Where do I report bugs?
On the issue tracker. Include your Acme Build version and a minimal repro.
///
//////
````

## What these demonstrate

- **Layouts wrap components** — `::::grid` of cards, `::::cluster` of tags,
  `::::split` for a header row.
- **Callouts carry severity** — `:::success` for wins, `:::warning` for
  prerequisites, `:::danger` for breaking changes.
- **Tabs for parallel alternatives** — per-OS install steps the reader picks one
  of.
- **Copy buttons on every command** — nothing to hand-select.
- **Accordion for the FAQ, Details for one optional aside** — group vs. single.
- **Inline tooltips and dates** stay in the flow of prose.
