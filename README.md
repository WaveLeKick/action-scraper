[Action Scraper](https://apify.com/appealing_jingle/action-scraper?fpr=data)

# Action.com Product Scraper

A Playwright-based scraper built with [Crawlee](https://crawlee.dev) for extracting product data from **Action.com** across multiple languages and categories.

It supports pagination, structured output, and configurable sorting.

In case of errors, bugs or feature requests please contact me: [0994try@gmail.com](mailto:0994try@gmail.com)

---

## Features

- Extracts key product information:

- Title
- Description
- Price
- Price description (e.g., per unit, per kg)
- Product URL
- Product image (clean URL)
- Category
- Works with **Action.com** across multiple country versions: `sk`, `nl`, `fr`, `de`, `pl`, `cs`, `it`, `es`.
- Allows filtering by **categories** and **sorting** (e.g., price ascending, descending).
- Handles **pagination** automatically.
- Outputs data into the **Apify Dataset** (JSON, CSV, Excel, etc.).

---

## Extracted Data Example

```
{
  "title": "Svetelná reťaz",
  "description": "20 LED svetiel | 1 m",
  "price": "0.64",
  "priceDescription": "0.64 €/ks",
  "url": "https://www.action.com/sk-sk/p/2535965/svetelna-retaz/",
  "imageUrl": "https://asset.action.com/image/upload/t_digital_product_image/w_1920/17828940.webp",
  "category": "week deals"
}
```