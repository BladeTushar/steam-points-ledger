# Steam Points Ledger

A single static page (`index.html`, no build step) that calculates Steam Points
earned per purchase in any country's currency.

## Why there's no hardcoded "points table"

Steam's own rule (store.steampowered.com/points/howitworks) is:

1. Whatever you spend is converted to USD.
2. You earn a flat **100 Points per $1.00** of that USD value.

Because step 1 runs through a currency conversion, the "points per 100 rupees"
or "points per 1 euro" figure isn't a fixed constant Valve publishes per
country — it's a byproduct of the exchange rate at the time, which drifts
daily. So instead of hardcoding numbers that go stale, this page pulls a live
USD exchange-rate feed (open.er-api.com, free, no API key) in the browser and
computes the rate for every country on the fly.

This means figures here are **close estimates**, not Valve's exact internal
conversion (Valve updates its own regional pricing/currency tables on its own
schedule, not tick-by-tick), but they track real-world currency movement far
better than a static table would.

## Deploy

### GitHub Pages
1. Push this folder to a GitHub repo.
2. Repo Settings → Pages → Deploy from branch → select `main` (or your
   default branch) and `/ (root)`.
3. Your site will be live at `https://<username>.github.io/<repo>/`.

### Vercel
1. `npm i -g vercel` (or use the Vercel dashboard "Import Project").
2. From this folder: `vercel --prod`.
3. No framework/build settings needed — it's a static `index.html`.

## Editing the country list

Countries and their real-world currency live in the `COUNTRIES` array near
the top of the `<script>` block in `index.html`. Steam's own supported
billing currencies are in `STEAM_CURRENCIES` — anything not in that set falls
back to EUR (for European countries) or USD, matching Valve's documented
behavior for unsupported regions.
