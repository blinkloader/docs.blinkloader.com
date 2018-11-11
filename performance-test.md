# Performance Test

Nice way to discover major website speed issues in the context of SEO.
We've put all important metrics together and keep adding more.

With the current version of the test you can see:
* page speed insights
* time to interactive
* time to first meaningful paint
* performance of your SERP competitors

Don't hesitate to suggest new features.

## Quickstart

Go to the <a href='https://blinkloader.com/test' target='_blank'>test page</a>.
Then enter a search query and the page you'd like to test. Here is an example:

<img src='https://cdn.staging-blinkloader.com/express/0c0o6rfmA2PD1wg0tggidApum/performance_test_inputs.png' />

It may take some time, because the system visits your website and waits until it's
fully loaded. Then you should see the results.

<img src='https://cdn.staging-blinkloader.com/express/2eSxrYuzquqFxxlJ0zsq81Qoz/performance_test_example.png' />

Further you can read more about each metric and why it's useful.

## Competition by Performance

Starting from July 2018 Google has began using page speed as a ranking factor for mobile searches.
Blinkloader performance test helps you understand how much faster your website should be in order
to outperform your SERP competitors.

Here is an example. We'll take a website with many organic search keywords. In our case,
that would be "upwork.com", with search keywords as "hire python developers".

<img src='https://cdn.staging-blinkloader.com/express/xBXJyWQE2aqor5RrBsI3mGNtn/performance_test_competitors.png' />

The seconds on the left are either TTI (time to interactive) or FMP (time to first meaningful paint),
depending on what you choose. You can switch between those in top bar filters.

If you want your page to be among top 3 results for a particular search keyword, then speed is really
important. This metric and insights are here for you to simplify the process.

## FMP (First Meaningful Paint)

According to official <a href='https://developers.google.com/web/tools/lighthouse/audits/first-meaningful-paint' target='_blank'>Google Documentation</a>, this metric identifies the time at which the user
feels that the primary content of the page is visible. We use Google Lighthouse to do the calculation.

This is an example from the test results:

<img src='https://cdn.staging-blinkloader.com/express/GXnlqtXgfRWvaCgCToFU0TqRK/performance_test_fmp.png' />

## TTI (Time to Interactive)

The Time to Interactive (TTI) metric measures how long it takes a page to become interactive.
"Interactive" is defined as the point where:
* The page has displayed useful content, which is measured with First Contentful Paint.
* Event handlers are registered for most visible page elements.
* The page responds to user interactions within 50 milliseconds.

Some sites optimize content visibility at the expense of interactivity. This can create a frustrating user experience. The site appears to be ready, but when the user tries to interact with it, nothing happens.

The definition above is taken from <a href='https://developers.google.com/web/tools/lighthouse/audits/time-to-interactive' target='_blank'>official Google docs</a>.

This is an example from the test results:

<img src='https://cdn.staging-blinkloader.com/express/1S8LElHDmL367jT1JhBTkbv2m/performance_test_tti.png' />

## Page Speed Insights

One more gem from Google is their Page Speed Insights service. We decided to add those insights to the test
as well. The insights are very actionable and help to improve website performance significantly.

This is an example from the test results:

<img src='https://cdn.staging-blinkloader.com/express/F8qwie8n2gJQf6STnPdrrCXHh/page_speed_insights.png' />

## Read more about other products

* [Automatic Image Optimizer](automatic-image-optimizer.md)
* [Express CDN](express-cdn.md)
