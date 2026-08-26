---
name: markawesome
description: >-
  Authors and reviews Markawesome-flavoured Markdown — a terse syntax
  (:::, ===, @@@, !!!, %%%, ^^^, ++++++, &&&, and more) that the markawesome
  and markawesome-js engines transform into Web Awesome web components
  (callouts, cards, tabs, accordions, tags, badges, buttons, tooltips,
  carousels, and grid/stack/cluster/split/flank/frame layouts). Use when
  writing, editing, or reviewing Markdown for a site built with markawesome,
  markawesome-js, jekyll-webawesome, or eleventy-plugin-webawesome — and
  proactively whenever plain prose would read better as a component (a warning
  as a callout, a feature list as a card grid, alternatives as tabs, a glossary
  term as a tooltip). Covers which component to reach for, when, and its exact
  syntax.
license: MIT
metadata:
  author: Janne Warén
  version: "0.1.0"
  homepage: https://github.com/jannewaren/markawesome-skill
---

# Markawesome authoring

Markawesome is a terse Markdown dialect that the **markawesome** (Ruby) and
**markawesome-js** (Node) engines transform into [Web Awesome](https://webawesome.com/)
web components. It powers the **jekyll-webawesome** and **eleventy-plugin-webawesome**
static-site integrations. Both engines accept **byte-for-byte identical** input,
so everything documented here works in either world.

## Behavioral contract (be proactive)

When writing, editing, or reviewing Markdown for one of these projects:

1. **Scan prose for component opportunities and act on them.** Don't wait to be
   asked. A paragraph that warns wants a `:::warning` callout; a bulleted feature
   list wants a `::::grid` of `===` cards; "on macOS… on Windows…" wants
   `++++++` tabs; a copy-me command wants a `<<<` copy button; a defined term
   wants a `(((term >>> definition)))` tooltip. Suggest the change and write it.
2. **Prefer terse Markawesome syntax over raw `<wa-*>` HTML.** If you would reach
   for a Web Awesome web component, write the Markawesome delimiter instead. Drop
   to raw HTML only for something Markawesome has no syntax for.
3. **Default to the primary shorthand delimiters** (`:::`, `===`, `@@@`, …). The
   `:::wa-*` / `::::wa-*` alternative forms exist for readability or disambiguation;
   reach for them only when the shorthand is ambiguous in context.
4. **Keep the Markdown valid.** Never break a table, list, or fenced code block.
   Component syntax inside a fenced ``` block is **not** transformed (it is
   protected), so use fences to show Markawesome examples literally.
5. **Never invent attributes.** Every delimiter, variant, size, and flag is
   enumerated in the reference files. If it isn't listed there, an engine will
   reject or ignore it — verify before you emit it.

## Component roster — recognize the opportunity

Each row is enough to *spot* a candidate without loading a reference. Load the
referenced file for exact attributes before writing anything non-trivial.

| Delimiter | Component | Reach for it when… | Reference |
|-----------|-----------|--------------------|-----------|
| `:::info` `:::success` `:::warning` `:::danger` `:::neutral` `:::brand` | Callout | highlighting a note, tip, prerequisite, warning, or error | components-content |
| `===` | Card | a self-contained unit (feature, product, link preview), esp. inside a grid | components-content |
| `@@@` | Tag | a status/category label — New, Beta, Deprecated, a topic (inline or block) | components-content |
| `!!!` | Badge | a compact count/status chip, often with `pulse`/`bounce` attention | components-content |
| `%%%` | Button | a call-to-action or link that should look like a button | components-content |
| `<<<` | Copy button | a command, URL, or config value users will copy-paste | components-content |
| `$$$name` / `:::wa-icon` | Icon | an inline decorative icon, or a labeled block icon | components-content |
| `^^^` | Details | one collapsible block of optional/advanced info | components-interactive |
| `//////` | Accordion | a *group* of collapsible sections — FAQ, doc sections | components-interactive |
| `++++++` | Tabs | switchable alternatives — multi-language code, per-OS steps, A/B | components-interactive |
| `???` | Dialog | long supplementary content hidden behind a trigger button | components-interactive |
| `&&&` | Popover | hover/click floating content (rich markdown block, or inline) | components-interactive |
| `(((` | Tooltip | an inline glossary term / short definition on hover | components-interactive |
| `......` | Random content | rotating tips/testimonials/featured content (zero-JS) | components-interactive |
| `\|\|\|\|\|\|` | Tree | a file/dir hierarchy or nested navigation from a bullet list | components-interactive |
| `~~~~~~` | Carousel | an image gallery or step-by-step visual slides | components-media |
| `\|\|\|` | Comparison | a before/after two-image slider | components-media |
| `;;;` / `;;;;;;` | Video / Playlist | embedded video(s) — Web Awesome **Pro** | components-media |
| `[[[…]]]` | Format date / Relative time | a localized absolute or "3 days ago" date | components-media |
| `::::grid` `::::stack` `::::cluster` `::::split` `::::flank` `::::frame` | Layouts | arranging the above (card grids, sidebars, tag clusters) | layouts |

## Where to read what

Load only what the task needs — the references are one level deep, each
self-contained:

- **`references/when-to-use.md`** — the decision guide: content shape → component,
  why, a generic snippet, and the anti-patterns. Read this first when deciding
  *whether* and *which*.
- **`references/components-content.md`** — callout, card, tag, badge, button,
  copy button, icon.
- **`references/components-interactive.md`** — details, accordion, tabs, dialog,
  popover, tooltip, random content, tree.
- **`references/components-media.md`** — carousel, comparison, video, video
  playlist, format date, relative time.
- **`references/layouts.md`** — the six `::::` layouts, the shared gap scale,
  `align`/`justify`, and nesting.
- **`references/authoring.md`** — dual syntax, Markdown-inside-blocks, image/link
  auto-detection, the `>>>` separator, front matter, the Web Awesome 3.12.0 pin,
  and static-safety / Pro caveats.
- **`references/examples.md`** — full generic pages combining many components.

## Companion skills

This is the **authoring layer** — which Markawesome Markdown to write, and when.
It does not document the underlying `<wa-*>` component APIs or page-level design.
For those, also install Web Awesome's own skills:

- **`webawesome`** — the individual `<wa-*>` component APIs (props, slots, events).
- **`webawesome-design`** — page layout, theming, design tokens, and brand color.

Reach for them when the work goes beyond emitting Markawesome Markdown (custom
component behavior, `<wa-page>` scaffolding, a theme). This skill deliberately
does not duplicate their content.
