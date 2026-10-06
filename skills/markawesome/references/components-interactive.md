# Interactive components

Details · Accordion · Tabs · Dialog · Popover · Tooltip · Random content · Tree

Most of these split a trigger from its body with a `>>>` line (see the shared
`>>>` separator in `authoring.md`). Attributes are optional and order-independent.

## Details

One collapsible section. For a *group* of them, use an Accordion instead.

- **Primary:** `^^^appearance? icon-placement? disabled? open? name:value? icon:expand:name? icon:collapse:name?`
- **Alt:** `:::wa-details appearance? icon-placement? …`
- Separate the summary from the content with `>>>`. Close with `^^^`.

**Appearances:** `outlined` (default), `filled`, `filled-outlined`, `plain`.
**Icon placement:** `end` (default), `start`.
**Flags:** `disabled` (can't toggle), `open` (starts expanded).
**Accordion grouping:** `name:value` gives several details the same group name so
only one stays open (e.g. `name:faq`).
**Custom toggle icons:** `icon:expand:name` and `icon:collapse:name`.

```
^^^icon:expand:plus icon:collapse:minus
Show advanced options
>>>
These settings are optional. Most projects never change them.
^^^
```

## Accordion

A multi-section collapsible container — the grouped sibling of Details. Ideal for
FAQs and doc sections.

- **Primary:** `//////appearance? mode? icon-placement? heading:N?`
- **Alt:** `:::wa-accordion appearance? mode? icon-placement? heading:N?`
- The container fence is `//////` (**6 slashes**). Each item is a `///` block
  (**3 slashes**) with an explicit `///` close. Item bodies are full Markdown and
  may contain other components.

**Container tokens** (bare, order-independent, rightmost wins):

- **appearance:** `outlined` (default), `filled`, `filled-outlined`, `plain`.
- **mode:** `multiple` (default — several open at once), `single` (one open at a
  time, one always stays open), `single-collapsible` (one at a time, all can
  close).
- **icon-placement:** `end` (default), `start`.
- **heading:N** — semantic heading level for item headers: `1`–`6` or `none`.

**Item tokens** (leading, on the `///` header line): `expanded` (starts open),
`disabled` (renders but can't toggle), `icon:name` (custom expand icon). The rest
of the header line is the item's label.

```
//////filled single heading:3
/// What is Web Awesome?
A library of web components you can use anywhere.
///
/// expanded Is it free?
The core library is free and open source.
///
//////
```

`wa-accordion` is stable in Web Awesome (since 3.13.0), and everything here is
declarative and static-site-safe.

## Tabs

Switchable panels for parallel alternatives — per-OS steps, multi-language code, A/B.

- **Primary:** `++++++placement? activation? active? no-scroll-controls?`
- **Alt:** `:::wa-tabs placement? activation? active? no-scroll-controls?`
- The container fence is `++++++` (**6 pluses**). Each tab is `+++ Title` … `+++`.

**Placements:** `top` (default), `bottom`, `start`, `end`.
**Activation:** `auto` (default — switch on hover), `manual` (switch on click).
**Active panel:** name it with `active` (e.g. `tab-1`, `tab-2`).
**Flags:** `no-scroll-controls` (disable scroll arrows for overflowing tabs).
**Per-tab flag:** `disabled` as a leading token on the `+++ ` header line.

```
++++++top manual
+++ macOS
`brew install example`
+++
+++ Windows
`winget install example`
+++
+++ disabled Linux (coming soon)
Not yet available.
+++
++++++
```

## Dialog

Long supplementary content behind a trigger button — a modal.

- **Primary:** `???params?`
- **Alt:** `:::wa-dialog params?`
- Separate the trigger button text from the dialog content with `>>>`. Close with
  `???`.

**Parameters:** `light-dismiss` (close on outside click), and a **bare CSS width
value** to set the dialog width — `600px`, `50vw`, `40rem`, etc. (a bare
number-with-unit token, not `width:…`).

```
???light-dismiss 600px
Read the full changelog
>>>
## Changelog

Every release, in detail. Supports full **Markdown** inside the dialog.
???
```

## Popover

Floating content attached to a trigger — richer than a tooltip (full Markdown,
links). Works as a **block** or **inline**.

- **Block primary:** `&&&placement? link? without-arrow? distance:N? skidding:N?`
- **Inline:** `&&&trigger text >>> popover content&&&`
- **Alt:** `:::wa-popover placement? …`
- Block form separates trigger from content with `>>>`; close with `&&&`.

**Placements:** `top` (default), `bottom`, `left`, `right`, plus the eight aligned
variants (`top-start`, `top-end`, `right-start`, `right-end`, `bottom-start`,
`bottom-end`, `left-start`, `left-end`).
**Parameters:** `link` (render the trigger as a link instead of a button),
`without-arrow` (hide the arrow), `distance:N` (offset away from the trigger, px),
`skidding:N` (offset along the trigger, px; may be negative).

```
&&&bottom-start
More info
>>>
Popover content with **Markdown**, [links](https://example.com), and lists.
&&&
```

```
Click &&&here >>> This is an inline popover!&&& to learn more.
```

Inline extras: inline code in the trigger (`` &&&`code` trigger >>> content&&& ``)
and `\n` line breaks in the content.

## Tooltip

An inline glossary term / short definition on hover or focus. Declarative and
zero-JavaScript: the anchor renders as a focusable, dotted-underlined span wired
to the tip automatically.

- **Inline primary:** `(((placement? distance:N? skidding:N? anchor >>> tip)))`
- **Block alt:** `:::wa-tooltip placement? distance:N? skidding:N?` (anchor,
  `>>>`, tip, `:::`).

**Placements:** `top` (default), `bottom`, `left`, `right`, plus the eight aligned
variants. **Parameters:** `distance:N`, `skidding:N` (leading tokens, before the
anchor term).

**Tip content** is plain text (HTML-escaped). Use `\n` for line breaks (rendered
as `<br>`). Unlike a popover, a tooltip has no `link` or `without-arrow`.

```
Styling is handled by (((CSS >>> Cascading Style Sheets))) on the web.
```

```
(((bottom-start Org number >>> NO: 9 digits\nSE: 10 digits)))
```

## Random content

A container that shows one (or more) of its options at random and hides the rest,
optionally rotating them — a rotating tips / testimonials / featured-content block
with **zero JavaScript of your own** (Web Awesome's own runtime does the work).

- **Primary:** `......params?` (**6 dots**)
- **Alt:** `:::wa-random-content params?`
- Separate each option with a `>>>` line. Close with `......`.

**Parameters** (order-independent, on the opening fence):

- **mode:** `unique` (WA default), `random`, or `sequence` — as a bare word or
  `mode:random`.
- **animation:** `none`, `fade`, `fade-up`, `fade-down`, `fade-left`,
  `fade-right` — as a bare word or `animation:fade`.
- **items:n** — how many children to show at once (a bare integer like `2` works).
- **autoplay** — rotate the shown children automatically.
- **autoplay-interval:value** — milliseconds between rotations (e.g.
  `autoplay-interval:3000`).

```
......mode:random animation:fade
> "This tool saved us days of work." — A happy user
>>>
> "Setup took five minutes." — Another happy user
......
```

## Tree

A `<wa-tree>` hierarchy rendered from a **nested Markdown bullet list** — file/
directory layouts, taxonomies, nested navigation.

- **Primary:** `||||||open?` (**6 pipes**)
- **Alt:** `:::wa-tree open?`
- Wrap a normal nested bullet list; close with `||||||`. Children are more-indented
  list items (2- or 4-space indentation both work).

**Fence token:** `open` (alias `expanded`) marks every branch (any node with
children) expanded.
**Per-node leading tokens** (on each list item, stripped from the label):
`expanded` (force this branch open), `icon:name` (a leading folder/file icon).
Colon-bearing labels like `cbc:ID` are kept verbatim — only a *leading* `icon:`
token is treated as an icon.

```
||||||open
- icon:folder src
  - icon:file index.ts
  - icon:file utils.ts
- icon:file README.md
||||||
```

**Display/navigation only:** Web Awesome's interactive tree selection
(`selection`, `lazy`, `selected`) needs JavaScript and is deliberately omitted —
this emits a static-safe tree (nesting, initial expand state, leading icons).

> **WA runtime caveat (3.9.0):** `<wa-tree-item>` only honors a static `expanded`
> on items visible at load, so `open` expands the **top-level** branches; deeper
> branches stay collapsed until their parent is opened. The attribute is still
> emitted on every branch (harmless and forward-compatible); full deep-expand-on-
> load would need JavaScript.
