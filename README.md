# Family Kitchen Index

A single-page recipe reference: nine easy, batch-friendly family recipes with links
to trusted sources and a tap-to-check ingredient list per recipe. Amounts show the
original recipe unit first with SI in parentheses (weight preferred for dry
cup/spoon measures).

## Publish with GitHub Pages

The site is a single static `index.html` — no build step needed.

1. Create a repo (e.g. `family-recipes`) and push these files to the `main` branch.
2. In the repo: **Settings → Pages → Source: Deploy from a branch → main / root**.
3. The site goes live at `https://<username>.github.io/family-recipes/` within a minute or two.

Or with the GitHub CLI:

```bash
gh repo create family-recipes --public --source=. --push
gh api repos/{owner}/family-recipes/pages -X POST \
  -f "source[branch]=main" -f "source[path]=/"
```

## Editing

Each recipe is an `<article class="ticket">` block in `index.html`. Copy one,
change the title, links, and list items to add a recipe. Checked ingredient-list
items persist in the browser via localStorage.

Every recipe gets a "Copy link" button and a URL anchor derived from its title
(e.g. `#carne-asada`), so new recipes are shareable automatically. Opening a
shared link scrolls to that recipe with its sections expanded.

Ingredients with `data-base` / `data-unit` on their `<label class="item">` are
tap-to-scale: entering how much you have rescales the whole recipe live to the
most limiting ingredient (e.g. `data-base="500" data-unit="g"`). Leave the
attributes off non-scalable rows (to-taste items, equipment).

Recipes are listed alphabetically and filtered by tags rather than grouped:
give each `<article>` metadata like `data-cuisine="mexican" data-course="main"
data-protein="beef" data-traits="batch high-protein"`. Filter chips and card
pills are generated from these attributes, and the ingredient filter box
matches the actual ingredient rows. Keep new recipes in alphabetical order
within the single `.cards` list.
