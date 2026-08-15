# Cargocicleta Brașov — bike picker

Single self-contained page (`index.html`) that lets a customer pick one of
the 3 cargobikes and book it — each card links straight to that bike's
Calendly scheduling page. No API key, no build step, no server — just
static HTML/CSS/JS.

## Before going live

Edit the `BIKES` array near the top of the `<script>` in `index.html`:

- All three bikes already have their real Calendly links.
- `image` is a path relative to `index.html` (e.g. `images/bullitt.jpg`).
  Drop the photo files in the `images/` folder with matching names; a bike
  with an empty `image` gets an auto-generated placeholder tile instead.

## Behavior

- Each bike is a card (image, name, short description, "Rezervă" button);
  tapping/clicking anywhere on an available bike's card navigates straight
  to that bike's Calendly page — no intermediate step, no embedded widget.
- On phones (≤480px wide), the cards become a full-width, one-at-a-time
  horizontal swipe carousel — Bullitt → Omnium → Tricicletă cargo, left to
  right. On wider screens they sit in a multi-column grid.
- Styled to match [rastel.io](https://rastel.io)'s look: dark navy hero
  (`#0b1024`) with a violet glow, deep-violet primary color (`#2f0094`),
  rounded cards, pill buttons.

## Marking a bike out of service

Edit `status.json` (sits next to `index.html`) — no need to touch the page
itself:

```json
{
  "unavailable": ["bike3"]
}
```

List whichever bike ids (`bullitt`, `omnium`, `bike3` — matching each
bike's `id` in the `BIKES` array) are currently broken/in maintenance.
Empty array = all 3 bookable. The page fetches this file on every load, so
updating it on GitHub takes effect immediately, no redeploy of `index.html`
needed.

An unavailable bike still shows on the page (greyed out, "Indisponibilă
momentan") rather than disappearing, so customers know it exists but can't
click it.

This used to be a `?unavailable=...` URL param, but that's visible and
editable by anyone in the address bar — a customer could just delete it
to make a broken bike look bookable again. `status.json` isn't part of the
URL a visitor sees or is invited to edit, so it's not something a casual
visitor stumbles into changing.

**Important limit:** greying out a bike here only changes what this page
*displays*. It does **not** stop someone from booking directly at that
bike's raw Calendly link (e.g. by finding it in browser history, or if it's
still linked anywhere else). This page has no server and can't enforce
anything — it's just a nicer front door. To actually prevent bookings for
a broken bike, pause its event type in Calendly itself (Calendly dashboard
→ that event type → toggle it off) whenever you add it to `unavailable`.

## Hosting / embedding under carrd.co

Carrd itself can't host multi-section custom HTML/JS on a free plan, so
pick one of:

1. **Host this file separately** (GitHub Pages, Netlify, Vercel, Cloudflare
   Pages — all free for a static file) and point a Carrd **Button/Link**
   element at that URL, e.g. "Rezervă acum" → `https://your-username.github.io/cargocicleta/`.
2. **Paste it into a Carrd "Embed → Code" element** (requires a Carrd Pro
   plan) if you want it to live directly inside the existing carrd.co
   page instead of linking out.

Option 1 is the simplest and keeps the current carrd.co page as-is; you'd
just swap its two bike links for one link to this page.
