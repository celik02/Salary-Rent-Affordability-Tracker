# Test Ideas for "Salary vs. Rent Affordability Tracker"

In this section, we outline test ideas to ensure that the web scrapers and data processing logic in the project function as expected. These tests will validate that data is correctly parsed, normalized, and structured before it's used for analysis and displayed in the dashboard.

---

## 1. **Test Basic Parsing Structure**

**Goal:** Ensure that the scraper returns results in the expected format (e.g., list of dictionaries or pandas DataFrame). This helps confirm that data is properly extracted and structured before any further processing.

```python
def test_job_scraper_output_format():
    jobs = scrape_jobs("Boston")
    assert isinstance(jobs, list)
    assert "salary" in jobs[0]
    assert "title" in jobs[0]
```

**What this tests:**
- The scraper's output is in a list.
- Each job listing contains necessary fields like salary and title.

## 2. **Test Sample HTML Input**

**Goal:** Use static, controlled HTML files for testing the scraper's ability to parse content. This is particularly useful for continuous integration (CI) testing, as it avoids the need for live web requests.

```python
def test_parse_static_rent_listing():
    with open("tests/sample_rent_listing.html") as f:
        html = f.read()
    results = parse_rent_html(html)
    assert results["rent"] == 1800
    assert results["location"] == "San Francisco"
```

**What this tests:**
- The scraper can extract relevant fields like rent and location from a static HTML file.

## 3. **Test Salary Normalization**
**Goal:** Validate that salary data is properly normalized. This includes handling salary ranges, hourly rates, and any missing or poorly formatted data.

```python
@pytest.mark.parametrize("input_salary,expected", [
    ("$80,000 - $100,000 a year", 90000),
    ("$45 an hour", 93600),
    ("Up to $70,000", 70000),
])
def test_salary_parser(input_salary, expected):
    assert normalize_salary(input_salary) == expected
```

**What this tests:**
- The normalize_salary function can correctly interpret salary ranges, hourly rates, and phrases like "up to" to return a normalized salary.

## 4. **Test Metro Name Extraction**
**Goal:** Ensure that the scraper correctly extracts metro/city names, even when the location format varies. This is essential for identifying which city a job or rental belongs to.

```python
def test_extract_metro_from_location():
    assert extract_metro("Boston, MA") == "Boston"
    assert extract_metro("San Jose, California") == "San Jose"
```

**What this tests:**
- The extract_metro function can correctly parse location names, even when the format varies (e.g., "San Jose, California" vs. "Boston, MA").

## 5. **Mock Network Requests (Advanced)**
**Goal:** Use mocking to simulate network requests and avoid making live web requests during testing. This helps test the scraper's ability to handle real-world scenarios without depending on actual web pages.

```python
@patch("requests.get")
def test_scrape_jobs_mocked(mock_get):
    mock_get.return_value.text = "<html>...</html>"
    jobs = scrape_jobs("Chicago")
    assert len(jobs) > 0
```

**What this tests:**
- The scraper handles a mocked network request and successfully processes the returned HTML.
- It ensures the function behaves as expected without making actual web requests.

## 6. **Error Handling**
**Goal:** Ensure that the scraper gracefully handles errors, such as missing data or broken pages, without crashing.

```python
def test_handle_missing_salary():
    job_data = "<html><div class='title'>Engineer</div></html>"
    parsed = parse_job_html(job_data)
    assert parsed.get("salary") is None
```

**What this tests:**
- The scraper should handle missing fields (like salary) gracefully, returning None or a default value instead of throwing an error.
