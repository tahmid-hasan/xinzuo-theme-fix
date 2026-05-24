## What I picked

I went after the **Bundle Builder** first (`/pages/bundle-builder`). On the live store it was basically a blank page — just the title, no tabs, no products. That felt like the biggest thing broken for a customer actually trying to buy.

## Why it's the highest-impact thing here

The Bundle Builder is where someone builds a knife set and gets a bundle discount. Without it, that whole flow is gone. When I dug in, the Liquid and JS were already there — the problem was what gets created when you seed the dev store. Pages weren't getting the right template, and custom collections like Mo Series had no products in them. Same root issue was also killing Series Comparison, empty collection pages, and messy breadcrumbs on product pages.

## What I did

I fixed the seed script in two steps: pages now get the correct `template_suffix` (so Bundle Builder and Series Comparison use their real templates), and products get added to custom collections through the Collects API based on their tags.

On the theme side I cleaned up a few things that only showed up because the seed data was incomplete — breadcrumbs now treat knives as knives (tags instead of a metafield that never got seeded), recommendations no longer suggest the product you're already on, I removed a duplicate description on the PDP, and the reviews page uses the built-in best-reviews section since Judge.me gets stripped on push anyway.

Re-seeded the store and pushed the theme to `qyalma-sandbox.myshopify.com`.

## What I'd do next

I'd run Lighthouse on the homepage and a PDP, seed metafields properly so the theme doesn't need tag workarounds, and either wire up Judge.me or polish the native reviews page. Full catalog seed if there's time.
