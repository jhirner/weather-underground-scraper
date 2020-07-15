# weather-underground-scraper
 A tool for scraping historical weather data.


 ## Installing / Getting Started

 1. Clone this repo to a directory of your choice.
 2. Ensure the you have the required libraries installed. (See Requirements.)
 2. Open a Python 3 console in the terminal or your favorite virtual environment.
 3. `from weather_underground_scraper import scrape`
 4. `scrape()`
 5. Follow the on-screen prompts.

 After executing `scrape()`, you will be prompted for the following:
 * A base Weather Underground URL for the location of interest.
 * The range of dates for which you want to scrape data.
 * Your preferred name for a local SQLite file & table for storing the data.

 ## Tested With
 * Python 3.8.2
 * Weather Underground, through 14 July 2020


 ## Workflow

 ### General process:

 * Prompts the user for the information outlined above.
 * Establishes a connection to the local SQLite database using Dataset.
 * Opens a hidden Chrome window via Selenium.
 * Divides the date range into individual days. Accesses the Weather Underground
   page for each date and parses it using BeautifulSoup:
   * Parses the table headers and extracts units of measure from the first data
     row. Formats these into SQL-friendly, column labels such as "Time",
     "Humidity_pct", or "Wind_Speed_mph".
   * Parses all the data rows, one for each hour of the day.
   * Writes the day's data to the SQLite database.


 ### Heirarchy of functions, in the order they are called upon execution:
 * scrape(): The only user-callable function.
   * parse_date_str(): Converts dates as YYYY-MM-DD to the corresponding seconds
     from epoch. Used only for handling the user's input date range.
   * epoch_to_str(): Converts seconds from epoch back to YYYY-MM-DD, a string
     which is appended to the user-specified Weather Underground base URL to
     access data from a specific date.
   * parse_wu_page(): Coordinates the two subservient parsers below & writes
     results to the database.
     * clean_column_labels(): Generates SQL-friendly column labels.
     * parse_row(): Parses weather measurements.

 ## Requirements
 * [Beautiful Soup 4](https://www.crummy.com/software/BeautifulSoup/)
 * [Dataset](https://dataset.readthedocs.io/en/latest/)
 * [Selenium](https://www.selenium.dev/)


 ## Contributing

 If you'd like to contribute, please do. I also invite your constructive
 criticism of my code, as I am still learning!


 ## Licensing

 The code in this project is licensed under MIT license:

 Copyright 2020 Joshua Hirner.
