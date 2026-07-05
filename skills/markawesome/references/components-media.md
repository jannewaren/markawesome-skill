# Media & date components

Carousel · Comparison · Video · Video playlist · Format date · Relative time

## Carousel

An image slider or content rotator with navigation — a gallery or step-by-step
visual slides.

- **Primary:** `~~~~~~params?` (**6 tildes**)
- **Alt:** `:::wa-carousel params?`
- Separate slides with `~~~` (**3 tildes**). Close with `~~~~~~`.

**Parameters** (order-independent):

- `navigation` — prev/next arrows.
- `pagination` — dot indicators.
- `loop` — infinite loop.
- `autoplay` — auto-advance; `autoplay-interval:value` sets the ms between
  advances (e.g. `5000`; default `3000`).
- `mouse-dragging` — drag to slide.
- `vertical` — vertical orientation.
- `scroll-hint:value` — peek of the next slide.
- `aspect-ratio:value` — e.g. `16/9`, `4/3`.
- `slide-gap:value` — gap between slides.
- `slides-per-page:n` — slides visible at once.
- `slides-per-move:n` — slides advanced per move.

```
~~~~~~navigation pagination loop autoplay autoplay-interval:5000
~~~
![Dashboard](/img/slide-1.png)
~~~
~~~
![Reports](/img/slide-2.png)
~~~
~~~~~~
```

## Comparison

A before/after image comparison with a draggable slider. Requires **exactly two
images**.

- **Primary:** `|||position?`
- **Alt:** `:::wa-comparison position?`
- Close with `|||`. First image → `before` slot; second image → `after` slot.
- Optional `position` (0–100) sets the initial slider position.

```
|||40
![Before](/img/before.jpg)
![After](/img/after.jpg)
|||
```

## Video (Web Awesome Pro)

Embed a single video as `<wa-video>`. **Requires a Web Awesome Pro kit** and is
experimental.

- **Primary:** `;;;controls:? preload:? flags?`
- **Alt:** `:::wa-video controls:? preload:? flags?`
- Close with `;;;`.

**Body:** the first Markdown link `[Title](src)` supplies the video `title` and
`src`; the first Markdown image `![alt](poster)` supplies the `poster`. A block
with **no link (no `src`) is left untransformed**.

**Parameters** (order-independent; invalid enum values dropped):

- `controls:none|standard|full` — controls preset (default `standard`).
- `preload:auto|metadata|none` — how the browser preloads (default `metadata`).
- `autoplay`, `autoplay-muted`, `autoplay-on-visible`, `loop`, `muted`.

```
;;;controls:full
[Product tour](/media/tour.mp4)
![Poster](/media/tour-poster.jpg)
;;;
```

v1 emits a single `src` (no `<source>`/`<track>` children yet). For a navigable
set of videos, use a Video playlist.

## Video playlist (Web Awesome Pro)

Group multiple videos into `<wa-video-playlist>` with navigation. **Pro**,
experimental.

- **Primary:** `;;;;;;controls:?` (**6 semicolons**)
- **Alt:** `:::wa-video-playlist controls:?`
- Wrap each video in a bare `;;;` … `;;;` item between the `;;;;;;` fences (mirrors
  the carousel `~~~`/`~~~~~~` structure). Each item follows the same body rules as
  a single Video.

**`controls:none|standard|full`** sets the preset for the whole playlist (default
`full`); it is forwarded to every child, so the children omit their own
`controls`.

```
;;;;;;controls:standard
;;;
[Part 1 — Intro](/media/part1.mp4)
![Poster](/media/part1.jpg)
;;;
;;;
[Part 2 — Setup](/media/part2.mp4)
;;;
;;;;;;
```

## Format date

An absolute, locale-formatted date baked in at build time (`<wa-format-date>`).
The browser formats it via `Intl.DateTimeFormat`. Works **inline** or as a block.

- **Inline primary:** `[[[date style:preset? time:preset? granular? lang:locale?]]]`
- **Block alt:** `:::wa-format-date date style:preset? …` (empty body, close `:::`).

**The date** is an ISO 8601 date (`2026-06-26`) or datetime with a `T`
(`2026-06-26T14:30:00Z`). Omit it to show the viewer's current time.

**Presets:** `style:short|medium|long|full` and `time:short|medium|long|full`
expand to granular attributes. A bare date defaults to `style:long`; `time:`
without a date style emits time-only.

**Granular overrides** (win over presets, rightmost wins): `weekday`, `era`,
`year`, `month`, `day`, `hour`, `minute`, `second` (each an `Intl` value), plus
`hour-format:auto|12|24`, `time-zone-name:short|long`, `time-zone:IANA`, and
`lang:` / `locale:` for the locale. Unknown tokens and invalid enum values are
silently dropped.

```
Published [[[2026-06-26 style:long]]].
```

```
:::wa-format-date 2026-06-26 style:full lang:fr
:::
```

## Relative time

A relative "3 days ago"-style phrase, optionally live-ticking
(`<wa-relative-time>`, via `Intl.RelativeTimeFormat`). Works **inline** or as a
block.

- **Inline primary:** prefix the date with `relative` —
  `[[[relative date format:? numeric:? sync? lang:?]]]`.
- **Block alt:** `:::wa-relative-time date format:? numeric:? sync?` (close `:::`).

**Parameters:**

- `format:long|short|narrow` — phrasing width (default `long`).
- `numeric:auto|always` — `auto` allows "yesterday"/"tomorrow"; `always` forces
  "1 day ago" (default `auto`).
- `sync` — keep the phrase ticking live as time passes.
- `lang:` / `locale:` — the locale.

Date-formatting tokens (`style:`, `time:`, `month:`, …) are ignored in relative
mode.

```
Updated [[[relative 2026-06-20]]].
```

```
:::wa-relative-time 2026-06-20 sync
:::
```

> **Static-site caveat (Format date & Relative time):** like `<wa-icon>`, both
> render generated text into shadow DOM with **no light-DOM fallback** — with Web
> Awesome's JavaScript disabled they show nothing. See `authoring.md`.
