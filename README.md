# 📰 Ada Derana Scraper

A lightweight API and scraper for Ada Derana Sinhala news content. This package allows you to easily access hot news headlines, summaries, and links from the Ada Derana Sinhala news website.

## 🚀 Installation

```bash
npm install adaderana-scraper
```

## ✨ Features

- 🌐 Express.js API endpoint for hot news
- 🔍 Standalone scraper function
- 🔌 Simple integration with existing applications

## 📘 Usage

### 🖥️ Using a Custom Server (server.js)

You can create a comprehensive server with additional features:

```javascript
// server.js
const express = require('express');
const cors = require('cors');
const morgan = require('morgan');
const helmet = require('helmet');
const { createAdaDeranaAPI, scrapeHotNews } = require('adaderana-scraper');

// Create the base app
const app = express();
const adaDerana = createAdaDeranaAPI();

// Apply middleware
app.use(helmet()); // Security headers
app.use(cors()); // Enable CORS for all routes
app.use(morgan('dev')); // HTTP request logging
app.use(express.json()); // Parse JSON bodies

// Mount the Ada Derana API routes
app.use('/api', adaDerana);

// Root route
app.get('/', (req, res) => {
    res.json({
        status: 'success',
        message: 'Ada Derana API server is running',
        endpoints: {
            hotNews: '/api/hotNews'
        }
    });
});

// Additional endpoint for scraped data
app.get('/api/data', async (req, res) => {
    try {
        const data = await scrapeHotNews();
        res.json({
            status: 'success',
            data
        });
    } catch (error) {
        res.status(500).json({
            status: 'error',
            message: error.message
        });
    }
});

// Error handling
app.use((err, req, res, next) => {
    console.error(err.stack);
    res.status(500).json({
        status: 'error',
        message: 'Something went wrong!'
    });
});

const PORT = process.env.PORT || 3000;
app.listen(PORT, () => {
    console.log(`Ada Derana API server running on http://localhost:${PORT}`);
});
```

### 🛠️ As an Express API

```javascript
const { createAdaDeranaAPI } = require('adaderana-scraper');
const app = createAdaDeranaAPI();

// Optional: Add more routes or middleware here

const PORT = process.env.PORT || 3000;
app.listen(PORT, () => {
  console.log(`Ada Derana API server running on port ${PORT}`);
});
```

### 🧰 As a Scraper

```javascript
const { scrapeHotNews } = require('adaderana-scraper');

async function getNews() {
  try {
    const news = await scrapeHotNews();
    console.log(news);
  } catch (error) {
    console.error('Error scraping news:', error);
  }
}

getNews();
```

## 📚 API Documentation

### 🔄 API Endpoints

#### Basic Endpoints (createAdaDeranaAPI)

#### 📋 GET `/hotNews`

Returns the latest hot news headlines from Ada Derana Sinhala.

#### Extended Server Endpoints (server.js)

#### 🏠 GET `/`
Returns server status and available endpoints information.

#### 📈 GET `/api/hotNews`
The mounted Ada Derana API endpoint for hot news.

#### 📊 GET `/api/data`
Alternative endpoint that also returns hot news data.

**Response Format:**
```json
{
  "code": 200,
  "code_creator": {
    "name": "Pasindu Madhuwantha",
    "github": "@PasinduOG"
  },
  "data": [
    {
      "news": "News headline",
      "details": "News summary",
      "url": "https://sinhala.adaderana.lk/news-url"
    }
    // More news items...
  ]
}
```

### ⚙️ Functions

#### 🔧 `createAdaDeranaAPI()`

Creates an Express application with the AdaDeranaAPI routes configured.

**Returns:** Express application instance

#### 🔍 `scrapeHotNews()`

Scrapes hot news headlines directly from Ada Derana Sinhala website.

**Returns:** Promise that resolves to an array of news objects

## 📝 License

MIT

## 👨‍💻 Author

- Pasindu Madhuwantha ([@PasinduOG](https://github.com/PasinduOG))