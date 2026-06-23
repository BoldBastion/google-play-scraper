[Google Play Scraper](https://apify.com/sourabhbgp/google-play-scraper?fpr=data)

# Google Play Store Scraper — 100 Free | App Details, Reviews & Search

Scrape app details, user reviews, and search results from the Google Play Store. Fast HTTP-only scraper — no browser needed. Supports all countries and languages.

## 💰 Pricing

- **100 free results** — lifetime, no credit card needed
- After that: **$2 per 1,000 results** (pay-per-event)

| Results | Cost |
| --- | --- |
| 100 | Free |
| 1,000 | $2 |
| 10,000 | $20 |
| 100,000 | $200 |

## 🔍 What can you scrape?

### App Details

Full app information: name, developer, description, rating (with 1-5 star histogram), exact install count, price, category, content rating, screenshots, release notes, privacy policy, and more.

### User Reviews

Up to 20 reviews per app with: author name, star rating, review text, thumbs-up count, date, and app version at review time.

### Search Results

Search the Play Store by keyword. Returns app name, developer, rating, install count, price, and category for each result.

## 📥 Input

| Field | Type | Default | Description |
| --- | --- | --- | --- |
| `urls` | string[] | `["com.whatsapp"]` | App URLs, package IDs, or search keywords |
| `mode` | enum | auto-detect | `app-details`, `reviews`, or `search` |
| `maxResults` | integer | 50 | Max results to return (0 = unlimited) |
| `language` | string | `en` | Language code (en, de, fr, ja...) |
| `country` | string | `us` | Country code (us, gb, in, de...) |

### Auto-Detection

- `play.google.com/store/apps/details?id=...` → app-details
- `play.google.com/store/search?q=...` → search
- `com.whatsapp` (package ID format) → app-details
- `weather app` (plain text) → search
- Set mode to `reviews` explicitly to get reviews instead of app details

### Example Input

```
{
    "urls": ["com.whatsapp", "com.mojang.minecraftpe"],
    "mode": "app-details",
    "maxResults": 10,
    "language": "en",
    "country": "us"
}
```

## 📤 Output

### App Details

```
{
    "type": "app-details",
    "packageId": "com.whatsapp",
    "name": "WhatsApp Messenger",
    "developer": "WhatsApp LLC",
    "rating": 4.7,
    "ratingCount": 232743506,
    "ratingHistogram": { "1": 7100000, "2": 2200000, "3": 6700000, "4": 20400000, "5": 196300000 },
    "installs": "10,000,000,000+",
    "installsExact": 11812982503,
    "price": 0,
    "free": true,
    "category": "Communication",
    "url": "https://play.google.com/store/apps/details?id=com.whatsapp"
}
```

### Reviews

```
{
    "type": "review",
    "packageId": "com.whatsapp",
    "appName": "WhatsApp Messenger",
    "authorName": "John Doe",
    "rating": 5,
    "text": "Great app!",
    "thumbsUpCount": 42,
    "reviewDate": "2026-04-01T00:00:00.000Z",
    "appVersion": "2.26.4.10"
}
```

### Search Results

```
{
    "type": "search-result",
    "packageId": "com.whatsapp",
    "name": "WhatsApp Messenger",
    "developer": "WhatsApp LLC",
    "rating": 4.7,
    "installs": "10B+",
    "price": 0,
    "free": true,
    "category": "Communication"
}
```

## 💡 Use Cases

- **App market research** — compare ratings, installs, and reviews across competitors
- **Review monitoring** — track user sentiment for your app or competitors
- **App discovery** — find apps by keyword with ratings and install data
- **Lead generation** — find developer contact info (email, website) from app listings
- **Investment research** — track app growth via install counts and rating trends

## ⚡ Tips

- Use package IDs (`com.whatsapp`) for fastest results — no URL parsing needed
- Reviews mode returns up to 20 reviews per app (sorted by most relevant)
- Set `language` and `country` to get localized results (e.g., `language: "ja"`, `country: "jp"` for Japan)
- The `ratingHistogram` field shows exact counts per star — useful for sentiment analysis
- `installsExact` gives the precise install count (e.g., 11,812,982,503) vs the rounded `installs` field ("10B+")