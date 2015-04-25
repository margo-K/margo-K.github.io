At the company I work for, we've recently been talking about integrating more A|B testing into our dev cycle.As the person generally responsible for explaining all things statistical, I've started looking for some good resources about how A|B testing actually works that I could share with my colleagues. One of the first things that I found early on in my search for good resources was a short article from Amazon explaining what goes on under the hood in their A|B testing product - [The Math Behind A|B Testing](https://developer.amazon.com/public/apis/manage/ab-testing/doc/math-behind-ab-testing). The article is pretty short and to the point -it gives a basic overview of the reports that the Amazon A|B testing product provides and gives the formulas they use in their calculations. When I forwarded this to one of my colleagues, though, I realized that what it doesn't provide is any real context. Though the calculations they do are simple, if you haven't seen these particular formulas before, you probably have no idea where they came from. This article is an attempt to provide some of the context for the math behind A|B testing. It is targeted at those who have taken a statistics class or two in the past, but do not work with statistics on a day-to-day basis. By the end of it, you should have an understanding of how A|B testing fits in with hypothesis testing in general and the specific assumptions that underlie Amazon's analysis of an A|B test. The goal is not to explain every little aspect of either A|B testing or hypothesis testing but to give you enough about what's going on (statistically) so that you can search for more resources to deepen your understanding on your own.* 

From the way you hear people talk about A|B testing, it can sound a bit like magic (not unlike the way people talk about [Machine Learning](INSERT CITATION)). Have a question? Want to know if Thing One is better than Thing Two? Just A|B test it! Then we'll know!. Well - sort of. To figure out what we will know and what we won't know when we run an A|B test, we first find out what we're testing when we A|B test.

I. A|B testing is hypothesis test on the difference of two proportions
I think people generally have some sense that A|B testing involves a hypothesis test (?) of some sort and there's something (??) involving degree of confidence.

Remember hypothesis testing? Null hypotheses, alternate hypotheses, p-values, significance levels? I can you for sure that if your response is more of a "uh .. sort of?", you are not alone. Even doing something as seemingly simple as describing exactly what we're testing when we run an A|B test is not immediately obvious to everyone. Before you read any further, if you need a bit of a refresher about hypothesis testing in general, I recommend stopping and taking a look at [RECOMMENDATION].

1. Formulate Null and Alternate Hypotheses
Now, back to A|B testing. When we set up an A|B test, we usually have a rough idea of what we want to find out - we want to know whether Option 1 is better than Option 2. We usually define "better" by some sort of conversion rate - i.e. the number of people who **do** the thing we want them to divided by the number of people who **could have** done that thing. Usually the "could have" camp is everyone who got to that point in a funnel or everyone who we showed some variation of a page to. If Option 1 is the current state of affairs and Option 2 is some new variation we're interested in trying, what we're usually interested in finding out is whether conversion_option_2 > conversion_option_1. If you remember your basic Algebra, this is equivalent to  asking whether conversion_option_2 - conversion_option_1 > 0. 

So let's set up the [hypothesis test](http://mathworld.wolfram.com/HypothesisTesting.html). Step 1: Formulate your null and alternate hypotheses. To set up our hypothesis test, we want to first assume that any difference in conversion rate is due to pure chance and shouldn't be an indication that Option 2 is actually any better than Option 1. This initial assumption is what we will call the null hypothesis (H_0)). Our alternate hypothesis will be the hypothesis contrary to this one.

H_0: The conversion rates between Option 1 and Option 2 are the same. (p_1 = p_2 <=> p_1 - p_2 = 0)
H_1: The conversion rates of Option 1 and Option 2 are different (p_1 != p_2 <=> p_1-p_2 !=0)

2. Identify a test statistic
Remember, what we're testing is the difference between two proportions. Our test statistic should 
thus reflect that. The test statistic used in the amazon example is Z_score:

///insert formula.

How did they get here? 
- sum of variances
- eliminated the zero term (the null hypothesis)

2.a. The SE calculation

3. Two sided test, the Binomial Distribution and Normal Approximation

4. Other Notes




The Null Hypothesis in an A|B test
In hypothesis testing, formulating your null and alternative hypothesis is a very important part of setting up the test. Often, you can set up multiple different tests that address the same general problem by specifying slightly different hypotheses. 

So what hypothesis are they testing in the Amazon example?

They're testing:
* the difference of two proportions p_variation_b - p_variation_a
* they're doing a [two-sided test](https://www.khanacademy.org/math/probability/statistics-inferential/hypothesis-testing/v/one-tailed-and-two-tailed-tests) because they're looking at two sides of the probability distribution - i.e. both the sides where Variation A converts better than Variation B and the side where Variation B converts better than Variation A


