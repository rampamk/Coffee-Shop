# cml. / commonly

A one-page website concept for Commonly (`cml.`), a coffee and bakery shop in Bang Rak, Bangkok. It is plain HTML and CSS with a small inline script. There is no build step, framework or dependency.

## Sections

- **Hero**: wordmark and tagline
- **Story**: about the shop
- **Menu**: drinks and bakery with approximate baht prices. Hovering a row shows a photo preview.
- **Gallery**: close-up coffee and bakery photos
- **Visit**: both branches (Si Wiang and Surawong) with addresses, opening hours, a live Open/Closed pill and contact links

## Run locally

From this folder, start any static server and open the URL it prints:

```sh
python3 -m http.server 8000
```

Then visit <http://localhost:8000>. You can also open `index.html` directly in a browser.

## Project structure

```
Cafe Website/
├── index.html    markup, styles (inline <style>) and script
├── assets/       photographs
├── HANDOFF.md    notes on content accuracy, design decisions and launch checklist
├── CLAUDE.md     project instructions
└── README.md
```

## Editing

- **Colors**: change the custom properties on `:root` in `index.html` (`--shell`, `--sand`, `--wood`, `--ink`, `--calico`, `--bark`).
- **Hours**: each hours `<tr>` has `data-o` and `data-c` attributes (24-hour decimal, so `6.5` is 06:30, and `data-c="0"` means closed). They drive the Open/Closed pill and the "today" highlight. Update them together with the visible text.
- **Row labels**: keep labels like `Mon – Fri`, `Sat – Sun`, `Saturday` and `Sunday`. The script parses them to find today.
- **Images**: replace files in `assets/` and check each at full size for other businesses' branding first.

## Notes

- Fonts (Instrument Serif and Hanken Grotesk) load from Google Fonts, so the page needs internet access to show them as designed.
- All photography is licensed stock standing in for the real shop. Prices and hours are approximate and need confirming with the shop.
- See [HANDOFF.md](HANDOFF.md) for the full list of open items before launch.
