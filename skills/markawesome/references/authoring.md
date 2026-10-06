# Authoring conventions & caveats

Cross-cutting rules that apply to every component. Read this once; it explains the
mechanics the per-component references assume.

## Dual syntax: primary shorthand vs. `:::wa-*` alternative

Every component accepts two equivalent spellings:

- **Primary** — the terse delimiter: `:::info`, `===`, `@@@brand`, `%%%`, `^^^`,
  `//////`, `++++++`, `&&&`, `(((…)))`, `[[[…]]]`, `::::grid`.
- **Alternative** — an explicit `:::wa-component` (or `::::wa-layout`) form:
  `:::wa-callout info`, `:::wa-card`, `:::wa-tag brand`, `::::wa-grid`.

**Default to the primary shorthand.** Reach for the `:::wa-*` form only when the
shorthand would be ambiguous or hard to read in context — for instance when a line
could be mistaken for something else, or when a reviewer benefits from the
component name spelled out. Both produce identical HTML; the choice is purely
readability.

## Markdown renders inside component bodies

The body of a component (a callout, a card, a tab panel, an accordion item, a
dialog, a details block) is **full Markdown** — headings, lists, links, emphasis,
inline code, even other components all work inside. Only the *inner* content of
components is rendered; the surrounding page Markdown is left for your site's own
Markdown processor.

Exceptions where the body is **plain text, not Markdown**:

- **Tooltip** tip content is plain text (HTML-escaped); `\n` becomes `<br>`.
- **Tree** labels are plain text (a leading `icon:name` token aside).

## The `>>>` separator

`>>>` on its own splits a **trigger from its body** inside these blocks:

- **Details** (`^^^`) — summary `>>>` content.
- **Dialog** (`???`) — trigger-button text `>>>` dialog content.
- **Popover** (`&&&`) — trigger `>>>` content (inline form too:
  `&&&trigger >>> content&&&`).
- **Tooltip** (`(((…)))`) — anchor `>>>` tip.
- **Random content** (`......`) — separates each option from the next.

It only has meaning **inside** one of those blocks. Elsewhere `>` is an ordinary
Markdown blockquote. The **Stepper** fence `>>>>>>` (six chevrons) is a separate
delimiter and never acts as a separator.

## Image & link auto-detection in cards

A card (`===`) reads its body positionally — you don't name slots:

- First **Markdown image** → the media slot.
- First **bold line** (`**Title**`, *not* a `#` heading) → the header slot.
- A **trailing Markdown link** on its own line → a footer button.
- Everything else → the body.

Buttons (`%%%`) and videos (`;;;`) similarly pick up a Markdown link in their body
to become clickable / sourced. See the per-component references for specifics.

## Code fences are protected

Anything inside a fenced ``` code block is **not** transformed — the engines
replace fenced blocks with placeholders before running, then restore them. So to
show Markawesome syntax literally in documentation, put it in a fenced block (as
this skill's references do). Inline code (`` `like this` ``) is likewise safe.

## Front matter is SSG-specific

Markawesome transforms the Markdown **body**, not the YAML front matter. How front
matter works — permalinks, layouts, collections, data — is defined by your static
site generator, not by Markawesome:

- **Jekyll** (via `jekyll-webawesome`) — Jekyll/Liquid front matter and layouts.
- **Eleventy** (via `eleventy-plugin-webawesome`) — Eleventy front matter and
  templating.

Author the component syntax in the body; leave front-matter conventions to the
host SSG's own docs.

## Web Awesome version pin: 3.14.0

The ecosystem's examples sites pin **Web Awesome 3.14.0** in their CDN URLs, and
this skill's attribute vocabulary (icon families, animations, the `xs–xl` size
scale, canvas sizing) matches that release. If a project pins a different Web
Awesome version, some newer families/animations may not exist there — validate
against the version the site actually loads.

## Static-safety & Pro caveats

Most components are **declarative and static-site-safe** — they render correctly
with only the Web Awesome library on the page and no JavaScript of your own.
Know the exceptions:

- **Web Awesome Pro required:** Video (`;;;`) and Video playlist (`;;;;;;`) emit
  `<wa-video>` / `<wa-video-playlist>`, which are Pro (and experimental). They do
  nothing on a free kit.
- **No light-DOM fallback (needs Web Awesome's JS to show anything):** Icon
  (`$$$` / `:::wa-icon`), Format date (`[[[…]]]`), and Relative time
  (`[[[relative …]]]`) render generated content into shadow DOM. With Web
  Awesome's JavaScript disabled they show nothing.
- **Fires an event but doesn't act on its own:** a Tag's `with-remove` × button
  fires `wa-remove` but doesn't remove the tag without your listener.
- **Declarative-safe but note the runtime quirk:** Tree (`||||||`) expands only
  top-level branches on load (WA 3.9.0). Random content (`......`) and Accordion
  (`//////`) are stable in Web Awesome (since 3.13.0) and fully declarative here.
- **Experimental but declarative:** Stepper (`>>>>>>`) emits `<wa-stepper>`,
  experimental in Web Awesome 3.14.0. It is display-only here (no click-to-navigate),
  so it needs no JavaScript of your own.

When a page must work with scripting disabled, prefer the declarative-safe
components and avoid the shadow-DOM-only ones for essential content.

## The lockstep guarantee

The **markawesome** (Ruby) and **markawesome-js** (Node) engines accept
byte-for-byte identical input. Everything in these references works in both, so a
document authored for a Jekyll site transforms identically on an Eleventy site.
Never emit a delimiter or attribute that only one engine supports — if it isn't in
these references, don't use it.
