# Asos Supply Chain Audit — Data Science Project

A personal data science project that approaches the fashion retailer **Asos** from the outside, the way a data consultant would: take available product data, look for what's missing, and surface opportunities the company might be leaving on the table.

## Project Idea

What can the _public_ product pages still tell us about how well their supply chain is running?

For example, when a size is marked _Out of stock_ on a product page, that's a customer who wanted to buy and couldn't. Aggregating that signal across thousands of products gives a rough but useful estimate of **phantom revenue**: money lost to stockouts.

## Dataset

- `products_asos.csv` — ~18k scraped product rows
- Columns include `url`, `name`, `size`, `category`, `price`, `color`, `sku`, `description`, `images`

## Approach

1. **Clean** the price column (force numeric, drop malformed rows).
2. **Extract brand** from the description field using the _"Category by Brand ..."_ pattern.
3. **Map and filter** brand names (fix multi-word brands, drop ones with too few products).
4. **Quantify stockouts** by counting _Out of stock_ mentions in the `size` column and computing a per-product stockout rate.
5. **Estimate lost revenue** as `price × stockout_count`.
6. **Visualize brand strategy** on a price vs. stockout-rate scatter plot, with bubble size = total lost revenue, to spot the high-opportunity quadrant.

## Files

- [Asos_analysis.ipynb](Asos_analysis.ipynb) — analysis with expanded markdown explanations for each section
- `products_asos.csv` — raw scraped dataset

## Running It

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install pandas matplotlib seaborn jupyter
jupyter notebook Asos_analysis_documented.ipynb
```
