# Content components

Callout · Card · Tag · Badge · Button · Copy button · Icon · Stepper

Every component has a **primary** shorthand delimiter and an equivalent
**`:::wa-*` alternative**. All attributes are optional and order-independent
(rightmost wins on conflict). Inner content is full Markdown. Unknown tokens are
silently dropped, so a mistyped variant simply vanishes — spell them exactly.

## Callout

Draw attention to elevated information with a colored, icon-led block.

- **Primary:** `:::type size? appearance? family? variant? animation? icon:name?`
- **Alt:** `:::wa-callout type size? appearance? family? variant? animation? icon:name?`
- Close with `:::`.

**Types** (the first token; sets color + default icon):

| Type | Color | Default icon | Use for |
|------|-------|--------------|---------|
| `info` / `brand` | blue | `circle-info` | notes, tips (`info` is an alias for `brand`) |
| `success` | green | `circle-check` | confirmations, "done" states |
| `warning` | yellow | `triangle-exclamation` | things that need care |
| `danger` | red | `circle-exclamation` | data loss, errors, destructive actions |
| `neutral` | gray | `gear` | low-key asides |

**Sizes:** `xs`, `s`, `m`, `l`, `xl` (Web Awesome 3.x five-step scale) plus the
legacy `small` / `medium` / `large` aliases.

**Appearances:** `accent`, `filled`, `outlined`, `plain`, `filled-outlined`.

