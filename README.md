# Cargocicleta Brașov — bike picker

Single self-contained page (`index.html`) that lets a customer pick one of
the 3 cargobikes and book it via its Calendly inline widget. No API key,
no build step, no server — just static HTML/CSS/JS.

## Before going live

Edit the `BIKES` array near the top of the `<script>` in `index.html`:

- `bullitt` and `omnium` already use the real Calendly links found on the
  current carrd.co page.
- `bike3` has a placeholder Calendly URL (`PUNE-LINKUL-AICI`) — replace it
  with the third bike's real Calendly scheduling link, and update its
  `name`/`desc`.
- Optionally set `image` on each bike to a real photo URL; otherwise a
  placeholder tile is generated automatically.

## Behavior

- Each bike is a card; clicking one loads that bike's Calendly booking
  widget inline, below the cards.
- "Nu ești sigur(ă)? Arată-mi toate cele 3 calendare" reveals all three
  widgets behind quick-switch tabs, so a customer can flip between bikes
  if their first choice has no open slot — without leaving the page.
- Fully responsive: cards reflow to a single column below 480px, buttons
  and tabs are sized for touch (≥40px targets), the calendar widget height
  adapts to viewport instead of a fixed 700px, and safe-area insets are
  respected on notched phones.
- Styled to match [rastel.io](https://rastel.io)'s look: dark navy hero
  (`#0b1024`) with a violet glow, deep-violet primary color (`#2f0094`),
  rounded cards, pill buttons/tabs.

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
