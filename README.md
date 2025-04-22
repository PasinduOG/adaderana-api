# 📰 Ada Derana Scraper (v1.1.1)

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

You can create a simple server to run the API:

```javascript
// server.js
const express = require('express');
const adaDerana = require('adaderana-scraper');
require('dotenv').config(); // Load environment variables from .env file

const server = adaDerana.createAdaDeranaAPI();
const PORT = process.env.PORT;

server.listen(PORT, () => {
    console.log(`Server is running on http://localhost:${PORT}`);
});
```

### 🛠️ As an Express API

```javascript
const { createAdaDeranaAPI } = require('adaderana-scraper');
require('dotenv').config(); // Load environment variables

const app = createAdaDeranaAPI();

// Optional: Add more routes or middleware here

const PORT = process.env.PORT;
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

## 🔧 Environment Configuration

You can configure the application using environment variables:

### Available Environment Variables:
- `PORT`: The port number for the server (default: `3000`)

### Setting Environment Variables:

#### Using .env file (recommended for development):
Create a `.env` file in your project root:

```
PORT=8080
```

Then install the dotenv package:

```bash
npm install dotenv
```

And import it in your server file as shown in the usage examples above.

#### Using command line (for production):

```bash
# Linux/Mac
PORT=8080 node server.js

# Windows Command Prompt
set PORT=8080 && node server.js

# Windows PowerShell
$env:PORT=8080; node server.js
```

## 📚 API Documentation

### 🔄 API Endpoints

#### Basic Endpoints (createAdaDeranaAPI)

#### 📋 GET `/hotNews`

Returns the latest hot news headlines from Ada Derana Sinhala.

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
      "time": "Published time",
      "url": "https://sinhala.adaderana.lk/news-url"
    }
    // More news items...
  ]
}
```

**Error Response Format:**
```json
{
  "code": 500,
  "code_creator": {
    "name": "Pasindu Madhuwantha",
    "github": "@PasinduOG"
  },
  "error": "Failed to fetch headlines"
}
```

### ⚙️ Functions

#### 🔧 `createAdaDeranaAPI()`

Creates an Express application with the AdaDeranaAPI routes configured.

**Returns:** Express application instance with the following endpoints:
- `GET /hotNews` - Returns the latest hot news headlines

#### 🔍 `scrapeHotNews()`

Scrapes hot news headlines directly from Ada Derana Sinhala website.

**Returns:** Promise that resolves to an array of news objects with the following properties:
  - `news`: The headline of the news article
  - `details`: A summary or snippet of the news article
  - `time`: The published time of the article
  - `url`: The full URL to the news article

## 📝 License

MIT

## 👨‍💻 Author

- Pasindu Madhuwantha ([@PasinduOG](https://github.com/PasinduOG))