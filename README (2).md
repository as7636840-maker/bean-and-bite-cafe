# ☕ Bean & Bite — Landing Page

A single self-contained file: `bean-and-bite-landing-page.html`. No build step, no dependencies to install — open it or upload it and it works.

## Preview it

Double-click the file to open it in any browser, or drag it into a browser window. Everything (HTML, CSS, JS, and the product illustration) lives in that one file, except for the Cairo/Tajawal fonts, which load from Google Fonts over the internet.

## Deploy it

Upload `bean-and-bite-landing-page.html` to any static host and rename it to `index.html` at the root (or point your domain at it directly). It works as-is on Netlify, Vercel, GitHub Pages, Cloudflare Pages, or a plain web server — no server-side code required.

## What's inside

| Section | What it does |
|---|---|
| Header | Sticky logo bar with a small "اطلب الآن" button |
| Hero | Headline, subheadline, main CTA, the four trust chips, and the product illustration |
| Why Choose Us | The two feature cards (coffee, cake) |
| Offer ticket | The discount package, price, and the daily countdown |
| Checkout form | Name / phone / address, validation, and the confirm button |
| Sticky mobile bar | Appears once you scroll past the hero on phones, hidden on desktop |

## The most common edits

**Price.** Search for `price-old` and `price-new` in the HTML — the two numbers sit right next to each other near the offer ticket.

**Copy.** All Arabic text is plain text inside the HTML, not generated — search for the phrase you want to change.

**Colors.** Everything pulls from the `:root` block at the top of the `<style>` section (`--coffee`, `--gold`, `--beige`, etc.). Change a value there and it updates everywhere that color is used.

**Countdown.** Right now it counts down to midnight and restarts daily, so it never looks "expired" after launch. To make it count down to a fixed end date instead, find `tickCountdown()` in the script and replace the `end.setHours(23,59,59,999)` line with a fixed date, e.g. `var end = new Date('2026-07-15T23:59:59');`.

**Product illustration.** It's hand-drawn inline SVG (inside `.hero-visual`), so there's no image file to swap. If you'd rather use real product photography, replace that `<svg>...</svg>` block with an `<img src="..." alt="...">` tag.

## Connecting the order form to something real

Right now, submitting the form simulates a network request (a 1.4-second delay) and then shows the success message — nothing is actually sent anywhere yet. In the script, look for this comment inside the `submit` handler:

```js
// NOTE: replace this simulated delay with a real request to your
// order-processing endpoint, e.g.:
// fetch('/api/orders', { method:'POST', body: new FormData(form) })
```

Swap the `window.setTimeout(...)` block for a real `fetch()` call to wherever you want orders to land — your own backend, a Google Sheet via Apps Script, Airtable, a WhatsApp Business API webhook, Zapier/Make, etc. Keep the `.then()`/success logic the same so the success state still shows correctly.

## Notes

- No frameworks, no npm install, no build process — it's vanilla HTML/CSS/JS on purpose, so it stays fast and easy to host anywhere.
- The page respects `prefers-reduced-motion`, so animations turn off automatically for visitors who've requested that at the OS level.
- Phone validation currently expects Egyptian mobile numbers (`01` + 9 digits). If you're running ads elsewhere, update the regex in the `validators.phone` function in the script.
