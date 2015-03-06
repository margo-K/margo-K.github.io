#Marketing and A|B Testing
Recently, I started working with the person on our marketing team in charge of the so-called "quantitative marketing". Her first task was to run a Facebook campaign to test several different "creatives" (as a recently learned images are called in the online marketing world). The first level objective of the campaign was to increase downloads of one of our apps. We of course were also measuring clicks on the ad itself (> total installs) and actions within the app (our "conversion events"). Today, my colleague and I met to discuss significance testing. In preparation for our talk, I searched for articles talking about statistical hypothesis testing in terms of marketing that I could provide her with. Though I found a few, it seemed like the relative number of resources focused on this was small and the gap between the math and the implementation was quite small. Additionally, the number of online calculators for this purpose makes it easy to just type some numbers in without understanding the underlying math. 

The objective of this post is to explain the math between hypothesis testing to the marketing audience. As someone who considers math her "first love", I think it's important for people to not just use math but understand it. 

One of the things that our conversation (and my research) made me wonder was how much people making marketing and other business decisions EVER think about statistical significance? My guess is if ever, people only think about it in the context of A|B testing, and even then probably not that much since so much of A|B testing is automated. Additionally, all the articles I've found about statistical significance and hypothesis testing use relatively simple examples. If you instead start from something as (seemingly) straightforward as 



##Articles about Math
* [The Math Behind A|B Testing - Amazon](https://developer.amazon.com/sdk/ab-testing/reference/ab-math.html)

##Articles about Marketing and A|B Testing
* [The ABCs Of A/B Testing](http://marketingland.com/the-abcs-of-ab-testing-42554)
* [A|B Testing: Example of a good hypothesis](http://www.marketingexperiments.com/blog/analytics-testing/creating-good-hypothesis.html)
* [A/B Testing: Working with a very small sample size is difficult, but not impossible](http://www.marketingexperiments.com/blog/analytics-testing/testing-small-sample-sizes.html)
** [A Marketer's Guide to Understanding Statistical Significance](http://blog.hubspot.com/marketing/marketers-guide-understanding-statistical-significance)
** [2 Questions That Will Make You A Statistically Significant Marketer](http://marketingland.com/2-questions-will-make-statistically-significant-marketer-91626)
* [A CLEAR PICTURE OF POWER AND SIGNIFICANCE IN A/B TESTS](http://abtestguide.com/calc/)
** [How To Apply Statistical Significance In Business Marketing](http://marketingland.com/statistical-significance-business-114834) - a quick note about the difference between statistical significance in an academic context and in a business context

##Cool Statistical Significance Calculators
* [AB Testguide](http://abtestguide.com/calc/) - includes visualizations of the normal distributions based on the data. Pretty cool.
* [Calculator for Multiple Groups](https://mixpanel.com/labs/split-test-calculator)

##Random Other Stuff
* [A|B Testing Case Studies](https://whichtestwon.com/page-tested/search-results/)

##Questions
1. Why does [this calculator](https://mixpanel.com/labs/split-test-calculator) have different results than [this calculator](http://www.houseofkaizen.com/conversion-rate-optimisation/resources/calculators/split-test-significance/#). Does it have to do with having a "control" vs. just having all four as treatments?