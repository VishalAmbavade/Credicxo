# Credicxo
The repository contains the internship task given by Credicxo.

**Given Task**
In this task we want you to scrape a minimum hundred URLs.
The URL will be in format of "https://www.amazon.{country}/dp/{asin}". The country code and Asin parameters are in the CSV file https://docs.google.com/spreadsheets/d/1BZSPhk1LDrx8ytywMHWVpCqbm8URTxTJrIRkD7PnGTM/edit?usp=sharing . The CSV file contains 1000 rows.
Use Selenium or bs4 to Scarpe the following details from the page.
1. Product Title
2. Product Image URL
3. Price of the Product
4. Product Details
If any URL throws Error 404 then print the {URL} not available and skip that URL.

### Approach:
1. First thing I did was analyzed the CSV file that was provided with `Asin` and `country` columns.
2. Then I had to create a URL based on these values which I did by using string concatenation in Python.
3. I had to make sure that whatever code I write should work for at least one URL anf then I can move forward and adapt it for other URLs if needed.
4. I started from the first URL, went to the webpage and found that it was throwing error (It was 404 error). Since Amazon handles `404` differently than anyone else, I had to sweat there.
5. So, I moved to the URL that was working and inspected the page using `Inspect` in Google Chrome.
6. Getting the Product title was easy. Did not have any problems with that.
7. Although, getting product image link and other parameters was kinda hard.
8. One thing that made this whole scraping business a nightmare was not all the products follow the same `html` code. So I had to check multiple URLs to cover all the corner cases.
9. Other thing which made me go crazy was that Amazon thre `503` when I tried scraping continuously. I had to stop scraping just to get out of that virtual jail.
10. But finally I figured out the `headers` required to scrape the data without getting blocked.
11. Once I ran the code for first 10 values, again I found shortcomings in the code. Like I said earlier, Not all the pages on amazon follow same coding style.
12. In some cases, titles have subtitles as well. I had to take care of that.
13. Some products have descriptions as paragraphs while others are in list format.
14. Some products have prices in a text format whereas others are button texts. Also, some have `euro` symbol in the beginning and some have at the back.
15. I scraped the data by the batches of 100 as was asked and saved them as `csv`s. Finally, I appended these `csv`s with all the data at one place.
16. But, I eventually conquered them all and with multiple `try-catch` and `nested try-catch` blocks, I was able to scrape the data.

### Data Cleaning
1. There was no task related to data cleaning in the given pdf although, I did it anyhow.
2. The scraped data looked really bad. The description column in particular had multiple lines content and had special character and unnecessary spaces. Which I removed to prettify it.
3. Removed all the currency symbols (because all were `euro`) and replaced `,` with `.`

### Saving the output as JSON and in DB
1. I saved the output of scraping in a JSON file to upload it here.
2. Next thing I did was finding a free `postgreSQL` db. I found `ElephantSQl` fit to my needs so I went ahead with it and dumped the data in it.
