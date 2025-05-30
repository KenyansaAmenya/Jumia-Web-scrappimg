# Jumia webscrapping with LUXDEVHQ on (29-05-25)
# Overview
This Jupyter Notebook script performs web scraping of teacup products from Jumia Kenya's website using Selenium and BeautifulSoup, then organizes the data into a structured pandas DataFrame.
# The breakdown:
# 1. Installation & Setup
- pip install selenium bs4 webdriver_manager
# This installs required packages:

 - selenium: For browser automation
 - bs4 (BeautifulSoup): For HTML parsing
 webdriver_manager: Manages ChromeDriver automatically

# 2. Imports
- from selenium import webdriver
- from selenium.webdriver.chrome.service import Service
- from webdriver_manager.chrome import ChromeDriverManager
- from bs4 import BeautifulSoup
- import time
- import pandas as pd
# what the imports do:
- Selenium: Controls a Chrome browser instance
- BeautifulSoup: Parses HTML content
- time: Adds delays for page loading
- pandas: Structures scraped data into a DataFrame

# 3. Web Scraping Process
# A. Initialize Chrome Driver
- using python
driver = webdriver.Chrome(service=Service(ChromeDriverManager().install()))
- this automatically downloads and configures ChromeDriver.

# B. Fetch page
   - using python
- url = "https://www.jumia.co.ke/dining-entertaining-teacups/ceramics--generic/#catalog-listing"
- driver.get(url)
- time.sleep(5)  # Wait for page to load
this:
- Opens the Jumia product listing page.
- time.sleep(5) ensures dynamic content loads fully.
# C. Parse HTML
  - using python
- soup = BeautifulSoup(driver.page_source, 'html.parser')
- products = soup.find_all('div', class_='info')
This extracts all product cards (div elements with class info).
# D. Extract Product Data
![2025-05-30 14 33 10](https://github.com/user-attachments/assets/82995f1a-f06d-47f7-a201-437ef714de01)
This code:
Scrapes:
- Product name (h3.name)
- Current price (div.prc)
- Original price (div.old)
- Discount (div.bdg._dsct._sm)
- Uses conditional checks to handle missing data.
# E. Close Browser
driver.quit()
- Terminates the Chrome session.
# 4. Data Structuring
- df = pd.DataFrame(product_list)
- df.head()
This:
- Converts the scraped data into a pandas DataFrame.
- Outputs the first 5 rows:
![2025-05-30 14 45 38](https://github.com/user-attachments/assets/fa9c7eee-555e-4110-8814-bc43f5dc6ec4)

# Key Observations
Targeted Elements:
- Product names, prices, and discounts are scraped using specific HTML classes.
- Fallback values (e.g., 'no names') handle missing elements gracefully.
Browser Automation:
- Selenium simulates a real user browsing Jumia.
- time.sleep(5) compensates for dynamic content loading (though explicit waits would be more robust).
Data Output:
- Results are stored in a list of dictionaries, then converted to a DataFrame for analysis.
Potential Improvements:
- Replace time.sleep() with Selenium's explicit waits (e.g., WebDriverWait).
- Add error handling for failed page loads or missing elements.
- Scrape additional fields (e.g., ratings, seller info).

# Use Case
This script could be used for:
- Price comparison across similar products.
- Discount tracking to identify deals.
- Inventory analysis for e-commerce research.
The structured DataFrame (df) can be saved to CSV/Excel or analyzed further with pandas.



