# FindStock

## Overview

The FindStock Website offers an intuitive interface for beginners and traders to search for an individual stock and make informed decisions. The homepage emphasizes a search-first approach with minimal distractions, while individual stock pages focus on delivering actionable insights with interactive charts and fundamental data.

### Problem Space

Many beginner investors and traders struggle to find and analyze stock market data in an accessible, user-friendly format. Existing platforms often provide complex interfaces and lack simplified insights for beginners or actionable tools for advanced users.

### User Profile

**Target Users:**
- **Beginner Investors:** Need simplified stock data and accessible insights.
- **Experienced Traders:** Require real-time updates, advanced screening, and technical analysis tools.

### Features

1. **Minimalist Search-Focused Homepage**
   - **Design:** A Google-like search bar at the center for entering stock symbols or company names.
   - **Quick Links:** Below the search bar, links to popular stocks (e.g., AAPL, TSLA) for faster access.

2. **Stock Detail Page**
   - **Overview Section:** Prominently displays:
     - Stock ticker and name.
     - Current price, daily change (%), and volume.
   - **Interactive Chart:** Candlestick chart with adjustable timeframes (1D, 1W, 1M, etc.).
   - **Key Metrics:** Market cap, P/E ratio, dividend yield, and technical indicators.
   - **News Section:** Latest articles related to the stock from the News API.

---

## Implementation

### Tech Stack

**Frontend:**
- **React.js:** For responsive and modular component-based development.
- **Chart.js / TradingView Widget:** For seamless integration of candlestick charts.

**Backend:**
- **Node.js with Express:** Handles real-time data queries and API routing.
- **MySQL Database:** Stores stock-related data for analysis.

---

### APIs

- **Alpha Vantage:** For stock and technical data.
- **News API:** For relevant updates.

---

### Sitemap

1. **Home Page:**
   - Minimal search-centric interface with quick links to popular stocks.
2. **Stock Detail Page:**
   - Combines real-time price data, charts, and news.

---

### Mockups

1. Homepage:
   ![Homepage](./src/images/Screenshot%202024-11-19%20at%208.36.35 PM.png)
2. Stock Detail Page:
   ![Stock Detail Page](./src/images/Screenshot%202024-11-19%20at%208.36.59 PM.png)

---

## Data

The data for the Stock Market Assessment Website revolves around two primary entities: **Stocks** and **News Articles**.

### Stocks
**Attributes:**
- `symbol`: Stock ticker symbol (e.g., AAPL, TSLA).
- `price`: Current stock price.
- `marketCap`: Market capitalization.
- `volume`: Trading volume.
- `peRatio`: Price-to-earnings ratio.
- `historicalData`: Array of historical price points (e.g., date, opening price, closing price, volume).
- `indicators`: Technical indicators like RSI, moving averages, and MACD.

### News Articles
**Attributes:**
- `id`: Unique identifier for the article.
- `title`: Headline of the article.
- `content`: Full article content.
- `publishedAt`: Publication date and time.
- `relatedSymbol`: The stock symbol(s) associated with the article.

**Relationships:**
- **Stocks ↔ News Articles:**
  - Each article is linked to one or more stock symbols.
  - A stock can have multiple related news articles.

---

## Endpoints

### 1. Stock Data Endpoints

- **GET /api/stock/:symbol**
  - **Description:** Retrieves real-time and historical data for a specific stock.
  - **Parameters:** `symbol` (string, required) - Stock ticker.
  - **Example Response:**
    ```json
    {
      "symbol": "AAPL",
      "price": 150.25,
      "marketCap": 2400000000000,
      "volume": 9000000,
      "peRatio": 28.5,
      "historicalData": [
        { "date": "2024-11-01", "open": 148.5, "close": 150.25, "volume": 8900000 },
        { "date": "2024-11-02", "open": 150.0, "close": 149.75, "volume": 8500000 }
      ],
      "indicators": {
        "rsi": 56.3,
        "movingAverages": { "50_day": 147.8, "200_day": 140.5 }
      }
    }
    ```

- **GET /api/stocks/trending**
  - **Description:** Returns a list of trending stocks based on volume and price changes.
  - **Example Response:**
    ```json
    [
      { "symbol": "AAPL", "price": 150.25, "change": 1.5 },
      { "symbol": "TSLA", "price": 240.5, "change": 3.2 }
    ]
    ```

### 2. News Endpoints

- **GET /api/news/:symbol**
  - **Description:** Fetches news articles related to a specific stock symbol.
  - **Parameters:** `symbol` (string, required) - Stock ticker.
  - **Example Response:**
    ```json
    [
      {
        "id": 1,
        "title": "Apple announces new product lineup",
        "content": "Apple unveiled its latest product range at a press event today...",
        "publishedAt": "2024-11-15T08:00:00Z",
        "relatedSymbol": "AAPL"
      }
    ]
    ```

- **GET /api/news/recent**
  - **Description:** Fetches recent financial news.
  - **Example Response:**
    ```json
    [
      {
        "id": 3,
        "title": "Tesla's record-breaking Q4 earnings",
        "content": "Tesla reported record earnings this quarter...",
        "publishedAt": "2024-11-18T07:00:00Z",
        "relatedSymbol": "TSLA"
      }
    ]
    ```

---

## Roadmap

### Week 1:
- Build frontend for homepage and stock detail pages.
- Set up backend endpoints for fetching stock data (e.g., `/api/stock/:symbol`).
- Integrate Alpha Vantage and News API.

### Week 2:
- Implement charts and timeframes on stock detail pages.
- Add quick access links to commonly searched stocks.
- Perform testing and debugging across devices.
- Finalize UI with responsive design.

---

## Future Implementations

1. **Save Stock to Watchlist:**
   - Add a user-specific watchlist feature for saving stocks.
   - Enable watchlist management with options to remove or prioritize stocks.

2. **Educational Content:**
   - Create accessible guides, tutorials, and articles for beginners.
   - Add interactive learning modules for analyzing stock market trends.

3. **Login/Signup Pages:**
   - Introduce user authentication for personalized features like watchlists.
   - Use JWT for secure authentication and authorization.

4. **Advanced Charting Tools:** Add custom indicators and volume overlays.

5. **Mobile App:** A simplified version for quick stock searches.

6. **Community Insights:** Allow users to share predictions or analyses.
