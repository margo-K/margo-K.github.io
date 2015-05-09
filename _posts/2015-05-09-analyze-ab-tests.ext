---
layout: post
title:  "How to analyze A/B tests"
date:   2015-05-09 14:30:00
---
As a Data Scientist, if I use an A/B testing framework to test changes to my product, I want to know exactly what assumptions are underlying that framework and the reports it produces. In this post, I'll explain the approach that Amazon uses to analyzing A/B tests, which also happens to be one of the simplest approaches - the Z test with a Wald interval.

I should also start by saying that if the content of this post seems a bit basic to you, then this particular post is probably not for you. Amazon gives the bare bones math of their approach in [The Math Behind A/B Testing](https://developer.amazon.com/public/apis/manage/ab-testing/doc/math-behind-ab-testing), which should be enough to get most Data Scientists or Statisticians started. This post is not targeted at that group but instead at their colleagues, who may have some statistics background but could use a little bit of a guide to linking what they learned in school to what they're doing at work. There are many great resources, so this post is only intended to provide a bit of signposts to support more intensive study.

###Let's start with an example
Say you run a news website which can be browsed with or without registration. Registering allows readers to get access to premium content and content recommendations and allows you to gather the data needed to build more extensive profiles of readers necessary better tailor content to them. Users aren't registering at the rate you would like, so you decide to add a short block of text under the registration prompt explaining what advantages they will get if they register to see if this affects conversion. Let's call the normal registration prompt Version A and the prompt with the additional information Version B. Suppose we use the Amazon A/B testing framework to test these two variations of our sign up prompt and now we're looking to analyze the results. 

###Modelling the problem
What we're interested in when we run our A/B test is which variation of the registration prompt results in more users registering using conversion rate as our metric. We consider each user who comes to this page to be a potential newly registered user and we consider the users who actually do register to be successes. Mapping this to stastical terms, each unique view is a "trial" and each registration is a "success". Alone, each user's success or failure in registering would be considered a [Bernoulli trial](http://en.wikipedia.org/wiki/Bernoulli_trial). If all of these trials are independent, then the number of successes in N trials (or N unique vistors, in our cases) can be modelled as a [binomial distribution](http://en.wikipedia.org/wiki/Binomial_distribution). Simply put, the binomial distribution tells you what the probability of obtaining n successes is in N independent trials, where each trial can only be a success or a failure and the probability of success (the true conversion rate) is referred to as p.

###Formulating a hypothesis
When I run an A/B test, I randomly assign my incoming customers to one variation or the other. What I want to see is whether changing only the variation in the sign up prompt, in our case, results in any difference in the observed conversion rate between the two groups (p_A and p_B, respectively). The quantity of interest for us is thus the mathematical difference between p_A and p_B. Specifically, I want to test the statement:

	p_B = p_A <=> p_B - p_A = 0.

We thus want to construct a hypothesis test where the statement above is our [null hypothesis](http://mathworld.wolfram.com/NullHypothesis.html). Our [alternative hypothesis](http://mathworld.wolfram.com/AlternativeHypothesis.html) would thus be that
	
	p_B != p_A <=> p_B - p_A !=0.

Speaking more broadly, our null hypothesis states that any difference in our the observed conversion rates for the two variations could be attributed to chance (see "Randomness" below) and our alternative hypothesis states that variations between these two conversion rates are indicative of a true difference in performance between the two variations. 

###Calculating the Test Statistic
To [test a hypothesis](http://mathworld.wolfram.com/HypothesisTesting.html) we must specify a [test statistic](http://en.wikipedia.org/wiki/Test_statistic), which we use to capture information about the data set. In our example, we will use a normal approximation to the binomial distribution (the Wald interval) and thus perform our [hypothesis test using the Z score](http://en.wikipedia.org/wiki/Z-test). Note that we are using this method here because it is the simplest and examining it helps provide some intuition which can be used in other approaches as well. There are definite limitations to using this approximation and there are other alternatives which often perform better. Why we would or wouldn't use the Wald method is beyond the scope of this post, but will perhaps be the topic of a future post. To see how the choice of method affects confidence intervals for your data see [this calculator](http://epitools.ausvet.com.au/content.php?page=CIProportion&SampleSize=200&Positive=35&Conf=0.95&Digits=3). 

The [Z-score](http://mathworld.wolfram.com/z-Score.html) tells how many standard deviations our observed value is away from the mean and is as follows:
	
	z = (X - E[X])/Std(X)


As mentioned in the previous section, the quantity of interest for us here is the difference between the conversion rate of the control, p_A, and the variation, p_B. So for every quantity in the Z score formula, we'll be looking at the quantity for the difference in the conversion rates between Variation A and Variation B. To find what value we should use for the mean term, ```E[X] = E[p_B-p_A]```, we rely on our null hypothesis. In setting up our hypothesis, we are assuming that the null hypothesis is true and then figure out how likely (or unlikely) our observations would be under that assumption. This is equivalent to saying that we assume that p_A and p_B are actually equal, even if in the specific samples we saw they were slightly different. So we get ```E[p_B-p_A] = 0 ```. We also note that our ```X``` term, i.e. the observation term or "point estimate" is just equal to ```p_B - p_A```. Finally, we need to find an expression for our "spread" term, ``Std(X)``` in the formula above. We use the estimated standard error formula which we got from the assumption that we use the Wald interval:

				SE = sqrt(p(1-p)/sampleSize). 

Combining the SE of each variation to get the total variation of ```p_B - p_A```, we get:

		Z_score = (p_B - p_A) / sqrt(SE_A^2 + SE_B^2)

which is the formula Amazon presents. Combining this with a pre-selected p-value, we can now perform a hypothesis test in the standard way.

###Effect of Sample Size
We use the concept of "confidence intervals" around a conversion rate to quantify our degree of certainty about where the true conversion rate lies. Because confidence intervals are just calculated by multiplying the z score of a certain percentile times the standard error, it's clear that from an experimental side, variation in our confidence will come through the standard error term. From the formula for standard error, we can clearly see that a larger sample size (or number of views, in our case) would result in a smaller standard error and a smaller interval on which we think the true conversion rate lies. If we see a 10% conversion rate for our variation, but only 10 people total have seen it so (i.e. 1 person signed up), we can be less sure about this point estimate being close to the real conversion rate than if we had the same conversion rate but 100,000  people had seen the page. Intuitively, this makes sense and we can clearly see that the math agrees with the intuition:

	 10% conversion rate, 10 views => SE ~= 9.5%
	 10% conversion rate, 100,000 views => SE ~= 0.3%. 

It's also worth noting that from this standard error formula we can see that, given the same number of views, the largest error will be when the conversion rate is exactly 50%. The standard error gets smaller if the observed conversion rate is closer to the extremes - 0% or 100%. This is equivalent to saying that the more distant the success and failure rates are from each other, the more certain we can be about our estimate.

###Randomness
In general, when we run an A/B test, we want to be able to say something about this **true conversion rate** instead of just the conversion rate we see in our experiment. More specifically, I run an A/B test not to find out whether Variation A performs better than Variation B for the subset of people who see the test but for all of my customers. In statistical terms, I want to know about the **population** not just a smaller **sample**. I'm using this smaller group of people to get a rough guess (an **estimate**) of what the conversion rate will be in the whole population. I also know that there's going to be some variation from sample to sample, even if they ultimately have the same true conversion rate. If a take a fair coin (50/50 chance of getting heads or tails) and flip it 100 times, I won't always get 50 heads and 50 tails exactly. If I do this twice and I get 51 heads and 49 tails in one go (51% success) and 48 heads and 52 tails in one go (48% success), I won't throw up my hands and say the coin I flipped in the first trial was different from the coin I flipped in the second one. In a similar way, it would be possible for me to get two different conversion rates for my registration prompts with and without text without their **true** conversion rates actually being different. At the end of the day, when we act on the conclusions we draw from an A|B test or from any other statistical test, we're still just making our best guess, given the evidence. What understanding the math behind A|B testing gets me is some sense of whether a difference in conversion rate would constitute enough evidence for me to "bet" on my variation.

So what makes for a good bet? Traditionally, we use [p-values](http://mathworld.wolfram.com/P-Value.html) to quantify what "good enough". There are a [number of issues](https://xkcd.com/882/) you can run into when relying on p-values alone. More on that in my next post in this series about A/B Testing.