**Icon overrides** (the callout's leading icon):

- `icon:name` — swap the icon glyph (e.g. `icon:rocket`, `icon:shield`).
- `family` — icon family: `classic`, `sharp`, `duotone`, `sharp-duotone`,
  `brands`, plus the WA 3.10.0 families `mosaic`, `pixel`, `vellum`, `slab-duo`,
  `slab-press-duo`, `chisel`, `etch`, `graphite`, `jelly`, `jelly-duo`,
  `jelly-fill`, `notdog`, `notdog-duo`, `slab`, `slab-press`, `thumbprint`,
  `utility`, `utility-duo`, `utility-fill`, `whiteboard`.
- `variant` — Font Awesome weight: `thin`, `light`, `regular`, `solid`,
  `semibold`.
- `animation` — `beat`, `fade`, `beat-fade`, `bounce`, `flip`, `shake`, `spin`,
  `spin-pulse`, `spin-reverse`, plus WA 3.10.0's `flip-360`, `spin-snap`,
  `spin-snap-4`, `spin-snap-8`, `buzz`, `float`, `jello`, `swing`, `wag`.
  Animation needs no Pro kit — e.g. `:::warning shake`.
- `canvas` — icon sizing box: `fixed` (default), `auto`, `square`, `roomy`.

```
:::success l icon:trophy
**Deploy succeeded.** Your site is live at the production URL.
:::
```

```
:::warning shake
This warning's icon animates. Family/variant glyph changes depend on your
Font Awesome kit tier; animation and canvas work with any kit.
:::
```

## Card

A flexible container with optional media, header, body, and footer slots — the
building block of a `::::grid`.

- **Primary:** `===appearance? orientation?`
- **Alt:** `:::wa-card appearance? orientation?`
- Close with `===`.

**Appearances:** `outlined` (default), `filled`, `filled-outlined`, `plain`,
`accent`. **Orientation:** `vertical` (default), `horizontal` (media and content
side by side).

**Composition is auto-detected from the body** (this is the part people get
wrong):

- The **first Markdown image** `![alt](src)` becomes the **media** slot.
- The **first bold line** `**Title**` becomes the **header** slot. (It must be a
  bold line on its own — *not* a `#` heading.)
- A **trailing Markdown link** on its own line becomes a **footer** button.
- Everything else is the body.

```
===
![Chart](/img/analytics.png)
**Analytics**
Track visits, referrers, and conversions in real time.
[Learn more](/docs/analytics)
===
```

```
===horizontal accent
**Horizontal card**
Media and content sit side by side.
===
```

## Tag

A small colored label for a category or status. Works **inline** in a sentence or
as a **block**.

- **Primary:** `@@@variant? appearance? size? pill? with-remove? icon:name?`
- **Alt:** `:::wa-tag variant? appearance? size? pill? with-remove? icon:name?`
- Inline form opens and closes on one line: `@@@variant Label @@@`.

**Variants:** `brand`, `success`, `neutral`, `warning`, `danger`.
**Appearances:** `accent`, `filled`, `outlined`, `filled-outlined`.
**Sizes:** `xs`, `s`, `m`, `l`, `xl` plus legacy `small` / `medium` / `large`.
**Flags:** `pill` (rounded), `with-remove` (adds a × button).
**Icon:** `icon:name` places an icon inside the tag.

```
The @@@success icon:check Stable @@@ API and the @@@warning Beta @@@ API differ.
```

```
@@@brand pill icon:star
Featured
@@@
```

> **`with-remove` caveat:** the × button only *fires* a `wa-remove` event — Web
> Awesome does not remove the tag for you. On a page with no JavaScript beyond
> the Web Awesome library it is inert. Add your own `wa-remove` listener to make
> it functional. The markup is valid either way.

## Badge

A compact count/status chip, often used to grab attention.

- **Primary:** `!!!variant? appearance? attention? pill?`
- **Alt:** `:::wa-badge variant? appearance? attention? pill?`
- Close with `!!!`.

**Variants:** `brand`, `success`, `neutral`, `warning`, `danger`.
**Appearances:** `accent`, `filled`, `outlined`, `filled-outlined`.
**Attention:** `none`, `pulse`, `bounce`. **Flags:** `pill`.

```
!!!brand pulse
New
!!!
```

Tag vs. badge: reach for a **tag** for a category/status label in flowing content,
a **badge** for a small attention-grabbing count or "new" marker (badges carry
the `pulse`/`bounce` animations).

## Button

A styled button — a link when it wraps a Markdown link, a plain button otherwise.

- **Primary:** `%%%variant? appearance? size? pill? caret? loading? disabled? target? download? icon:name? icon:end:name?`
- **Alt:** `:::wa-button variant? appearance? size? pill? caret? loading? disabled? …`
- Close with `%%%`.

**Variants:** `brand`, `success`, `neutral`, `warning`, `danger`.
**Appearances:** `accent`, `filled`, `outlined`, `filled-outlined`, `plain`.
**Sizes:** `xs`, `s`, `m`, `l`, `xl` plus legacy `small` / `medium` / `large`.
**Flags:** `pill`, `caret` (dropdown indicator), `loading`, `disabled`.

**Link behavior** (link-form buttons only — the body holds a Markdown link).
These are **bare tokens**, not `key=value` pairs:

- `_blank`, `_self`, `_parent`, `_top` set the anchor target; `_blank` also adds
  `rel="noopener noreferrer"` automatically.
- `download` makes the link download its target instead of navigating.

**Icons:** `icon:name` for a start icon, `icon:end:name` for an end icon (or the
explicit `icon:start:name`); combine both.

```
%%%brand icon:rocket
[Get started](https://example.com/start)
%%%
```

```
%%%neutral outlined icon:end:arrow-right _blank
[Read the docs](https://example.com/docs)
%%%
```

```
%%%success download
[Download sample](/files/sample.zip)
%%%
```

## Copy button

A button that copies text to the clipboard — attach it to any command, URL, or
value the reader will copy. The display supports Markdown while the copied text
stays raw.

- **Primary:** `<<<placement? tooltip:full|copy|none? duration? disabled? copy-label? success-label? error-label? from?`
- **Alt:** `:::wa-copy-button placement? tooltip:full|copy|none? …`
- Close with `<<<`.

**Tooltip placement:** `top` (default), `right`, `bottom`, `left`.
**Tooltip mode:** `tooltip:full` (default — hover/focus + copy feedback),
`tooltip:copy` (feedback only), `tooltip:none` (no tooltip).
**Feedback duration:** a bare number is the success-message duration in ms
(e.g. `2000`).
**Custom labels:** `copy-label="…"`, `success-label="…"`, `error-label="…"`.
**Copy from another element:** `from="element-id"` (also `from="input.value"`,
`from="link[href]"`). **Flags:** `disabled`.

```
<<<top copy-label="Copy install command"
npm install markawesome-js
<<<
```

## Icon

A standalone Web Awesome `<wa-icon>` — inline and decorative, or a labeled block.

- **Inline** `$$$name` — name only, decorative, no attributes; use mid-prose:
  `Click the $$$gear icon.`
- **Block** `:::wa-icon name family? variant? animation? canvas?` — the first
  token is the icon name; the rest are optional, order-independent attributes. A
  non-empty block body becomes the icon's accessible `label`; an empty body
  leaves it presentational. Close with `:::`.

**Icon attributes** (same vocabulary as the callout icon overrides):

- **family** — `classic`, `sharp`, `duotone`, `sharp-duotone`, `brands`, plus the
  WA 3.10.0 families (`mosaic`, `pixel`, `vellum`, `slab-duo`, `slab-press-duo`,
  `chisel`, `etch`, `graphite`, `jelly`, `jelly-duo`, `jelly-fill`, `notdog`,
  `notdog-duo`, `slab`, `slab-press`, `thumbprint`, `utility`, `utility-duo`,
  `utility-fill`, `whiteboard`).
- **variant** (Font Awesome weight) — `thin`, `light`, `regular`, `solid`,
  `semibold`.
- **animation** — `beat`, `fade`, `beat-fade`, `bounce`, `flip`, `shake`, `spin`,
  `spin-pulse`, `spin-reverse`, `flip-360`, `spin-snap`, `spin-snap-4`,
  `spin-snap-8`, `buzz`, `float`, `jello`, `swing`, `wag`.
- **canvas** (sizing box) — `fixed` (default), `auto`, `square`, `roomy`.

Animation and canvas work with any kit; family/variant glyph changes depend on
the kit's Font Awesome tier.

```
Enable it under the $$$gear Settings menu.
```

```
:::wa-icon bell shake
Notifications
:::
```

> **Static-site caveat:** an icon renders its glyph into shadow DOM with no
> light-DOM fallback — with Web Awesome's JavaScript disabled it shows nothing.
> See `authoring.md`.

## Stepper

Progress through a multi-step process — a checkout, an onboarding flow, a
tutorial's "you are here", a release pipeline's status. Written as a Markdown
**task list** inside a `>>>>>>` fence (6 chevrons). Display-only: it shows where
the reader is; it does not navigate.

- **Primary:** `>>>>>> orientation? label:"text"?` … `>>>>>>`
- **Alt:** `:::wa-stepper orientation? label:"text"?` … `:::`

**Container:** `horizontal` (default), `vertical`, `auto` → orientation;
`label:"text"` → accessible name.

**Steps** — each unindented `-`/`*`/`+` list line:

- `[x]` (or `[X]`) → completed (checkmark); `[ ]` or no box → not yet.
- **Leading flags:** `active` (the current step), `loading`, `disabled`.
- **Variants:** `neutral`, `brand`, `success`, `warning`, `danger`.
- **Attention:** `pulse`, `bounce`, `none`.
- `icon:name` replaces the step number with an icon.
- The rest of the line is the label (inline Markdown).
- Lines indented two or more spaces under a step become its **description**.

The current step is the one flagged `active`; otherwise the first incomplete
step; if every step is done, the last one.

```
>>>>>> label:"Checkout progress"
- [x] Cart
- [x] Shipping
- [ ] Payment
- [ ] Review
>>>>>>
```

```
>>>>>> vertical
- [x] icon:user Create an account
  Takes about a minute.
- [ ] active warning pulse icon:envelope Verify your email
  Check your inbox for the **confirmation** link.
- [ ] icon:rocket Launch your first project
>>>>>>
```

- Steps are one line each (plus description lines) — a stepper is a status
  display, not a container for step content. For the *content* of each step,
  use headings or a numbered list below it, or tabs.
- A flag word at the start of a label is read as a flag (`- active users` →
  flag `active`, label "users"); rephrase if that bites.
- `>>>>>>` never collides with the `>>>` separator of details, dialog,
  popover, tooltip and random content.
- `<wa-stepper>` is **experimental** in Web Awesome 3.14.0.
