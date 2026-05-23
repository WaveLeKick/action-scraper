[Action Scraper](https://apify.com/studio-amba/action-scraper?fpr=data)

# Action Scraper -- Europe's Biggest Discount Retailer at Your Fingertips

Scrape products, prices, deals, and availability from Action.com across 16 European locales. From household essentials to seasonal bargains, extract Action's entire catalog of affordable goods in structured JSON.

## What is Action Scraper?

Action is Europe's fastest-growing non-food discount retailer, operating over 2,500 stores in 12 countries. Their product range rotates constantly, with new items arriving weekly at rock-bottom prices. This scraper gives you programmatic access to that data.

Here's what people use it for:

- **Price monitoring at scale** -- Track Action's notoriously volatile pricing across Belgium, Netherlands, France, Germany, and 12 other markets. Spot when your competitor's products drop below the euro threshold.
- **Product discovery** -- Action's assortment changes weekly. Automated scraping catches new arrivals before they sell out, whether you're a reseller, a deal blogger, or just curious.
- **Cross-border price comparison** -- The same item can cost differently in Action Belgium vs Action France. Compare prices across all 16 locales in a single run.
- **Discount & deal tracking** -- Action's "deals" and "new arrivals" rotate fast. Build alerts for specific categories or price drops.
- **Retail competitive intelligence** -- If you sell household goods, DIY supplies, or seasonal items, Action's pricing sets the floor. Know what that floor is.

## What data does Action Scraper extract?

Every product comes with a rich set of fields:

- 🏷️ **Product name** and description
- 💰 **Current price** and original price (when on sale)
- 📊 **Price per unit** (e.g., "EUR 0.50/L")
- 🏪 **Stock status** -- in stock or not
- 🆕 **New arrival flag** -- freshly added items
- 🔥 **Deal flag** -- currently discounted
- 🖼️ **Product images** -- main image + all gallery images
- 📂 **Category breadcrumbs** -- full category hierarchy
- 🔢 **SKU and product ID** -- unique identifiers
- 💱 **Currency** -- EUR for most markets
- 🌍 **Language/locale** -- which country site the data came from

## How to scrape Action.com

The scraper supports three input modes. Pick the one that fits your use case.

### Search by keyword

Find products matching a search term. Good for targeted extraction.

```
{
    "searchQuery": "lamp",
    "locale": "nl-be",
    "maxResults": 50
}
```

### Browse by category or product URL

Pass one or more Action.com URLs -- category pages or individual product pages.

```
{
    "startUrls": [
        { "url": "https://www.action.com/nl-be/c/wonen/verlichting/" }
    ],
    "maxResults": 200
}
```

### Full catalog scrape

Enable `scrapeFullCatalog` to grab every product from the sitemap. Action carries roughly 5,500 products per locale. This ignores `startUrls` and `searchQuery`.

```
{
    "scrapeFullCatalog": true,
    "locale": "nl-nl",
    "maxResults": 5500
}
```

### Locale options

Action operates in 16 locales. Set the `locale` field to target a specific country:

| Locale | Country |
| --- | --- |
| `nl-be` | Belgium (Dutch) |
| `fr-be` | Belgium (French) |
| `nl-nl` | Netherlands |
| `fr-fr` | France |
| `de-de` | Germany |
| `de-at` | Austria |
| `pl-pl` | Poland |
| `cs-cz` | Czech Republic |
| `es-es` | Spain |
| `it-it` | Italy |
| `fr-lu` | Luxembourg |
| `pt-pt` | Portugal |
| `sk-sk` | Slovakia |
| `ro-ro` | Romania |
| `hr-hr` | Croatia |
| `de-ch` / `fr-ch` | Switzerland |

**Tip:** Run the same search across multiple locales to compare regional pricing. Action's assortment and pricing vary significantly between countries.

## Output

Each product is returned as a JSON object. Here is a realistic example from Action Belgium:

```
{
    "name": "LED bureaulamp met flexibele arm",
    "brand": "",
    "price": 4.29,
    "currency": "EUR",
    "url": "https://www.action.com/nl-be/p/3254891/led-bureaulamp-met-flexibele-arm/",
    "scrapedAt": "2025-04-03T10:30:00.000Z",
    "originalPrice": 5.95,
    "pricePerUnit": "EUR 4,29/stuk",
    "sku": "3254891",
    "productId": "prod-3254891",
    "inStock": true,
    "isNew": false,
    "isDeal": true,
    "imageUrl": "https://asset.action.com/image/upload/t_digital_product_image/w_640/led-bureaulamp.webp",
    "imageUrls": [
        "https://asset.action.com/image/upload/t_digital_product_image/w_640/led-bureaulamp.webp",
        "https://asset.action.com/image/upload/t_digital_product_image/w_640/led-bureaulamp-2.webp"
    ],
    "description": "Handige LED bureaulamp met flexibele arm en USB-aansluiting. Geschikt voor op kantoor of in de slaapkamer.",
    "category": "Wonen > Verlichting",
    "categories": ["Wonen", "Verlichting", "LED bureaulamp met flexibele arm"],
    "language": "nl"
}
```

## How much does it cost?

Action Scraper runs on the Apify platform. You pay only for compute and proxy usage.

| Scenario | Estimated cost |
| --- | --- |
| 100 products (search or category) | ~$0.01 |
| 500 products (multiple categories) | ~$0.03 |
| Full catalog (~5,500 products) | ~$0.25 |
| Full catalog + proxy | ~$0.50 |

The scraper uses CheerioCrawler (no browser needed), so compute costs stay minimal. Proxy is optional but recommended for large runs.

## Can I integrate?

Apify integrates natively with the tools you already use:

- **Google Sheets** -- push scraped data directly into a spreadsheet
- **Webhooks** -- trigger your pipeline when a run finishes
- **Zapier / Make** -- connect Action data to 5,000+ apps
- **Slack** -- get notified about new deals or price drops
- **Amazon S3 / Google Cloud Storage** -- export datasets to cloud storage
- **PostgreSQL / MySQL** -- store results in your own database

## Can I use it as an API?

Yes. Call Action Scraper programmatically from any language.

### Python

```
from apify_client import ApifyClient

client = ApifyClient("YOUR_API_TOKEN")

run = client.actor("studio-amba/action-scraper").call(run_input={
    "searchQuery": "stofzuiger",
    "locale": "nl-be",
    "maxResults": 25,
})

for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print(f"{item['name']} -- EUR {item['price']}")
```

### JavaScript

```
import { ApifyClient } from 'apify-client';

const client = new ApifyClient({ token: 'YOUR_API_TOKEN' });

const run = await client.actor('studio-amba/action-scraper').call({
    searchQuery: 'stofzuiger',
    locale: 'nl-be',
    maxResults: 25,
});

const { items } = await client.dataset(run.defaultDatasetId).listItems();
items.forEach(item => console.log(`${item.name} -- EUR ${item.price}`));
```

## FAQ

**Does this scraper work without a proxy?**
Yes. Action.com is accessible via got-scraping's TLS fingerprinting without a proxy. However, for full catalog scrapes or high-frequency runs, a proxy improves reliability.

**How often does Action update their product catalog?**
Action adds new products weekly and rotates seasonal items frequently. Running the scraper daily or weekly captures most changes.

**Can I scrape multiple countries in one run?**
The `locale` field applies to a single run. To compare across countries, run the scraper once per locale. You can orchestrate this with the Apify API or scheduler.

**What happens if a product is out of stock?**
Out-of-stock products still appear in results with `inStock: false`. This is useful for tracking availability over time.

**Does the scraper handle pagination automatically?**
Yes. For search and category pages, pagination is followed automatically until `maxResults` is reached.

**Why are some product descriptions empty?**
Action's category and search pages include product data via React Server Components. Not all fields are present in the RSC payload. For full descriptions, the scraper falls back to product detail pages when using the sitemap mode.

## Limitations

- Action.com uses Cloudflare protection. While the scraper handles this via TLS fingerprinting, very aggressive scraping patterns may trigger rate limiting.
- Product availability data reflects online stock, not individual store inventory.
- Some fields (like `pricePerUnit`) are only available for certain product types.
- The `scrapeFullCatalog` mode scrapes from the sitemap and fetches individual product pages, which takes longer than category or search scraping.

## Other retail and fashion scrapers

Looking for data from other European retailers? Check out these scrapers from our collection:

- [Mytheresa Scraper](https://apify.com/studio-amba/mytheresa-scraper) -- Luxury fashion products and prices
- [Rituals Scraper](https://apify.com/studio-amba/rituals-scraper) -- Premium cosmetics and home fragrance
- [Kruidvat Scraper](https://apify.com/studio-amba/kruidvat-scraper) -- Drugstore, beauty, and health products
- [ICI PARIS XL Scraper](https://apify.com/studio-amba/iciparisxl-scraper) -- Belgian beauty and perfume retailer
- [AS Adventure Scraper](https://apify.com/studio-amba/asadventure-scraper) -- Outdoor and adventure gear
- [Bergfreunde Scraper](https://apify.com/studio-amba/bergfreunde-scraper) -- Climbing and hiking equipment
- [Intersport Scraper](https://apify.com/studio-amba/intersport-scraper) -- European sports retail
- [Helly Hansen Scraper](https://apify.com/studio-amba/hellyhansen-scraper) -- Outdoor and sailing apparel

## Your feedback

Found a bug? Missing a field? Want a feature? Open an issue on the actor's page or reach out through the Apify platform. We actively maintain this scraper and ship fixes fast.