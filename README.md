# 🏙️ Salary vs. Rent Affordability Tracker

**Where can a junior embedded-systems engineer actually afford to live?**  
This project scrapes salary data for junior embedded software roles and compares it to real-time rental prices across major U.S. metros to calculate affordability and forecast trends.

---

## 📌 Project Overview

This app shows which cities offer a livable balance between income and housing costs for entry-level embedded software engineers. It combines job listings and rental data to compute the **% of income spent on rent**—a key affordability metric—and forecasts trends for the next six months.

### 🔍 Use Case

Relocation insights for:
- Recent grads in embedded systems
- Cost-of-living analysts
- Tech job seekers comparing cities

---

## 🛠️ Components

| Component              | Description |
|------------------------|-------------|
| **Scrapers**           | Gathers job listings from **Indeed/Adzuna** and rental listings from **Craigslist/Zillow** by metro area |
| **Data Store**         | Saves raw HTML and extracted data as **Parquet** tables using **DuckDB** |
| **Compute**            | Cleans and normalizes data, calculates annual rent and % of gross income spent |
| **Output**             | Interactive **Streamlit dashboard** with metro map and time slider |
| **Forecast Add-on**    | Predicts salary-to-rent ratio per city using **SARIMAX** forecasting |

---

## 🧱 Tech Stack

- **Python 3.11+**
- **DuckDB** for in-memory analytics and storage
- **Streamlit** for visualization
- **pandas, NumPy** for data wrangling
- **statsmodels** for forecasting (SARIMAX)
- **BeautifulSoup, requests, or Scrapy** for scraping

---

## 🚀 Getting Started

### 1. Clone the repo

```bash
git clone https://github.com/celik02/Salary-Rent-Affordability-Tracker.git
```

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

---

## 📈 Dashboard Preview

- 🗺️ Map of U.S. metros colored by affordability  
- 📅 Time slider to explore trends over time  
- 📊 Affordability forecasts up to 6 months ahead  

---

## 📅 Roadmap

- [ ] Add historical backfill option  
- [ ] Add export-to-Twitter or alerts  
- [ ] Expand to more job titles / industries



