# cml. / commonly — website concept

A pitch prototype for Commonly (`cml.`), the coffee and bakery shop in Bang Rak,
Bangkok. Single-page, static, no build step, no dependencies, no framework.
Open `index.html` in a browser, or serve the folder from any static host.

```
Cafe Website/
├── index.html            the concept
├── index-v1-ember.html   an unrelated earlier concept — safe to delete
├── assets/               17 photographs in use (+3 used only by v1)
└── HANDOFF.md            this file
```

`index-v1-ember.html` is a separate earlier design for a fictional London cafe.
It shares `assets/` but uses its own images. To remove it, delete that file plus
`hero-v1.jpg`, `about-interior.jpg`, `gallery-*.jpg` and `menu-*.jpg`.

---

## Read this before the meeting

**The photography is the weak point, and it is worth saying so out loud.**
Every image is licensed stock standing in for the real shop. During this build
three stock photos had to be thrown out after inspection, because wide cafe
shots carry other people's businesses:

- one was a **Blue Bottle Coffee** store — their logo was on the bean bags
- one was an **American street** — US plates, an Uber Eats sticker, Christmas garland
- one had **another cafe's illuminated logo** on the back wall

So the gallery was deliberately rebuilt out of **tight, brand-neutral craft
detail** — an extraction, a group head, beans, a croissant — rather than wide
room shots. It is honest and it looks intentional, but it means **the site has
no picture of their actual room**. That is the natural thing to offer them: a
photo session, or their own photos dropped into the same slots.

If you swap any image in, **look at it at full size first**. Check the back
wall, the cups, the street and the packaging for other people's brands.

---

## What is real, and what is not

Researched from public listings (Wongnai, their Linktree and Instagram bio,
customer posts on Lemon8 and Trip.com):

| | |
|---|---|
| Lowercase `cml.` wordmark | on their glass doors and wooden signage |
| "your everyday drink good coffee here" | their own line, printed on the glass |
| Calico cat | their mascot — on their postcards, and a real one sleeps in |
| Bright white + natural wood | "a small charming space in a glass room" |
| Both branch addresses and hours | Si Wiang and Surawong |
| Phone, LINE, Instagram, TikTok, Linktree | their own published channels, wired live |
| Menu items and baht prices | **approximate** — mixed branches and dates |

**Not real:** all photography (licensed stock, see above).

**Soft spots to check with them directly:**

- Prices mix branches and dates and may be out of date.
- Wongnai lists Si Wiang as Mon–Sat; their Instagram bio says daily. The bio is
  used here.
- No hex colors, logo vector or official site were found — the palette is
  interpreted from photographs, not from a brand guide.
- Their GrabFood deep link has expired, so the delivery button points at their
  Linktree instead.
- The `filter / single origin` row shows "ask" rather than a price, and light
  roast carries a +฿5 surcharge. Confirm both.

---

## Two places that must be edited together

Each hours `<tr>` carries `data-o` / `data-c` in 24-hour decimal (`6.5` = 06:30),
where `data-c="0"` means closed. These drive the per-branch Open/Closed pill and
the "today" highlight. The visible text is separate — change both, or the pill
will contradict the table.

```html
<tr data-o="6.5" data-c="16"><th scope="row">Mon – Fri</th><td>06:30 – 16:00</td></tr>
```

The row label is parsed to find today, so it must stay recognizable —
`Mon – Fri`, `Sat – Sun`, `Saturday`, `Sunday`. A label like "Weekdays" will not
match and the pill falls back to "See hours".

---

## Before it goes live

- [ ] Real photography, especially the room and the storefront
- [ ] Confirm every price and both sets of hours with the shop
- [ ] Swap the Linktree delivery link for a live GrabFood link
- [ ] Make `og:image` an absolute URL — relative paths break when shared
- [ ] Add a canonical URL
- [ ] Self-host the two Google Fonts if third-party requests are a concern
- [ ] Consider a Thai-language version. Their own signage is English-only, but
      their customers are not.

---

## How it is built

**Type.** Instrument Serif for display, Hanken Grotesk for everything else, both
from Google Fonts. Headings are lowercase throughout to match the `cml.` wordmark.

**Color.** Custom properties on `:root` — change them in one place:

| Token | Value | Use |
|---|---|---|
| `--shell` | `#faf8f4` | page background, warm off-white |
| `--sand` | `#f1eade` | the menu block |
| `--wood` / `--wood-deep` | `#c3a074` / `#9a7b55` | rules, kickers, accents |
| `--ink` | `#2c2926` | text — a soft near-black, not pure black |
| `--calico` | `#d2743c` | the cat, and every interactive highlight |
| `--bark` | `#332e28` | footer |

**Layout.** The hero is an asymmetric split — type on cream at left, photo
bleeding off the right — rather than a full-bleed image under a dark scrim,
because the shop's own character is bright and glass-walled. The hero carries a
top offset so the fixed header always sits over cream and never over the photo.

**Motion.** CSS only, disabled under `prefers-reduced-motion: reduce`.

**Menu photo previews.** Hovering a row floats a card that eases after the
cursor; tabbing anchors it beside the row instead; touch makes it tap-to-toggle.
The card is clamped so it cannot run off-screen, and images are prefetched on
idle so the first hover is instant.

**Accessibility.** Skip link, visible focus rings, labelled landmarks, real
`<th scope="row">` in both hours tables, alt text on every image, and menu rows
are `<button>`s so they are keyboard reachable. Scroll reveals are gated behind
a `.js` class — if the script fails the page stays fully readable instead of
sitting invisible at `opacity: 0`.

---

## Verified

Rendered and visually checked at 1440px desktop and at a true 390px phone
viewport, including the open mobile nav and both Open/Closed pills. Structural
checks pass: every image path resolves, tags balance, the JavaScript parses,
every image has alt text, and no asset is orphaned.

Not checked: real iOS or Android hardware, and any browser other than Chrome.
