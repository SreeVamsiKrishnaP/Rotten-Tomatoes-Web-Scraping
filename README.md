# Rotten Tomatoes Movie Web Scraper

A Python web-scraping project that collects movie information from
Rotten Tomatoes across multiple genres and stores the results in a
structured CSV dataset.

## Project Overview

This project automates the collection of movie metadata from Rotten
Tomatoes. It:

-   Retrieves movie URLs across multiple genres using Rotten Tomatoes'
    browse API.
-   Handles pagination using the API's cursor-based pagination.
-   Removes duplicate movie URLs that appear across multiple genres.
-   Scrapes individual movie pages using `Requests` and `BeautifulSoup`.
-   Extracts structured movie metadata from JSON embedded in the page.
-   Converts the scraped records into a Pandas DataFrame.
-   Exports the final dataset to CSV.

## Technologies Used

-   **Python**
-   **Requests** --- HTTP requests and API access
-   **BeautifulSoup** --- HTML parsing
-   **Pandas** --- data structuring and CSV export
-   **JSON** --- parsing structured data embedded in movie pages

## Genres Covered

The scraper is configured for 14 genres:

-   Action
-   Adventure
-   Animation
-   Comedy
-   Crime
-   Documentary
-   Drama
-   Fantasy
-   Horror
-   Mystery & Thriller
-   Romance
-   Sci-Fi
-   War
-   Western

## Data Collection Process

### 1. Retrieve Movie URLs

The `get_movie_urls()` function accesses Rotten Tomatoes' genre browse
endpoint and retrieves movie URLs using cursor-based pagination.

A target of approximately **200 movies per genre** is requested. The
scraper also checks for duplicate URLs before adding them.

### 2. Track Multiple Genres

Because a movie can belong to more than one genre, the project builds a
mapping between each unique movie URL and all genres associated with it.

This prevents the same movie from being scraped multiple times while
preserving its genre information.

### 3. Scrape Individual Movie Pages

The `scrape_movie()` function sends an HTTP request to each movie URL
and parses the page using BeautifulSoup.

It searches the page's `<script>` elements for structured JSON
containing movie information and extracts:

  Field               Description
  ------------------- ------------------------------------
  `title`             Movie title
  `genres`            Movie genre(s)
  `content_rating`    Content rating
  `release_date`      Release date
  `description`       Movie description
  `audience_rating`   Audience rating
  `director`          Director name
  `url`               Original Rotten Tomatoes movie URL

### 4. Create the Dataset

The collected movie dictionaries are converted into a Pandas DataFrame
for structured storage and inspection.

### 5. Export to CSV

The final DataFrame is exported as:

`rottentomatoes_movies.csv`

## Project Results

The executed notebook collected:

-   **14 genres**
-   Approximately **210 URLs per genre** for most genres
-   **1,820 unique movie URLs**
-   **1,820 successfully scraped movie records**

The Sci-Fi genre returned fewer URLs because the Rotten Tomatoes
endpoint produced a `404 Not Found` response during pagination,
resulting in **120 Sci-Fi URLs**.

## Project Structure

``` text
Rotten-Tomatoes-Web-Scraping/
│
├── Rotten_tomato.ipynb
├── rottentomatoes_movies.csv
└── README.md
```

## How to Run

### 1. Install dependencies

``` bash
pip install requests beautifulsoup4 pandas
```

### 2. Open the notebook

Open `Rotten_tomato.ipynb` in Jupyter Notebook, JupyterLab, or another
compatible environment.

### 3. Run the notebook

Execute the cells in order. The scraper will:

1.  Load the required libraries.
2.  Retrieve movie URLs by genre.
3.  Build the unique movie URL and genre mapping.
4.  Scrape movie details.
5.  Create the Pandas DataFrame.
6.  Export the dataset to CSV.

## Key Learning Outcomes

This project demonstrates practical experience with:

-   Web scraping
-   REST/API-based data collection
-   HTML parsing with BeautifulSoup
-   JSON extraction
-   Cursor-based pagination
-   Duplicate handling
-   Data collection across multiple categories
-   Pandas DataFrame creation
-   CSV data export
-   Basic error handling for HTTP/request and JSON parsing failures

## Notes

The project relies on Rotten Tomatoes' web/API structure at the time the
notebook was created. Website layouts, endpoints, response structures,
and access policies can change, so the scraper may require updates if
Rotten Tomatoes changes its implementation.

Use web-scraping responsibly and respect the website's terms of service
and applicable access rules.

## Author

**Sree Vamsi**
