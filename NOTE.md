## What I picked

Restoring the storefront **data layer** so broken merchant-facing pages work again — starting with the **Bundle Builder** at `/pages/bundle-builder`, which was completely dead (default page template, no products in custom collections).

## Why it's the highest-impact thing here

The Bundle Builder is a core conversion surface: tabbed series picker, tiered bundle discounts, sticky cart. Without it, customers cannot build a set at all. The same seed gap also broke **Series Comparison**, left **custom collection pages empty** (e.g. Mo Series), and cascaded into **wrong PDP breadcrumbs** because products were never linked to their series collections. Fixing the seed restores multiple pages from one root cause.

## What I did

- **Seed — page templates:** Assign `template_suffix` when creating pages so Bundle Builder, Series Comparison, Reviews, Contact, Best Sellers, and Bundles use their custom JSON templates.
- **Seed — collects:** After products and collections are created, assign membership via the Collects API using `series:*` and `knife-type:*` tags (metafields are not seeded).
- **Theme — breadcrumbs:** Classify knives from product tags instead of `custom.isknife` metafield so PDP shows `KNIVES` not `ACCESSORIES`.
- **Theme — recommendations:** Filter the current product out of “You Might Also Like”.
- **Theme — PDP description:** Disable duplicate `detail_content_custom` blurb where the accordion already renders the full description.
- **Theme — reviews page:** Replace pruned Judge.me app block with the native `best-reviews` section (static cards from the homepage).

Re-seeded the dev store and pushed the updated theme to `qyalma-sandbox.myshopify.com`.

## What I'd do next

- **Performance:** Lighthouse pass on homepage and PDP (image preload, defer non-critical JS, carousel lazy-load).
- **Metafields in seed:** Restore `custom.isknife` and spec metafields so theme logic does not rely solely on tags.
- **Judge.me:** Install the app on the dev store or keep the native reviews fallback and style it for the reviews page layout.
- **Full catalog:** Run `--full` seed (237 products) once collection assignment is proven at slim scale.
