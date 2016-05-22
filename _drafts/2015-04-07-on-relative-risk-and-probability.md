---
ID: 516
post_title: On relative risk and probability
author: Jonathan Carroll
post_date: 2015-04-07 21:19:23
post_excerpt: ""
layout: post
permalink: http://jcarroll.com.au/?p=516
published: false
---
I came across a question on <a href="http://math.stackexchange.com/questions/1220875/has-lack-of-mathematical-rigour-killed-anybody-before">Stack Exchange</a> regarding the dangers off ailing to apply mathematical rigor. Interesting read and all, but one comment in particular grabbed my interest. The example given relates to a (likely common) misinterpretation of probabilities and uses a well-known example of medical testing:

Given the following information (I've updated the numbers with current research estimates):
<ul>
	<li><span style="line-height: normal; -webkit-text-size-adjust: auto; background-color: rgba(255, 255, 255, 0);"><a href="http://canceraustralia.gov.au/affected-cancer/cancer-types/breast-cancer/breast-cancer-statistics">0.1% of women have breast cancer (age standardised, stable),</a></span></li>
	<li><span style="line-height: normal; -webkit-text-size-adjust: auto; background-color: rgba(255, 255, 255, 0);"><a href="http://www.cancer.gov/cancertopics/pdq/screening/breast/healthprofessional/page4">80% of mammograms detect breast cancer when it is there,</a></span></li>
	<li><span style="line-height: normal; -webkit-text-size-adjust: auto; background-color: rgba(255, 255, 255, 0);"><a href="http://www.cancer.gov/cancertopics/pdq/screening/breast/healthprofessional/page8">6% of mammograms detect breast cancer when it’s not there,</a></span></li>
</ul>
<span style="line-height: normal; -webkit-text-size-adjust: auto;">what is the probability that a positive mammogram correctly detects breast cancer? </span>

<span style="line-height: normal; -webkit-text-size-adjust: auto;">Not surprisingly, many will take the sensitivity and guess 80%. The true answer is much more frightening. </span>

The way to calculate this is to apply Bayes' Theorem which takes prior information and conditional probabilities into account. It's commonly stated in terms of the probability that '$$A$$' happens given condition '$$B$$' as $$P(A\vert B)$$, where the calculation of that is an updating of the base probability of '$$B$$', $$P(B)$$, by the probability that '$$A$$' will or won't happen.

\[ P(A\vert B) = \frac{P(B\vert A) P(B)}{P(B\vert A) P(B) + P(B\vert A^c) P(A^c)} \]

In the example above, we are considering '$$A$$' as having breast cancer, '$$B$$' being a positive mammogram result. So, what is $$P(A\vert B)$$, the probability of having breast cancer given a positive mammogram? $$P(B)$$ is the base incidence, $$P(B\vert A)$$ is the sensitivity, and $$P(B\vert A^c)$$ is the false positive rate.

Plugging in the numbers,

<span style="line-height: normal; -webkit-text-size-adjust: auto; background-color: rgba(255, 255, 255, 0);">\[ P(A|B) = 0.8 \times 0.001 / (0.8 \times 0.001 + 0.06 \times 0.999) = 0.013 \]</span>

Soak in that for a minute. A positive mammogram only indicates a slightly more than 1% probability that you actually have breast cancer. Now it is important to recall that the base incidence (i.e. probability that you have breast cancer before getting tested) is just 0.1%, so this is an thirteen-fold increase in the prediction. It's a reasonable question then to ask; why do we bother doing these tests? There's a growing movement away from mass arbitrary screenings because the risk of over diagnosis (and subsequent unnecessary surgery) is too great.

A concrete example helps show how these numbers come out. If 100,000 women are mammogram screened, then according to the above values 100 of those women likely have cancer. The screening will detect 80 of those and miss 20, and it will also incorrectly predict that another 6,000 have cancer when they don't. If your screen comes back positive (6,080 positives) then the chances that you're one of the 80 correctly identified is $$80/6080 = 0.013$$.

<span style="line-height: normal; -webkit-text-size-adjust: auto;">I recall Dr Ben Goldacre mentioning things along these lines regarding a 99% sensitivity for very rare diseases. When testing tens of thousands of people, a large number of them will genuinely be false positives.</span>

<span style="line-height: normal; -webkit-text-size-adjust: auto;">It's also worth noting the difference between absolute risk and relative risk. The base incidence rate of 0.1% is a low number. If 'X' (whatever the latest study suggests has a link to cancer) raises your risk by 20%, and (made clear or not) it's actually a rise in your relative risk, then the incidence rate for people exposed to 'X' is still just 0.12%, not 20.1%.</span>