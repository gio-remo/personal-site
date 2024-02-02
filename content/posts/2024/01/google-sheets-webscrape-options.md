---
title: Web Scraping futures prices
date: 2024-02-02
summary: Google Sheets definitely has some limitations, but with a bit of creativity and App Script they can sometimes (!) be bypassed.
linkedin: https://www.linkedin.com/posts/giovanni-remonti_webscraping-googlesheets-data-activity-7158413616659001347-MhCu
---

<div class="img-container">
    <img src="https://res.cloudinary.com/giospic/image/upload/f_auto,q_auto/v1706876048/images/webscraping-futures.webp" />
</div>

After my last post regarding webscraping in Google Sheets, a friend asked me if I could help him collect some data.

For his trading strategy, he needs the closing price for the future on the **VIX index** (= an indicator measuring the market’s expectation of volatility over the next 30 days for the US stock market).

[This](http://vixcentral.com/) website displays the data we want in a (damn) popup and the function `IMPORTHTML` can’t be used because our target isn’t within a table or a list. Indeed, this function and similars (`IMPORTDATA` or `IMPORTXML`) have some requirements and aren't always appropriate.

In this case,  **App Script**, the class `UrlFetchApp` and its function `fetch(URL)` solved our problem.

1. The values we want are (luckily) explicitly declared in the JS.
2. The function `fetch(URL)` makes the request and returns an `HTTPResponse` object.
3. With the method `getContentText()` we take the raw response, which we can then transform to extract and return the desired data.

Google Sheets definitely has some limitations, but with a bit of creativity and App Script they can sometimes (!) be bypassed.