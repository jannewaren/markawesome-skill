# Layouts

Grid · Stack · Cluster · Split · Flank · Frame · Divider

Layouts use the `::::` (**quadruple colon**) fence and map to Web Awesome CSS
utility containers (`<div class="wa-grid">`, etc.). They **wrap** components —
put cards, callouts, tags inside a layout; never put a layout inside a component.
Inner content is passed through untouched, so component `:::`/`===`/`@@@` syntax
inside a layout transforms normally.

- **Primary:** `::::type params?` … `::::`
- **Alt:** `::::wa-type params?` … `::::`

## Shared attributes (all six layouts)

- **`gap:SIZE`** — spacing between items. Scale: `0`, `3xs`, `2xs`, `xs`, `s`,
  `m`, `l`, `xl`, `2xl`, `3xl`, `4xl`, `5xl`.
- **`align:VALUE`** — align items: `start`, `end`, `center`, `stretch`,
  `baseline`.
- **`justify:VALUE`** — justify content: `start`, `end`, `center`,
  `space-between`, `space-around`, `space-evenly`.

Unknown gap/align/justify values are dropped, so a typo just has no effect.

## Grid

A responsive auto-wrapping grid — no media queries. The default layout for a
*set* of cards.

- **Extra attribute:** `min:CSS` — minimum column size before wrapping (e.g.
  `min:300px`, `min:20ch`, `min:15rem`).

```
::::grid gap:l min:16rem
===
**Fast**
Sub-second builds.
===

===
**Themeable**
Restyle with design tokens.
===

===
**Portable**
Works with any static site generator.
===
::::
```

## Stack

A vertical stack with consistent spacing — use it to give a run of blocks even
rhythm.

```
::::stack gap:m
:::info
First note.
:::

:::success
Second note.
:::
::::
```

## Cluster

Inline items that wrap — perfect for a tag cloud, a button row, or an icon list.

```
::::cluster gap:xs
@@@brand Ruby @@@ @@@success Jekyll @@@ @@@neutral Markdown @@@ @@@warning Beta @@@
::::
```

## Split

Distributes items to opposite ends — the classic header / footer / nav-bar
pattern.

- **Extra modifiers:** `row` (horizontal, default) or `column` (vertical).

```
::::split
**© 2026 Example, Inc.**

[Privacy](/privacy) | [Terms](/terms)
::::
```

## Flank

A sidebar beside main content; the flank wraps below on small screens.

- **Modifiers:** `start` (flank on the start side, default) or `end`.
- **Extra attributes:** `size:CSS` (flank size, e.g. `size:200px`, `size:15rem`),
  `content:PCT` (minimum content width, e.g. `content:70%`).

```
::::flank start size:220px gap:l
![Avatar](/img/avatar.jpg)

## About the author
A short bio goes here, beside the portrait.
::::
```

## Frame

An aspect-ratio container for images and media.

- **Modifiers:** `landscape` (16:9), `portrait` (9:16), `square` (1:1).
- **Extra attribute:** `radius:SIZE` — `s`, `m`, `l`, `pill`, `circle`, `square`.

```
::::frame landscape radius:l
<img src="/img/hero.jpg" alt="Product hero">
::::
```

> **Frame + images:** use a raw `<img>` tag inside a frame. Markdown image syntax
> may not be processed inside layout containers, so `![alt](src)` can fail to
> render there — this is the one place to drop to HTML. Elsewhere, Markdown
> images work normally.

## Divider

A labeled rule (Web Awesome 3.13.0+) — "or" between two alternatives, a section
label, an icon flourish, or an upright separator between items in a row. It is
**one line** with mirrored dashes; unlike the `::::` layouts it has no fence and
no body.

- **Primary:** `--- tokens? label ---`
- **Alt:** `:::wa-divider tokens?` … `:::` — the body is the label (empty → bare
  divider)

**Leading tokens** (consumed from the left; the rest of the line is the label, as
inline Markdown): `start`, `center` (default), `end` → label placement;
`horizontal` (default), `vertical` → orientation; `icon:name` → an icon before
the label (on its own: an icon-only divider).

```
::::stack
%%%brand
Sign in with email
%%%
--- or ---
%%%neutral
Continue with SSO
%%%
::::

--- start Release notes ---

--- icon:star ---
```

`vertical` makes an upright separator between inline items:

```
::::cluster align:center
%%%success
Approve
%%%
--- vertical or ---
%%%danger
Reject
%%%
::::
```

- A plain `---` (and `--- ---`) stays an ordinary `<hr>` — only a line **with a
  label** between the dashes becomes a `<wa-divider>`. A pipe-less table
  separator such as `--- | ---` is left alone too.
- A label that *starts* with `start`, `end`, `vertical`, … would be read as a
  token. Use the alt form for it: `:::wa-divider` / `start here` / `:::`.
- Dividers work anywhere — inside layouts, cards, callouts, tabs, accordion and
  dialog bodies.
- Don't use one where a heading belongs: a divider label is a quiet marker, not
  a section title.

## Nesting

- Components nest **inside** layouts: a `::::grid` of `===` cards, a `::::cluster`
  of `@@@` tags, a `::::stack` of `:::` callouts.
- Layouts may nest inside layouts when it genuinely helps (a `::::split` header
  above a `::::grid` body), but keep it shallow — deep nesting is hard to read and
  rarely necessary.
- Do **not** nest a layout inside a component body (no `::::grid` inside a `===`
  card). Component bodies hold prose and inline components, not block layouts.
