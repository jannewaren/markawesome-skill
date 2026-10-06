# When to use what — the decision guide

This is the proactive core. Match the **shape of the content** in front of you to
a component, reach for it, and write it. Every snippet below is generic — swap in
the real content. For exact attributes, open the linked component reference.

## Content shape → component

### A paragraph that warns, cautions, or flags a prerequisite → Callout

Prose like "Note that…", "Be careful…", "You must first…", "This will delete…"
is a callout. Pick the type by severity:

- `:::info` / `:::brand` — a neutral note or tip.
- `:::success` — a confirmation, a "you're done" state.
- `:::warning` — something that can go wrong or needs care.
- `:::danger` — data loss, irreversible or destructive actions, errors.
- `:::neutral` — a low-key aside.

```
:::warning
Rotating your API key invalidates every existing token immediately. Update your
deployed services before rotating.
:::
```

→ `components-content.md`. Don't turn *every* sentence into a callout — reserve
them for genuinely elevated information (see anti-patterns).

### A bulleted list where each item is a self-contained unit → Card grid

Three features, three pricing tiers, three linked resources — each with a title
and a sentence or two — read far better as cards in a responsive grid than as a
bullet list.

```
::::grid gap:l min:16rem
===
**Fast**
Zero-config, sub-second builds.
===

===
**Framework-agnostic**
Works with any static site generator.
===

===
**Themeable**
Restyle everything with design tokens.
===
::::
```

→ `layouts.md` (grid) + `components-content.md` (card). One card alone is fine
too; the grid is what makes a *set* of them shine.

### "On macOS… / On Windows…", or the same thing in several languages → Tabs

Parallel alternatives where the reader wants **one** of them — per-OS install
steps, the same API call in curl / JS / Python, an A/B choice — are tabs.

```
++++++
+++ macOS
`brew install example`
+++
+++ Windows
`winget install example`
+++
++++++
```

→ `components-interactive.md`. If the alternatives are meant to be read
*together* (a comparison), use a table or a `::::grid` instead.

### A list of question → answer pairs → Accordion

An FAQ, a set of collapsible doc sections, "common problems" — a *group* of
headers that expand — is an accordion. (One lone collapsible block is Details,
below.)

```
//////single
/// Is it free?
The core library is free and open source.
///
/// Does it need a build step?
No — it runs at your site's build time.
///
//////
```

→ `components-interactive.md`.

### One block of optional / advanced / "click for details" content → Details

A single spoiler, an advanced-config aside, a long stack trace you don't want
inline — one collapsible section — is Details, not an accordion.

```
^^^
Show the full configuration
>>>
```yaml
verbose: true
retries: 5
```
^^^
```

→ `components-interactive.md`.

### A term that needs a short definition → Tooltip

A jargon word, an acronym, a field whose format needs explaining — anything where
you'd otherwise write "(i.e., …)" — is an inline tooltip.

```
Styled with (((CSS >>> Cascading Style Sheets))) and shipped as one file.
```

→ `components-interactive.md`. For a *rich* floating block (markdown, links) on
hover, use a Popover instead.

### A command, URL, token, or config value the reader will copy → Copy button

Anything a reader will select-and-copy — an install command, a connection string,
an API endpoint — should carry a copy button so they don't have to hand-select.

```
<<<
npm install markawesome-js
<<<
```

→ `components-content.md`.

### A status or category label inline in prose or a heading → Tag or Badge

- **Tag** (`@@@`) — a category/status label with a variant color: `New`, `Beta`,
  `Deprecated`, a topic. Works inline mid-sentence or as a block.
- **Badge** (`!!!`) — a compact count or status chip, often demanding attention
  with `pulse` / `bounce` (a notification count, a "3 new" marker).

```
The @@@warning Deprecated @@@ endpoint is removed in v2.
```

→ `components-content.md`.

### A call to action or a link that should look like a button → Button

"Get started", "Download", "View docs" — a prominent link — is a button. Include
a markdown link to make it navigate; omit it for a plain (JS-wired) button.

