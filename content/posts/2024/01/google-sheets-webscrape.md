---
title: Web Scraping with Google Sheets
date: 2024-01-25
summary: (Hopefully) You’re a responsible investor and track your assets in Google Sheets. However, you encounter a problem.
linkedin: https://www.linkedin.com/posts/giovanni-remonti_googlesheets-webscrape-activity-7155884482099609603-EeLD
---

<div class="img-container">
    <img src="https://res.cloudinary.com/giospic/image/upload/f_auto,q_auto/v1706214493/images/google-sheets-webscrape.webp" />
</div>

(Hopefully) You’re a responsible investor and track your assets in Google Sheets. However, you encounter a problem: the GOOGLEFINANCE function can’t always retrieve data for some TICKERs in certain stock markets. To still get the data you want, for example the closing price, the solution is to web scrape them from other websites, like Morningstar.

Below, I'd like to show you how I got the closing price for AYEM (iShares MSCI EM IMI ESG Screened UCITS ETF USD Acc) listed on XETR (Xetra Trading German Electronic Exchange).

Search your asset in Morningstar, either by ISIN or by Ticker, and save the URL of the page. We are shown a graph and some tables. We need to identify in which table the closing price is located. To do so, right-click and open the Inspect tool of your browser. In the HTML, search for “table” and count in which position the HTML table element is in (don’t count the occurrences). For Morningstar, the closing price is inside table number 4.

Let’s move on to Google Sheets. To web scrape, we use the formula IMPORTHTML(URL, “table”, 4, “it_IT”). Paste inside the URL you copied before. A table is imported into your sheet (in the image, result in yellow). To obtain only the price as a number, it is necessary to make some transformations. Using the function INDEX, we index for row 2 and column 3 (result in orange). Use the SPLIT function to separate the appendix “EUR” using as a delimiter the blank space in between (result in blue). Finally, INDEX again to get column 2 and divide by 1000 to scale and transform the string to a decimal number.

I encountered this problem this morning while ordering my Google Sheet for the new year. I hope this helped or inspired you in some way!