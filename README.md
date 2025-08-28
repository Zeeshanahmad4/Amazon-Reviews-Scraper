# 🛒 Amazon Reviews Scraper  

<p align="center">
A BitBash product for structured Amazon review data
</p>

<p align="center">
  <a href="https://www.bitbash.dev/">
    <img alt="BitBash × Amazon Reviews Scraper" src="https://img.shields.io/badge/Built%20by-BitBash-000000.svg?style=for-the-badge">
  </a>
  <a href="https://discord.gg/zX7frTbx">
    <img alt="Discord contact" src="https://img.shields.io/badge/Discord-Appilot-5865F2?logo=discord&logoColor=white&style=for-the-badge">
  </a>
  <a href="https://t.me/devpilot1">
    <img alt="Telegram contact" src="https://img.shields.io/badge/Telegram-@devpilot1-2CA5E0?logo=telegram&logoColor=white&style=for-the-badge">
  </a>
</p>

---

## 📖 Introduction  
**Amazon Reviews Scraper** lets you extract reviews (rating, title, body, author, verified status, helpful votes, review date, etc.) into structured CSV/JSON.  
It’s designed for analytics, sentiment analysis, product research, and competitor benchmarking.  

---

## 📑 Table of Contents
1. [Overview](#overview)  
2. [Header Section Image](#header-section-image)  
3. [Features](#features)  
4. [Why This Matters (Problem Statement)](#why-this-matters-problem-statement)  
5. [Architecture](#architecture)  
6. [Workflow](#workflow)  
7. [Roadmap](#roadmap)  
8. [Python Code Example](#python-code-example)  
9. [FAQ](#faq)  
10. [Maintainers & Contact](#maintainers--contact)  
11. [License](#license)  
12. [Contact Us](#contact-us)  
13. [Footer Image](#footer-image)  

---

## 🔎 Overview  
Amazon reviews drive trust and sales decisions. Yet, accessing and analyzing them at scale is hard due to pagination, dynamic content, and unstructured formats.  
This scraper automates the process to deliver clean, analyzable review datasets.  

---

## 🖼 Header Section Image  
<p align="center">
<img src="hero.png" alt="Amazon Reviews Scraper — Hero Image" width="900">
</p>

---

## ⚡ Features  

| # | Feature                         | What It Does                                                                 | Why It Matters                                                                 |
|---|---------------------------------|------------------------------------------------------------------------------|--------------------------------------------------------------------------------|
| 1 | **Search-based Review Capture** | Scrape reviews by ASIN or direct product URL.                                | Target exactly the products you need.                                          |
| 2 | **Rich Review Schema**          | Extracts rating, title, body, author, verified purchase, helpful votes, etc. | Structured data for reliable analytics.                                        |
| 3 | **CSV/JSON Export**             | Save reviews in multiple formats.                                            | Easy integration with BI tools or code.                                        |
| 4 | **Pagination Handling**         | Iterates through multiple review pages.                                      | Scales beyond the first page of reviews.                                       |
| 5 | **Dedupe Helper**               | Removes duplicates by review_id.                                             | Keeps datasets clean and accurate.                                             |
| 6 | **Sentiment Enrichment (Optional)** | Tags reviews with sentiment/keywords.                                      | Adds instant value for research pipelines.                                     |
| 7 | **Flexible Configurations**     | Control review count, keywords, regions.                                     | Customizable scraping to your project needs.                                   |
| 8 | **White-Hat Positioning**       | No CAPTCHA/anti-bot bypass included.                                         | Keeps repo safe and professional.                                              |

---

## ❓ Why This Matters (Problem Statement)  
- Amazon reviews influence **buyer trust** and **conversion rates**.  
- Competitors and researchers need large volumes of reviews for **trend analysis** and **benchmarking**.  
- Manual review gathering is inefficient.  
- **This scraper solves the bottleneck** by offering structured, automated, and scalable review collection.  

---

## 🏗 Architecture  
<p align="center"><img src="architecture.png" alt="Amazon Reviews Scraper Architecture" width="900"></p>  

**High-Level Flow**:  
1. Chrome automation opens product review pages.  
2. Collector extracts review data into structured schema.  
3. Validator ensures required fields (rating, title, date, etc.).  
4. Writers export to CSV/JSON.  
5. Optional enrichment adds sentiment/keywords.  

---

## 🔄 Workflow  
<p align="center"><img src="workflow.png" alt="Amazon Reviews Scraper Workflow" width="900"></p>  

**Steps:**  
1. Input ASIN or product URL.  
2. Open "All Reviews" section.  
3. Iterate pages and extract fields.  
4. Normalize into schema.  
5. Export CSV/JSON.  
6. Optionally run dedupe & enrichment.  

---

## 🗺 Roadmap  
- [ ] Add dashboard for managing scraping tasks  
- [ ] Multi-language support (EN, ES, DE, FR)  
- [ ] Cloud deploy templates (Docker + CI)  
- [ ] Enrichment plugins (keyword cloud, sentiment graphs)  
- [ ] Parallel scraping with proxy pools  

---

## 🐍 Python Code Example  

```python
from pathlib import Path
import csv, json

rows = [
    {
        "asin": "B08N5WRWNW",
        "product_title": "Echo Dot (4th Gen)",
        "locale": "US",
        "rating": 4.0,
        "title": "Great sound for size",
        "body": "Surprisingly good bass for such a small speaker.",
        "author": "Jane D.",
        "verified_purchase": True,
        "helpful_count": 23,
        "review_date": "2025-08-01",
        "review_id": "R3A1BCXYZ",
        "review_url": "https://www.amazon.com/review/R3A1BCXYZ",
        "product_url": "https://www.amazon.com/dp/B08N5WRWNW"
    }
]

csv_path = Path("sample.csv")
with csv_path.open("w", newline="", encoding="utf-8") as f:
    writer = csv.DictWriter(f, fieldnames=rows[0].keys())
    writer.writeheader()
    writer.writerows(rows)

json_path = Path("sample.json")
json_path.write_text(json.dumps(rows, indent=2), encoding="utf-8")
print("Wrote sample.csv and sample.json")