```
%%%brand
[Get started](https://example.com/start)
%%%
```

→ `components-content.md`.

### A before/after pair of images → Comparison

A redesign, a filter on/off, an edit diff — two images the reader drags between —
is a comparison slider.

```
|||
![Before](before.jpg)
![After](after.jpg)
|||
```

→ `components-media.md`.

### A gallery or sequential visual steps → Carousel

Multiple images or slides the reader pages through — a screenshot gallery, a
step-by-step walkthrough — is a carousel.

→ `components-media.md`.

### A file/directory layout or nested hierarchy → Tree

Anywhere you'd draw an ASCII file tree, or show nested navigation/taxonomy, use a
Tree — it's just an indented bullet list inside a `||||||` fence.

```
||||||open
- icon:folder src
  - icon:file index.ts
  - icon:file utils.ts
- icon:file README.md
||||||
```

→ `components-interactive.md`.

### Rotating tips / testimonials / featured content → Random content

A "tip of the day", a rotating testimonial, a featured item that varies per load
— with **no JavaScript of your own** — is random content.

→ `components-interactive.md`.

### A multi-step process and where the reader is in it → Stepper

"Step 2 of 4", a checkout or onboarding flow, a tutorial's progress, a
pipeline's status — a task list inside `>>>>>>` with `[x]` on the finished steps.

```
>>>>>>
- [x] Install
- [x] Configure
- [ ] Deploy
>>>>>>
```

Use it for **status**, not for the steps' instructions: keep the how-to as a
numbered list or headings, and the stepper as the at-a-glance map.

→ `components-content.md`.

### Alternatives side by side, or a quiet section break → Divider

"Sign in with email — or — continue with SSO" wants `--- or ---` between the
two buttons; a light section marker wants `--- start Release notes ---`; a
separator between buttons in a row wants `--- vertical or ---` inside a
`::::cluster`. A plain `---` stays a plain rule.

→ `layouts.md`.

### A published/updated date → Format date or Relative time

"Published June 26, 2026" → `[[[2026-06-26 style:long]]]`. "Updated 3 days ago" →
`[[[relative 2026-06-20]]]`. Both localize in the browser.

→ `components-media.md`.

### A sidebar-plus-content or header-with-actions section → Layout

- Sidebar + main → `::::flank`.
- Two things pushed to opposite ends (logo left, nav right; copyright + links) →
  `::::split`.
- A row of tags/buttons/icons that wraps → `::::cluster`.
- Consistent vertical rhythm between blocks → `::::stack`.
- A responsive card grid → `::::grid`.
- An aspect-ratio media box → `::::frame`.

→ `layouts.md`.

## Anti-patterns — don't do these

- **Don't wrap everything.** If every paragraph is a callout, none of them stand
  out. Components are emphasis; emphasis is scarce. Plain prose is the default.
- **Don't nest interactive triggers.** A dialog inside a tooltip, a popover
  inside a popover, a tab group inside a single tab that only holds another tab
  group — these confuse readers and sometimes the runtime. Keep one trigger deep.
- **Layouts wrap components; components don't wrap layouts.** Put cards inside a
  `::::grid`; don't put a `::::grid` inside a `===` card. Layout containers are
  the outermost structure. (A callout or card body holds prose and inline
  components, not another `::::` block.)
- **Don't reach for a component when Markdown already says it.** A two-item list
  doesn't need a grid. A single link doesn't need a button. A one-line note
  doesn't need a callout. Use the plainest thing that reads well.
- **Don't use Details for a group or Accordion for one item.** One collapsible →
  Details (`^^^`). A set of collapsibles → Accordion (`//////`).
- **Don't invent attributes or variants.** `:::caution` is not a callout type;
  `@@@primary` is not a tag variant. Check the component reference — the engines
  silently drop unknown tokens, so a typo just disappears.
- **Don't put Markdown image syntax directly inside a `::::frame`.** Use a raw
  `<img>` tag there (Markdown images may not be processed inside layout
  containers). Elsewhere, Markdown images work normally.
