# Kvickly Scraper - Danish Grocery Products & Prices

Extract structured data from [www.kvickly.dk](https://www.kvickly.dk) — current Kvickly leaflet rows from www.kvickly.dk with structured names, prices, unit quantities, comparison prices, validity windows, catalog context and product links for Danish grocery price tracking.

**[Kvickly Scraper - Danish Grocery Products & Prices on Apify →](https://apify.com/blackfalcondata/kvickly-scraper?fpr=1h3gvi)**

---

## 🚀 How to use this actor

> ### 💚 $5 free Apify credits — every month
> No credit card required. No commitment. Cancel anytime.

### 👉 [Sign up free on Apify →](https://console.apify.com/sign-up?fpr=1h3gvi)

1. **Click sign up** — pick GitHub, Google, or email; takes ~30 seconds
2. **Open this actor** — input is pre-filled with a working example
3. **Click Start** — export results as JSON, CSV, or Excel

Your **$5 monthly platform credit** is enough to run this actor right away — and again every month — scraping typically several hundred to several thousand results per run, depending on your input.

## Key features

**Search with filters** — Search by keyword and location. Filter by ↕️ sort by, and more.

**Incremental mode** — Only get new or changed listings since your last run. Content hash per listing — no duplicates, no re-processing.

**Change classification** — Track unchanged, expired across runs. Build audit trails of how listings evolve over time.

**Compact output** — Emit core fields only (AI-agent / MCP-friendly). Keeps response size small for LLM workflows.

**Result cap** — Stop after N listings (up to 10.000). Set to 0 for the full catalog.

**Export anywhere** — Download as JSON, CSV, or Excel. Stream via Apify API, webhooks, or integrations with Make, Zapier, Airbyte, Keboola.

**Structured data** — Every listing returns the same schema with consistent field naming. All fields always present — `null` when unavailable, never omitted.

---

## Use cases

**Data pipeline automation**
Integrate with your ETL pipeline to collect structured listings from www.kvickly.dk on a schedule. Export to CSV, JSON, or directly to your database. Use compact mode to control output size.

**Market research**
Monitor listings, track trends, and analyze market dynamics with structured, deduplicated data from www.kvickly.dk.

**Change monitoring**
Run daily or hourly in incremental mode to capture only new, updated, or expired listings. Perfect for price-tracking, churn analysis, and alerting pipelines.

**AI / LLM training data**
Structured JSON per listing is ready for RAG pipelines, embeddings, and agent workflows. Compact mode trims tokens for LLM context windows.

---

## Quick start

```json
{
  "query": "mælk",
  "maxResults": 25
}
```

---

## Input parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `query` | string | — | Optional keyword filter across product names and descriptions, e.g. "mælk", "kaffe", "økologisk". Leave empty to export all matching leaflet products. |
| `catalogIds` | array | `[]` | Optional exact catalog IDs. Leave empty to use active Kvickly catalogs automatically. |
| `maxResults` | integer | `0` | Maximum number of product rows to emit. Use 0 for unlimited. |
| `sortBy` | enum | `"discount-desc"` | Optional ordering before maxResults is applied. |
| `includeCatalogInserts` | boolean | `true` | Include catalog inserts such as wine or themed leaflets when they are active. |
| `includeFutureCatalogs` | boolean | `false` | Include catalogs whose validity window starts in the future. |
| `includeExpiredCatalogs` | boolean | `false` | Include catalogs whose validity window already ended. |
| `incrementalMode` | boolean | `false` | Compare leaflet rows against previous run state and emit NEW, UPDATED and optionally EXPIRED rows. |
| `stateKey` | string | — | Stable identifier for incremental tracking. Leave empty to auto-generate from query, catalog IDs, sorting, maxResults and catalog filters. |
| `emitUnchanged` | boolean | `false` | Include rows with no detected change in incremental output. |
| `emitExpired` | boolean | `false` | Include rows that disappeared since the previous run for the same state key. |
| `telegramToken` | string | — | Telegram bot token from @BotFather. Required for Telegram notifications. |
| `telegramChatId` | string | — | Telegram chat or channel ID. Required when telegramToken is set. |
| `discordWebhookUrl` | string | — | Discord incoming webhook URL. |
| `slackWebhookUrl` | string | — | Slack incoming webhook URL. |
| `notificationLimit` | integer | `10` | Maximum number of product rows included in notification messages. |
| `notifyOnlyChanges` | boolean | `false` | When Incremental Mode is on, only send notifications for NEW and UPDATED rows. |
| `whatsappAccessToken` | string | — | WhatsApp Cloud API token. Recipient must have messaged the business number within the last 24 hours. |
| `whatsappPhoneNumberId` | string | — | Your WhatsApp Business phone-number ID. |
| `whatsappTo` | string | — | Recipient phone in E.164 format without +, e.g. "4512345678". |
| `webhookUrl` | string | — | Receives a JSON POST with {metadata, items} after each run. |
| `webhookHeaders` | object | — | Optional JSON object of custom headers, e.g. {"Authorization":"Bearer ..."}. |
| `compact` | boolean | `false` | Keep core product fields and drop page coordinates, tags and catalog detail fields. |
| `excludeEmptyFields` | boolean | `false` | Drop null, empty strings, empty arrays and empty objects from each output row. |
| `appConnector` | string | — | Optional. Pick a connected app under Settings → API & Integrations to receive your results. |
| `mcpIssueTeam` | string | — | Only when the connected app is an issue tracker: the team name or ID the summary issue is created under. |

---

## Output fields

Every listing returns the same 40-field schema. Missing values are `null` — never omitted.

- `leafletRowKey`
- `offerId`
- `productId`
- `name`
- `offerTitle`
- `description`
- `brand`
- `category`
- `departmentName`
- `price`
- `normalPrice`
- `currency`
- `discountPercent`
- `quantityText`
- `amount`
- `unit`
- `unitSizeFrom`
- `unitSizeTo`
- `unitMeasure`
- `piecesFrom`
- `piecesTo`
- `comparePrice`
- `compareUnit`
- `productImageUrl`
- `productUrl`
- `validFrom`
- `validTo`
- `publishedAt`
- `catalogId`
- `catalogLabel`
- `catalogValidFrom`
- `catalogValidTo`
- `catalogTags`
- `catalogTypes`
- `page`
- `pageImageUrl`
- `pageThumbUrl`
- `viewerUrl`
- `hotspotBox`
- `scrapedAt`

---

## Sample output

One object per listing. Here is a real example from a production run:

```json
{
  "leafletRowKey": "50e6bd619aea7ed7d56e470bd369dfe3ce53b665",
  "offerId": "r8u7ooRXFhUmB7d6OBRIS",
  "productId": "8008863039597",
  "name": "BIANCO FUOCO SALENTO ITALIEN 75 CL 12,5%",
  "offerTitle": "Fuoco",
  "description": "Italien. Før-pris 79,95. Tilbud gælder 19.juni - 2. juli 2026. 75 cl. Literpris 46,67. Frit valg.",
  "brand": null,
  "category": null,
  "departmentName": null,
  "price": 35,
  "normalPrice": 79.95,
  "currency": "DKK"
}
```

*Truncated — full records contain 40 fields. See Output fields for the complete schema.*

**[Try Kvickly Scraper - Danish Grocery Products & Prices now — $5 free credit, no credit card →](https://apify.com/blackfalcondata/kvickly-scraper?fpr=1h3gvi)**

---

## Pricing

Pay only for what you extract. No subscription required — Apify's free $5 credit covers thousands of results.

| Event | Price (USD) |
| --- | --- |
| Actor Start | $0.01 |
| Result | $0.002 |

See the [actor on Apify](https://apify.com/blackfalcondata/kvickly-scraper?fpr=1h3gvi) for current pricing.

---

## FAQ

**How do I scrape www.kvickly.dk?**
Use this actor on Apify to extract structured data from www.kvickly.dk. Configure your search query and filters in the input, then click Start — no coding required.

**How do I get www.kvickly.dk data as JSON, CSV, or Excel?**
The actor writes each listing to Apify's dataset. Download as JSON, CSV, or Excel from the Console, stream via the API, or push to Make, Zapier, Airbyte, or Keboola.

**Is it legal to scrape www.kvickly.dk?**
Web scraping of publicly available data is generally legal. This actor only accesses publicly visible information. Always check www.kvickly.dk's terms of service for your specific use case.

**How much does it cost?**
Pay-per-event pricing — you only pay for listings extracted. Apify's free $5 credit is enough to run thousands of results before you pay anything.

**How does incremental mode work?**
Each listing gets a content hash. On subsequent runs, only new or changed listings are emitted — saving time, compute, and storage. Expired listings can be tracked separately.

**Do I need an API key or credentials?**
No. Just sign up for Apify, paste your input, and click Start. No credit card required.

---

## Related products by Black Falcon Data

[Browse all Black Falcon Data actors →](https://apify.com/blackfalcondata?fpr=1h3gvi)

---

## Getting started with Apify

New to Apify? [Create a free account with $5 credit](https://console.apify.com/sign-up?fpr=1h3gvi) — no credit card required.

1. Sign up — $5 platform credit included
2. Open [Kvickly Scraper - Danish Grocery Products & Prices](https://apify.com/blackfalcondata/kvickly-scraper?fpr=1h3gvi) and configure your input
3. Click **Start** — export results as JSON, CSV, or Excel

Need more later? [See Apify pricing](https://apify.com/pricing?fpr=1h3gvi).

---

## About Black Falcon Data

Black Falcon Data builds production-grade web scrapers for job boards and marketplace data. Browse our full actor catalog at [www.blackfalcondata.com](https://www.blackfalcondata.com).

---

*Last updated: 2026 06*
